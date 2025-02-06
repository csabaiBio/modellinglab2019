# Which embedding to choose for data extraction from Whole Slide Images? Does it even matter?

## 1. Short description

Whole Slide Imaging is one of the primary techniques that allows the creation of large pathological datasets. A whole slide image (WSI) usually contains a tissue sample that was prepared using various pathological staining and drying procedures. 
To view such an image there exists a good number of tools such as the softwares SlideViewer and QuPath which offer tools to for example, annotate on the slides. 
However, when it comes to performing analysis on a great amount of images extracted from WSIs, it is generally a better idea to utilise programming packages like openslide-python.

![wsi_p.png](wsi_p.png)

Many machine learning models contain the conversion from image to vector data as a way to compress and highlight the most important information that is then used to perform prediction, classification, etc. Concerning neural networks, 
usually the model yields these "embeddings" right before they are pushed through something like a classification layer, making the task being performed on sequential (1D) instead of image (2D) data. There are a great many options to choose from regarding embedding generation with the goal of image classification. 
Examples: any convolutional network, pretrained models like ResNet50, Vision Transformeres, etc. (In truth, even methods like putting the tissue under a microscope and measuring infrared spectra from its surface counts as generating embeddings.)

One may ask the question: Does it matter what method/model we generate the embedding vectors with? Would it influence the quality of the classification results? The goal of this project is to explore this question on a certain level. More often than not when someone conducts a machine learning task,
they will simply look at a state of the art model and tune it to their needs. However, in this case we will go deeper and check how the embedding itself and not just something like the learning rate influences the outcome.

Requirements: Python coding, knowledge of data analysis tools and models from Scikit-learn and PyTorch.



## 2. Project outline

1. Install openslide-python and familiarise yourself with its features and with its connection to other packages. Specifically, check its ability to patch a WSI. (The package has some basic WSIs that you can use.)
2. Explore your options for data acquisition. Download some whole slide images and explore their pyramid structure with openslide-python. Make sure to get slides with different tissues on them (liver, stomach, intestine, etc.) or multiple WSIs with differing tissue types. The latter might be the easier option as proper annotations are hard to come by. Find the optimal zoom level for the images in openslide. (Be creative!)
3. Create patches at the optimal zoom level. Use tiles that contain an agreeable amount of tissue data instead of blank space, while dropping all empty patches. Create a dataset that consist of patches of the different classes of tissue types. Choose 3 different patch sizes (like 256, 512, 1024, etc.) to monitor the amount of information gained. In the end you should have 3 separate dataclusters with each containing all the patches you generated at a given pixel size. Keep it simple and don't use overlapping patches! Try to keep the classes balanced! How many images you should create per class?
4. Choose three different embedding generators. Recommendations: one should be a ResNet model, one a Vision transformer (UNI), and choose any other from the list on this page under "Classification" https://pytorch.org/vision/main/models.html . Keep it simple and use ImageNet weights. Convert all patches into embeddings and organize them into a new dataset. Don't forget to keep track of the labels!
5. Start to compare the embeddings. First, use simple methods: compare their length, pair them up and compute things like the Euclidean distance, Cosine similarity, etc. (Be creative!) Then, create heatmaps from larger tissue spaces covered by embeddings and put them beside the same area on the WSI. Did we get back some structural information visually apart from just the edges? Do this for all 3 datasets (patch sizes) and put them next to each other.
6. Perform unsupervised learning methods on the embeddings. Use the following methods: Principal Component Analysis (PCA), Linear Discriminant Analysis (LDA), t-Disctributed Stochastic Neighbour Embedding (tSNE), Uniform Manifold Approximation and Projection (UMAP). Keep track of the classes visually by adjusting the color scheme and plot meaningful, easy to read figures. In the end, it is enough to display the one method that shows the most interesting behaviour across all 3 patch sizes.
7. Perform K-Means clustering on the embeddings. The task is the same as in the previous step with one exception. Stick to only one patch size. It should be the one that yielded the best results in the previous step.
8. Final task: checking the infulence the differing nature of the embeddings has on the efficiency of a supervised learning model. Keep it simple, fast and accurate with XGBoost Classifier. Build a classification framework around this model. For accuracy metrics, stick to basics: overall accuracy, AUROC, confusion matrix. Do 5-fold cross-validation. Use Stratified 5-Fold without shuffling to not only keep the classes balanced during splits but also make sure that you have the same indices in a fold across all 3 embedding types. (You might need to set the random_seed the same for all 3.) This means you need to run the cross-validation 1 time for all 3 embedding types, meaning 15 runs altogether. At the end of the cross-validations make a plot which contains the mean +/ std confusion matrix and the mean ROC curve. A boxplot can be useful from the results as well.
9. Draw your conclusions! Does it matter which embedding generator we use for the task at hand?


## 3. Pointers, useful links
- Option to download whole slide images: https://portal.gdc.cancer.gov/
- Alternative download source: https://www.cancerimagingarchive.net/collection/ovarian-bevacizumab-response/
- openslide-python documentation: https://openslide.org/api/python/
- Whole Slide Imaging in Pathology: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7522141/
- A useful tutorial for openslide-python: https://www.youtube.com/watch?v=QntLBvUZR5c
- A useful article on embeddings: https://arxiv.org/abs/2307.05610
- A few good blogposts about embeddings: https://zilliz.com/learn/image-embeddings-for-enhanced-image-search, https://medium.com/@uday.chitragar/understanding-embeddings-in-image-analysis-c87b795cef60
- UNI embedder: https://huggingface.co/MahmoodLab/UNI

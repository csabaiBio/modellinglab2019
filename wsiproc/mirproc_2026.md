# Cancer classification with sample selection performed on mid-infrared spectra collected from tissue samples with colorectal cancer

## 1. Short description

Colorectal cancer stands among the most prevalent cancer types in Hungary, and is a hot topic in medical analysis. Mid-infrared (MIR) spectroscopy provides biochemical information on the underlying tissue by displaying the intensity of molecular vibrations.
Our previous studies have already indicated that MIR spectroscopy could be used as an effective embedding tool that retains the ability to separate cancerous and non-cancerous tissue. One approach to proceed, is to give every tissue sample a label that denotes whether the sample contained cancerous or non-cancerous tissue.
This of course would mean that every single spectrum collected from a specific tissue sample is granted the same label. However, without complete knowledge of tissue sample inner structure, such as tumour boundaries, a global sample label would encompass spectra not possessing information relevant to the classification task.

![wsi_p.png](wsi_p.png)

While collecting spectra, a small area of a tissue sample is scanned by a microscope. The procedure results in a one-dimensional array with hundreds of data points. A data point signifies the percentage of IR transmittance through the sample at a specific wavelength.
The spatial position of the spectrum on the tissue sample is also retained, therefore the neighbouring spectra can be displayed together as a heatmap of the underlying tissue sample. 
In conclusion, MIR spectra are embeddings of an image containing biochemical information, where the image is a physical patch of the tissue sample and the embedding generator model is the microscope.
Machine learning models such as XGBoost can conveniently handle embeddigs as simple tabular data to perform classification. Using the previously described global labels, our results are far from perfect, therefore we need to examine the spectra locally.

The goal of this project is to deduce which spectra affects classification negatively and why? Could we reconstruct the inner structure of the tissue samples without pathologist approved annotations? What are these "negative" spectra?
Could it be that surrounding tumour boundaries within a tissue sample sits perfectly normal and non-cancerous tissue that was mislabelled as cancerous because of the global labels?



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

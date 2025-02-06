# Whole Slide Imaging for image generation

## 1. Short description

Whole Slide Imaging is one of the primary techniques that allows the creation of large pathological datasets. A whole slide image (WSI) usually contains a tissue sample that was prepared using various pathological staining and drying procedures. 
To view such an image there exists a good number of tools such as the softwares SlideViewer and QuPath which offer tools to for example, annotate on the slides. 
However, when it comes to performing analysis on a great amount of images extracted from WSIs, it is generally a better idea to utilise programming packages like openslide-python.

<picture>
<img src="https://github.com/borbende/Scientific-Modelling-Computer-lab/blob/main/wsi_p.png">
</picture>

The goal of this project is to explore the data analysis options offered by openslide-python and create a proper workflow which relies on the user's knowledge on the data structure and properties of WSIs, and provides a potential way to generate new data to be used from them.

## 2. Project outline


1. Install openslide-python and familiarise yourself with its features and with its connection to other packages.
2. Explore your options for data acquisition. Download some whole slide images and explore their pyramid structure with openslide-python. Slice up a WSI into smaller patches/tiles and compare the same images from different pyramid levels. (Find a WSI with at least 10 levels.) Use tiles that contain an agreeable amount of tissue data instead of blank space. You should use general image analysis tools in python. (Size, pixel distribution, similarity measures,...) How would the tiles coming from different levels differ in t-SNE or UMAP space?
3. Perform unsupervised image classification. (K-Means, PCA, hierarchical clustering, ...) For this task, you will arguably obtain more meaningful results if the WSI contains more than one type of tissue or has significantly differing tissue parts. From which pyramid level could you get the best results? Compare them for both efficiency and runtime.
4. Find some WSIs with H\&E staining and apply the function (https://www.youtube.com/watch?v=tNfcvgPKgyU&t=1006s) that separates the two staining types. Produce some meaningful visualisation to highlight the difference in the new images. Do a little research as to why you are seeing what you are seeing. Then, repeat the image classification task for both staining on the "best" pyramid level you determined during the last task. What changed? Are the results worse for both staining?
5. Organise everything you worked on into a proper workflow with descriptions, comments and a good outline.

## 3. Additional tasks

1. Find a way to rebuild the pyramid structure of a WSI from the many tiles you extracted from all levels.
2. Explore your options to store images as vectors in a database. Encoding images as vectors might require the use of neural networks.

## 4. Pointers

- Option to download whole slide images: https://portal.gdc.cancer.gov/
- Alternative download source: https://www.cancerimagingarchive.net/collection/ovarian-bevacizumab-response/
- openslide-python documentation: https://openslide.org/api/python/
- Whole Slide Imaging in Pathology: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7522141/
- A useful tutorial for openslide-python: https://www.youtube.com/watch?v=QntLBvUZR5c

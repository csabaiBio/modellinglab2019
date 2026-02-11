# Understanding the Scaling of Fractal Properties of Brain Tumors

### Objective:

The goal of this project is to establish whether certain scale-dependent fractal properties are useful predictors of WHO Grade in intracranial meningiomas. While fractal dimension and lacunarity are well-established biomarkers for brain tumors [1,2], analysis of their scale dependence is lacking. Lacunarity is often "summarized" by a single index value, yet the choice of measurement scale is seldom justified. This project investigates whether lacunarity measured at specific scales provides better diagnostic value than aggregate indices, and compares two distinct computational approaches for 3D medical imaging data.

## Background

## Fractal Properties in Medical Imaging

Fractal geometry provides quantitative tools to characterize the complexity and heterogeneity of tumor morphology:

- **Fractal Dimension (D)**: Measures how detail in a pattern changes with scale, quantifying self-similarity.
- **Lacunarity (λ)**: Describes texture heterogeneity and "gappiness" in spatial patterns.

[Crude illustration of box counting on a brain-tumor segmentation mask.](box_counting.mp4)

Crude illustration of box counting on a brain-tumor segmentation mask.

For a given box size $\epsilon$, lacunarity is defined as:

$$
\lambda(\epsilon) = \frac{Z^{(2)}}{[Z^{(1)}]^2}
$$

where $Z^{(1)}$ is the first moment and $Z^{(2)}$ is the second moment of the distribution of values within the boxes. Equivalently, lacunarity is the coefficient of variation of this distribution.

**Two Approaches to Lacunarity Calculation**

This project requires implementing and comparing two distinct methods for calculating lacunarity from 3D medical images:

1. **3D Method:**
    - Apply the tumor (segmentation) mask to the MRI sequence
    - Use 3D sliding windows of size $\epsilon$  to create the inter-window voxel value histogram
    - Calculate $\lambda(\epsilon)$  from that distribution.
2. **4D Method:**
    - Apply the tumor (segmentation) mask to the MRI sequence
    - Create a 4D version, where the 4-th dimension is given by the voxel intensity. Each voxel has coordinates $(x, y, z, I)$ where $I$ is intensity
    - Use 4D sliding windows of size $\epsilon$ and counts voxel occupancy

**Students must implement both methods and compare their predictive power for WHO grade classification.**


## Tasks

### Part 1:  Data Exploration & Visualization

1. Explore the data structure. Verify alignment between segmentation masks and MRI sequences.
2. Create visualizations:
    1. 3D renderings of sample tumors (use `matplotlib` or `plotly`)
    2. Axial/coronal/sagittal slice views
3. Explore the metadata CSV

**Deliverables**: Jupyter notebook with visualizations and summary statistics.

### Part 2: Implementing Scale-Dependent Lacunarity

1. Study the provided lacunarity calculation script. Understand how it:
    1. Performs box-counting
    2. Selects scales automatically
    3. Computes lacunarity values
2. Modify the script to accept a set of specific box sizes as input:
    1.  Add parameter for user-defined scale
    2. Ensure it works with 3D intensities (implement!) and 4D volumes (already works)
    3. Return $\lambda(\epsilon)$ for the specified scale
3. Implement visualization for the lacunarity curves as the function of the scale parameter!

**Deliverables**: Modified Python script with documentation and example usage.

### Part 3: Statistical Analysis

1. With both methods implemented, run them to obtain scale-dependent lacunarity values for each patient and each MRI sequence (except the segmentation mask.) You should examine the following scales:
[1 mm, 2mm, 5mm, 10mm]
*Smaller scales may reflect cellular-level heterogeneity, while larger scales capture tissue-level architecture patterns relevant to tumor grade. What did you get for the 1mm scale? (Hint: what is the voxel resolution?)*
Meaning, for each patient, you’ll have 4 x 4 x 2 = 32 lacunarity values.
2. Compare the two methods!
    
    For each combination of scale and MRI sequence, test (using permutation test) whether the 3D and 4D methods produce significantly different lacunarity values.” → A set of 16 p-values are expected as results. Explain what do they mean!
    
    Using permuation tests, can you differentiate between WHO Grade I and Grade II tumors using any of the lacunarity values? → A set of 16 p-values are expected as results. Explain what do they mean!
    
    For any lacunarity value that turns out to be significant, create box plots! (`seaborn.boxplot`)
    
3. Univariate Logistic Regressions
    
    Fit logistic regressions to predict WHO Grade for each significant lacunarity value. Calculate the usual classification metrics: accuracy, precision, recall, area under ROC, f1 score and confusion matrix. Use bootstrapping! (Randomly sample from your data with replacement, test - calculate metrics - on out-of-boot samples, the ones that you’ve never drawn in that given round. Average your metrics over at least 100 bootstrap resamplings.)
    
4. Multivariate Logistic Regression
    
    Choose the 3 best-performing lacunarity values from the univariate analysis! Provide reasoning on which metrics were preferred, and why.
    
    For each of them, fit multivariate logistic regression to predict WHO Grade with the clinical metadata! Calculate metrics! Use bootstrapping.
    
    Note: *You’ll want to do some feature engineering. Select an optimal feature set from the clinical metadata. Scale (numeric) and/or one-hot-encode (categorical) them. Also scale the lacunarity values. If you use z-score scaling, prove that the given value follows the normal distribution. (Otherwise, why would you use it?)*
    
5. Feature Importance Analysis
    
    Using the 3 fitted models, calculate regression coefficients and odds-ratios with 95% confidence intervals based off the bootstrapping distributions.
    
    - Which features have the highest odds-ratios?
    - Are there any feature, where OR ~ 1?

**Deliverables**: Jupyter notebook containing:

- Scale-dependent lacunarity values for all patients (saved as CSV or pickle)
- Permutation test results tables (method comparison + grade comparison)
- Box plots for significant lacunarity values
- Bootstrap validation results for univariate models (metrics with 95% CIs)
- Bootstrap validation results for multivariate models (metrics with 95% CIs)
- Odds ratio plots with confidence intervals
- Feature importance summary table

### Part 4: Final Report & Workflow

1. Organize all code into a documented, reproducible workflow:
    - Clear structure with numbered scripts or notebooks
    - Comments and docstrings explaining each function
    - README file with instructions to run the analysis

2. Write a comprehensive report addressing:

- Are scale-specific lacunarity values better predictors of WHO grade than aggregate indices?
- Which method (3D volume-based vs 4D intensity-based) performs better? Why might this be?
- Which spatial scales are most diagnostically relevant?
- Which scales show significant differences between grades?
- Support your claims with performance metrics with confidence intervals
- Discuss sample size, generalizability, and potential confounders
- How could this analysis be extended or improved?

**Deliverables**: Complete documented workflow + final report (3-5 pages).

### Optional Extensions

- Calculate and include fractal dimension as an additional feature
- Test alternative lacunarity indices (e.g., average, maximum, AUC under λ(ε) curve)
- Perform PCA on the 32 lacunarity values and use principal components as features

---

Citations

(1) Sánchez, J., & Martín-Landrove, M. (2022). Morphological and fractal properties of brain tumors. *Frontiers in Physiology*, *13*, 878391.

(2) Markia, B., Mezei, T., Báskay, J., Pollner, P., Mátyás, A., Simon, Á., ... & Erőss, L. (2025). Consistency and grade prediction of intracranial meningiomas based on fractal geometry analysis. *Neurosurgical Review*, *48*(1), 598.


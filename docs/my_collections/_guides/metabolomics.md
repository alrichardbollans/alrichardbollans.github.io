---
layout: page
title: Metabolomics Analyses
name: Metabolomics
snippet: A brief look at some analyses used for metabolomics. 
---

# Metabolomics Analyses
### Volcano Plots/Differential Analysis
This combines fold change and statistical significance (e.g., p-values from t-tests) to visualize and identify metabolites that exhibit both significant changes and substantial fold differences between species.

The significance levels should maybe be adjusted, for which Bonferroni correction (https://en.wikipedia.org/wiki/Bonferroni_correction) is often used (e.g. in https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2117-2, https://www.sciencedirect.com/science/article/pii/S0169743921000393). Bonferroni is conservative but simple correction method.

Examples:
- “Bioinformatic Insight into Portulaca Oleracea L. (Purslane) of Bulgarian and Greek Origin,” _Acta Biologica Cracoviensia s. Botanica_, 2020, [https://doi.org/10.24425/abcsb.2020.131662](https://doi.org/10.24425/abcsb.2020.131662).
- "Integrated metabolomics and transcriptome analysis on flavonoid biosynthesis in safflower (Carthamus tinctorius L.) under MeJA treatment" 2020
### Peaks
This involves comparing individual variables (peaks) across species using techniques like t-tests, ANOVA, or non-parametric equivalents. It helps identify specific metabolites that significantly differ among species. Again, p values should be corrected.

Examples:
- “Bioinformatic Insight into Portulaca Oleracea L. (Purslane) of Bulgarian and Greek Origin,” _Acta Biologica Cracoviensia s. Botanica_, 2020, [https://doi.org/10.24425/abcsb.2020.131662](https://doi.org/10.24425/abcsb.2020.131662).
### PCA
Methods like Principal Component Analysis (PCA), Partial Least Squares Discriminant Analysis (PLS-DA), can be used for (1) visualising clusters of the data and (2) analyzing if there is a statistical difference between species based on the components.

For visualisations, https://plotly.com/python/pca-visualization/ is nice.

For quantifying differences, can use MANOVA. Other analyses are possible.

Examples:
- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4523310/
### (Hierarchical) Clustering
Clustering algorithms (e.g., Hierarchical Clustering, k-means) can reveal patterns or clusters in the data, highlighting differences or similarities among species based on multiple variables simultaneously.

Examples:
- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).

### Machine Learning Classification
We can also set up a model to predict species/regions based on the LCMS data.

Examples:
- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).
### General Notes
#### Normalization
Careful preprocessing, including data normalization and transformation, is crucial to ensure accurate comparisons. Normalization methods like median scaling, log transformation, or autoscaling are commonly used in LC-MS data analysis. This has hopefully already been done by the lcms/compound discoverer packages.
##### Statistical Significance Correction
To control the error associated with multiple tests, carry out Holm-Bonferroni Correction (https://en.wikipedia.org/wiki/Holm%E2%80%93Bonferroni_method) or Hochberg Correction (https://academic.oup.com/biomet/article-abstract/75/4/800/423177) if the p values are independent --- usually for us they won't be independent as they relate to the same pairs of species or compounds. It is possible that Tukey's HSD is incorrectly used in (Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).) . These can both be carried out in a python script e.g. see https://www.statsmodels.org/dev/generated/statsmodels.stats.multitest.multipletests.html.


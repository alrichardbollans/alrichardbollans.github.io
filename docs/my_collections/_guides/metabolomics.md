---
layout: page
title: Metabolomics Analyses
name: Metabolomics
snippet: A brief look at some analyses used for metabolomics. 
---

### Differential Analysis

#### Volcano Plots

This combines fold change and statistical significance (e.g. p-values from ANOVA) to visualize and identify metabolites that exhibit both
significant changes and substantial fold differences between species.

Examples:

- “Bioinformatic Insight into Portulaca Oleracea L. (Purslane) of Bulgarian and Greek Origin,” _Acta Biologica Cracoviensia s. Botanica_,
  2020, [https://doi.org/10.24425/abcsb.2020.131662](https://doi.org/10.24425/abcsb.2020.131662).
- "Integrated metabolomics and transcriptome analysis on flavonoid biosynthesis in safflower (Carthamus tinctorius L.) under MeJA treatment" 2020

#### Peak Areas

This involves comparing individual variables (peaks) across species using techniques like t-tests, ANOVA, or non-parametric equivalents. It helps
identify specific metabolites that significantly differ among species.

Examples:

- “Bioinformatic Insight into Portulaca Oleracea L. (Purslane) of Bulgarian and Greek Origin,” Acta Biologica Cracoviensia s. Botanica_,
  2020, [https://doi.org/10.24425/abcsb.2020.131662](https://doi.org/10.24425/abcsb.2020.131662).

### PCA

Methods like Principal Component Analysis (PCA), Partial Least Squares Discriminant Analysis (PLS-DA), can be used for (1) visualising clusters of the
data and (2) analyzing if there is a statistical difference between species based on the components using multivariate tests e.g. MANOVA.

For visualisations, https://plotly.com/python/pca-visualization/ is nice.

Examples:

- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (
  April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).
- Aaron M. Goodpaster and Michael A. Kennedy, “Quantification and Statistical Significance Analysis of Group Separation in NMR-Based Metabonomics
  Studies,” Chemometrics and Intelligent Laboratory Systems 109, no. 2 (December 2011): 162–70, https://doi.org/10.1016/j.chemolab.2011.08.009.

### (Hierarchical) Clustering

Clustering algorithms (e.g., Hierarchical Clustering, k-means) can reveal patterns or clusters in the data, highlighting differences or similarities
among species based on multiple variables simultaneously.

Examples:

- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (
  April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).
- Shaurya Chanana et al., “Hcapca: Automated Hierarchical Clustering and Principal Component Analysis of Large Metabolomic Datasets in R,” Metabolites
  10, no. 7 (July 21, 2020): 297, https://doi.org/10.3390/metabo10070297.

### Machine Learning Classification

We can also set up a model to predict species/regions based on the LCMS data, doing this can support that metabolite data can be used to distinguish
the species.

Examples:

- Florence Souard et al., “Metabolomics Fingerprint of Coffee Species Determined by Untargeted-Profiling Study Using LC-HRMS,” _Food Chemistry_ 245 (
  April 2018): 603–12, [https://doi.org/10.1016/j.foodchem.2017.10.022](https://doi.org/10.1016/j.foodchem.2017.10.022).

### General Notes

#### Normalization

Careful preprocessing, including data normalization and transformation, is crucial to ensure accurate comparisons. Normalization methods like median
scaling, log transformation, or autoscaling are commonly used in LC-MS data analysis. This has hopefully already been done by the lcms/compound
discoverer packages.

#### Statistical Significance Correction

To control the error associated with multiple tests we need to a correction procedure. To control for
the [family-wise error rate](https://en.wikipedia.org/wiki/Family-wise_error_rate), there are a few common
methods. [Bonferroni correction](https://en.wikipedia.org/wiki/Bonferroni_correction) is often used (
e.g. [here](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2117-2)
and [here](https://www.sciencedirect.com/science/article/pii/S0169743921000393)), though this is a weak method. [Holm-Bonferroni
Correction](https://en.wikipedia.org/wiki/Holm%E2%80%93Bonferroni_method) is uniformly more powerful than the Bonferroni method, and [Hochberg
Correction](https://academic.oup.com/biomet/article-abstract/75/4/800/423177) is a still more powerful option if the p values are independent. Tukey's
HSD can be used when comparing means, and is used [here](https://doi.org/10.1016/j.foodchem.2017.10.022), as well as in Compound Discoverer. These can
be carried out in a python script e.g. see [statsmodels](https://www.statsmodels.org/dev/generated/statsmodels.stats.multitest.multipletests.html).

Some analyses use [False Discovery Rate](https://en.wikipedia.org/wiki/False_discovery_rate) correction, which are more powerful but less stringent
than correcting for family-wise error.

Compound Discoverer (v 3.1), does some adjustments by default. In the differential analysis, the p-value for the sample group is calculated by running
the Tukey HSD test (posthoc) after an analysis of variance (ANOVA) test. An 'adjusted' p value is also provided using the Benjamini-Hochberg
algorithm to account for the false discovery rate. Note that in the volcano plots the former is used.


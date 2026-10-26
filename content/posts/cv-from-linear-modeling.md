+++
date = '2026-10-26T00:00:00Z'
draft = false
title = 'CV from linear modeling'
+++

### Background

In the [last post](/posts/cv-for-paired-proteomics-samples) on CV calculation,
the final maximum likelihood statistic relied on an experiment having just 2 repeated samples for a patient.
This is not an unlikely situation by any means.
However, the calculation potentially makes it difficult to generalize to longitudinal experimental designs or those with more technical replicates.
As an alternative, the problem can be reformulated to derive the CV from a linear model of the experiment.

Let's say we have a set of $N$ log normal protein measurements $X_1,. . .,X_N$.
Each measurement $X_i$ came from a patient $P_i$ with average expression for this protein measurement $\gamma_{P_i}$.
The value measured for $X_i$ is then,

$$
\log(X_i) = \gamma_{P_i} + e_i
$$

The value $e_i$ is normally distributed with mean 0 and variance $\sigma^2$.
It is this $\sigma^2$ that is transformed into the CV of the log normal distribution as,

$$
CV = 100*\sqrt{\exp(\sigma^2) - 1}
$$

Fitting this linear model in Python and R is straight forward.
However, a gotcha is that the estimate of the residual variance has a special formula which needs to be specified for Python.
Once the predicted $\hat{X}_i$ values are calculated the estimate of residual variance is given by,

$$
s^2 = \frac{\sum_i{\left(X_i - \hat{X}_i\right)^2}}{N - P}
$$

The $P$ here is the number of patients and accounts for the degrees of freedom in the model.
After calculating $s^2$, the sample CV is given by the final equation.

$$
CV = 100*\sqrt{\exp(s^2) - 1}
$$

### CV on the Candia *et al.* dataset

As described in the [last post](/posts/cv-for-paired-proteomics-samples), the Candia *et al.* [1] dataset contains 102 samples with 2 technical replicates.
In that post, I used a maximum likelihood estimator for the CV but it was specific to the 2 technical replicate case.
The median CV there was determined to be 5.32%, a bit higher than the 4.25% calculated using the paper's technique.
Here, I applied the linear modeling approach using `SampleId` as the covariates.
This produced the distribution below which is unsurprisingly identical to the 2 rep maximum likelihood approach and has a median of 5.32%.

![Alt_text](https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_10_16_cv_through_linear_modeling/probe_cv_distribution_lm.svg)

- [Notebook location of original distribution](https://github.com/AnthonyOfSeattle/affinity-proteomics-notebook/blob/main/results/2026_09_09_investigating_candia_dispersion/probe_cv_distribution_mle.svg)
- [Notebook location of new distribution](https://github.com/AnthonyOfSeattle/affinity-proteomics-notebook/blob/main/results/2026_10_16_cv_through_linear_modeling/probe_cv_distribution_lm.svg)

### Conclusion

Going forward, this would likely be the calculation I would use even in the 2 replicate case.
One part of that is the generalizability, but it is also nice that the this version can incorporate other covariates.
This matches the analysis up more closely to things like variance component analysis.
At this point, however, I don't think using the method from Candia *et al.* would be correct in the long run.
Better to use methods with better theoretical garuntees of estimating the variance and CV.

---

* [1] Candia J, Daya GN, Tanaka T, Ferrucci L, and Walker KA (2022). Assessment of variability in the plasma 7k SomaScan proteomics assay. *Scientific Reports*, 12:17147. DOI: [10.1038/s41598-022-22116-0](https://doi.org/10.1038/s41598-022-22116-0)
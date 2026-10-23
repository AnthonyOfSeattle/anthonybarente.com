+++
date = '2026-10-23T00:00:00Z'
draft = false
title = 'CV from linear modeling'
+++

### Background

In the last post on CV calculation, the final maximum likelihood statistic relied on an experiment having just 2 repeated samples for a patient.
This is not an unlikely situation by any means.
However, the calculation potentially makes it difficult to generalize to longitudinal experimental designs or those with more technical replicates.
As an alternative, the problem can be reformulated to derive the CV from a linear model of the experiment.

Let's say we have a set of $N$ log normal protein measurements $X_1,. . .,X_N$.
Each measurement $X_i$ came from a patient $P_i$ with average expression for this protein measurement $\gamma_{P_i}$.
The value measured for $X_i$ is then,

$$
\log(X_i) = \gamma_{P_i} + e_i
$$

The value $e_i$ is normally distributed with mean 0 and variance $sigma^2$.
It is this $sigma^2$ that is transformed into the CV of the log normal distribution as,

$$
CV = 100*\sqrt{\exp(\sigma^2) - 1}
$$

Fitting this linear model in Python and R is straight forward.
However, a common gotcha is that the estimate of the residual variance has a special formula which needs to be specified for Python.
Once the predicted $\hat{X}_i$ values are calculated the estimate of residual variance is given by,

$$
s^2 = \frac{\sum_i{\left(X_i - \hat{X}_i\right)^2}}{N - P}
$$

The $P$ here is the number of patients and accounts for the degrees of freedom in the model.
After calculating $s^2$, the sample CV is given by the final equation.

$$
CV = 100*\sqrt{\exp(s^2) - 1}
$$

---

* [1] Candia J, Daya GN, Tanaka T, Ferrucci L, and Walker KA (2022). Assessment of variability in the plasma 7k SomaScan proteomics assay. *Scientific Reports*, 12:17147. DOI: [10.1038/s41598-022-22116-0](https://doi.org/10.1038/s41598-022-22116-0)
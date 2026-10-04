+++
date = '2026-09-28T00:00:00Z'
draft = false
title = 'CV for paired proteomics samples'
+++

### Background

Back in 2022, Candia *et al.* [1] put out a nice study in *Scientific Reports* diving deep into preprocessing SomaScan datasets.
Alongside their paper, they released a repository of anonymized raw and processed data with code for each step in their pipeline.
This is an invaluable resource to get a handle on working with SomaScan data and discussing QC.

One of the cool things about the design in this dataset is that there are multiple types of samples with different purposes.
In addition to 1704 experimental samples, the dataset contains pooled experiment "calibrator" samples and "qc" samples supplied by SomaLogic.
There is also a series of "buffer" samples which can be used to assess limits of detection.

![Alt_text](https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/example_plate_map.svg)

The calibrators were used extensively in the paper for data normalization, making them a bit suspect for calculating the coefficient of variation (CV).
So the authors used 102 experiment samples which had 2 technical replicates in the experiment to show reduction in CV with processing steps.
In this post, I will talk about how the authors calculated CV for these, why they used replicated samples, and a more straightforward alternative method for CV calculation.

### Classic CV calculation

The classic definition of CV is just
$$ \frac{s\_n}{\bar{x}\_n}$$
where $s\_n$ is that sample standard deviation and $\bar{x}\_n$ is the sample mean.
This works fine for things like the pooled calibrator samples but breaks down for true patient samples.
Patient samples are overdispersed, since measurements theoretically represent patient variation and the cumulative history of the sample since it was drawn.
The technical noise from the assay is only small portion of this variation.
Check out how dramatic the difference can be between the pooled and patient samples below. 

{{< rawhtml >}}
<div style="display: flex; gap: 1rem; justify-content: center; align-items: flex-start;">
  <img src="https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/probe_cv_by_plate_calibrators.svg" style="width: 50%;">
  <img src="https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/probe_cv_by_plate_samples.svg" style="width: 50%;">
</div>
{{< /rawhtml >}}

For the calibrator samples, median plate CVs range from 2.41% to 5.38%, which fits well within the expected CVs compiled by SomaLogic.
On the other hand, median plate CVs for patient samples range from 26.1% to 38.2%.

### CV on paired samples

#### The method used in Candia *et al.*

#### Straight forward CV calculation

---

* [1] Candia J, Daya GN, Tanaka T, Ferrucci L, and Walker KA (2022). Assessment of variability in the plasma 7k SomaScan proteomics assay. *Scientific Reports*, 12:17147. DOI: [10.1038/s41598-022-22116-0](https://doi.org/10.1038/s41598-022-22116-0)


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
<img src="https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/example_plate_map.svg">

The calibrators were used extensively in the paper for data normalization, making them a bit suspect for calculating the coefficient of variation (CV).
So the authors used 102 experiment samples which had 2 technical replicates in the experiment to show reduction in CV with processing steps.
In this post, I will talk about how the authors calculated CV for these, why they used replicated samples, and a more straightforward alternative method for CV calculation.

### Classic CV on calibrators

### Classic CV breakdown on clinical samples

### CV on paired samples

#### The method used in Candia *et al.*

#### Straight forward CV calculation

---

* [1] Candia J, Daya GN, Tanaka T, Ferrucci L, and Walker KA (2022). Assessment of variability in the plasma 7k SomaScan proteomics assay. *Scientific Reports*, 12:17147. DOI: [10.1038/s41598-022-22116-0](https://doi.org/10.1038/s41598-022-22116-0)


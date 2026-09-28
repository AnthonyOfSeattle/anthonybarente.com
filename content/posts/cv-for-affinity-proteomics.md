+++
date = '2026-09-28T00:00:00Z'
draft = false
title = 'CV for affinity proteomics'
+++

### Background

Back in 2022, Candia *et al.* [1] put out a nice study in *Scientific Reports* diving deep into preprocessing SomaScan datasets.
Alongside their paper, they released a repository of anonymized raw and processed data with code for each step in their pipeline.
This is an invaluable resource to get a handle on working with SomaScan data and discussing QC.
In this post, I will discuss the many ways to get a coefficient of variation (CV) from this data and my thoughts on pitfalls.

One of the cool things about the design in this dataset is that there are multiple types of samples with different purposes.
On the technical side, there are buffer samples which act as negative controls for detection as well as 2 sets of pooled samples.
The first set of pooled samples is denoted by QC below and these are provided by SomaLogic themselves.
The second set, labeled Calibrator, is a set of pooled samples directly from this experiment.
The authors use this Calibrator set extensively to normalize the data, and I will also look at the CV of these measurements below.

Finally, there are the true samples (1704 of them) in the data.
Within this set, there is a small subet of 102 which actually have 2 technical replicates falling on different plates.
A clever bit of math will give us a CV from this data as well.

![Alt_text](https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/example_plate_map.svg)
<img src="https://raw.githubusercontent.com/AnthonyOfSeattle/affinity-proteomics-notebook/refs/heads/main/results/2026_09_09_investigating_candia_dispersion/example_plate_map.svg">

### Classic CV on calibrators

### Classic CV breakdown on clinical samples

### CV on paired clinical samples

#### The method used in Candia *et al.*

#### Straight forward CV calculation

---

* [1] Candia J, Daya GN, Tanaka T, Ferrucci L, and Walker KA (2022). Assessment of variability in the plasma 7k SomaScan proteomics assay. *Scientific Reports*, 12:17147. DOI: [10.1038/s41598-022-22116-0](https://doi.org/10.1038/s41598-022-22116-0)


---
layout: page
title: Hawkes Processes for Earthquake Modelling
description: Comparing Poisson and Hawkes point process models on a USGS seismic catalogue
img: assets/img/hawkes.jpg
importance: 2
category: research
related_publications: false
---

Short empirical study comparing a homogeneous Poisson process with marked and unmarked exponential and power-law Hawkes processes on an earthquake catalogue from the [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/earthquakes/search/). The dataset contains 2961 events recorded over the United States between January 2025 and May 2026.

Models are fitted by maximum likelihood and evaluated via Ogata's time-rescaling theorem: under correct specification, the rescaled inter-arrival times should be i.i.d. Exp(1). KS and chi-squared tests on the residuals are used to assess absolute goodness of fit.

## What I did

- Implemented the **Hawkes process models** (exponential and power-law kernels, marked and unmarked), including the log-likelihood and its numerical maximisation via `scipy.minimize`.
- Applied **Ogata's time-rescaling theorem** for residual diagnostics, and ran KS and chi-squared tests against the Exp(1) reference.

## Main findings

The homogeneous Poisson model is strongly rejected (KS p < 10⁻²⁰), consistent with the pronounced temporal clustering visible in the raw inter-event times. Among Hawkes specifications, the marked exponential kernel provides the best fit (KS statistic 0.017, p ≈ 0.39; chi-squared p ≈ 0.07), while the power-law variants are also rejected. The positive magnitude coefficient (γ̂ = 1.12) confirms that larger earthquakes trigger more aftershock activity.

The analysis is purely temporal and ignores spatial structure, and the background rate is assumed constant — both acknowledged limitations in the report.

## Code

Available on [GitHub](https://github.com/FlorentinAcker/earthquakes).
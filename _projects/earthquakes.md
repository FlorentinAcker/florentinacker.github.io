---
layout: page
title: Hawkes Process Modelling of Seismic Activity
description: Comparing Poisson and Hawkes processes on a USGS earthquake catalogue
img: assets/img/hawkes.jpeg
importance: 2
category: research
related_publications: false
---

Course project at École Polytechnique (Statistical Modelling, supervised by M. Rosenbaum), based on a USGS seismic catalogue of 2,961 events recorded across the United States between January 2025 and May 2026.

We compared five point process models — from a homogeneous Poisson baseline to marked Hawkes processes — using maximum likelihood estimation and residual diagnostics based on Ogata's time-rescaling theorem.

## What we did

- Fitted a **homogeneous Poisson process** as a baseline, and verified empirically that inter-event times exhibit strong temporal clustering incompatible with a constant-rate model.
- Fitted four **Hawkes process** specifications: exponential and power-law kernels, each in marked and unmarked variants, via numerical MLE (`scipy.minimize`).
- Evaluated all models using **Ogata's time-rescaling theorem**: under correct specification, rescaled inter-arrival times should be i.i.d. Exp(1). We applied Kolmogorov–Smirnov and chi-squared tests on the transformed residuals.

## Main findings

The Poisson model and the power-law Hawkes processes are strongly rejected by both tests (p < 10⁻¹⁹). The unmarked exponential Hawkes performs reasonably well (KS statistic 0.022, p ≈ 0.12), but the **marked exponential Hawkes** provides the best fit overall (KS statistic 0.017, p ≈ 0.39; chi-squared p ≈ 0.07).

The estimated mark coefficient γ̂ = 1.12 confirms a positive dependence of the triggering intensity on earthquake magnitude, consistent with Omori-type aftershock behaviour. The marked model's rescaled residuals are nearly indistinguishable from the Exp(1) reference, both in CDF and density diagnostics.

## Limitations

The analysis is purely temporal and ignores the spatial distribution of events. A spatiotemporal Hawkes process would likely provide a more faithful description of seismicity. The background rate μ is also assumed constant throughout the observation window, which may not hold over long periods or across distinct seismic sequences.

## Code

Available on [GitHub](https://github.com/FlorentinAcker/hawkes_earthquakes).
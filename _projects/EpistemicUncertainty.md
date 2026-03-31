---
layout: page
title: Bayesian Deep Learning for Predictive Uncertainty
description: Benchmarking MC-Dropout and Deep Ensembles on toy regression and MNIST
img: assets/img/mnist.jepg
importance: 1
category: research
related_publications: false
---

Course project at École Polytechnique (with Lucas Jung, Hubert Leroux, and Al-Hakim Taoufik), based on a reimplementation and extension of [Gustafsson et al. (2020)](https://arxiv.org/abs/1906.02506).

We focused on two lightweight benchmarks — 1D sinusoid regression and MNIST classification — to keep experiments reproducible and interpretable within course compute constraints.

## What we did

- Reimplemented **Deep Ensembles** and **MC-Dropout** on both tasks, with HMC as a reference posterior on the regression benchmark.
- Added three extra uncertainty methods on regression: **test-time augmentation (TTA)**, **BN perturbation**, and **ensemble distillation**.
- Implemented a **Jacobian-based epistemic uncertainty proxy** (inspired by Zepf et al., 2023), which estimates output sensitivity to parameter perturbations without multiple forward passes.
- Ran a basic **targeted adversarial attack** on MNIST to stress-test the uncertainty decompositions.

## What I did

- Extended the experimental pipeline to **MNIST classification**: training loops, evaluation utilities, and uncertainty metrics (accuracy, NLL, ECE, reliability diagrams) for both Deep Ensembles and MC-Dropout.
- Designed and ran the **adversarial attack study**: implemented a targeted attack (surrogate CNN, cross-entropy descent under perturbation budget) and analyzed whether epistemic entropy can detect poisoned inputs.

## Main findings

On sinusoid regression, Deep Ensembles closely approximate the HMC posterior in-distribution (KL ≈ 0.19, NLL gap of 0.6 nats), while MC-Dropout is a coarser approximation (KL ≈ 0.59, NLL gap of ~2 nats). Both correctly recover the aleatoric/epistemic decomposition, with epistemic uncertainty growing outside the training interval. Ensemble distillation offered the best cost/quality trade-off among the additional methods.

On MNIST, both methods reach 99% accuracy and NLL of 0.030, improving over the deterministic CNN (NLL 0.050). ECE is slightly higher for the Bayesian methods (0.005 vs <0.001), consistent with mild over-spreading on a well-separated dataset.

The Jacobian epistemic scores correlate well with ensemble epistemic entropy (Spearman ρ = 0.84), suggesting both methods identify the same uncertain samples despite very different mechanisms.

Under adversarial attack, both MC-Dropout and Deep Ensembles remain overconfident: total entropy rises but is driven by aleatoric entropy, while the epistemic component stays low. The methods do not reliably flag adversarial inputs in this setting.

## Code

Available on [GitHub](https://github.com/FlorentinAcker/epistemic_uncertainty).
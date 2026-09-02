---
title: "Estimating Population Effects of an Innovation City on Its Host and Surrounding Areas Using Spatial Vertical Regression: A Case Study of Gyeongbuk Gimcheon Innovation City"
excerpt: "South Korea's Innovation City program relocated public institutions to provincial cities to counter over-concentration in the capital region, yet most host cities have missed their population targets amid concerns of a \"straw effect\" on surrounding areas. This study estimates the causal population impact of Gimcheon Innovation City on its host neighborhood and four concentric distance bands (5–20 km) over 1997–2024 using Spatial Vertical Regression (SVR), a Bayesian variant of the synthetic control method that models spatial dependence across adjacent treated units with Gaussian process priors. The host neighborhood's population surged from about 7,000 to over 29,000, while the legacy urban core within 5 km experienced a significant decline—consistent with hollowing-out—and the 15–20 km band saw significant growth. SVR outperformed OLS and Bayesian Vertical Regression, yielding lower prediction error and substantially narrower credible intervals under a short pre-treatment window."
collection: portfolio
date: 2025-12-01
header:
  teaser: /images/post_2013.png
tags:
  - Spatial Causal Inference
  - Synthetic Control Method
  - Bayesian Statistics
  - Demography
  - Regional Policy
---

## Overview

South Korea's Innovation City program relocated public institutions from the Seoul metropolitan area to provincial cities to counter regional population decline and over-concentration. Despite this effort, eight of ten Innovation Cities failed to meet their target populations as of 2021, and critics have pointed to a "straw effect" whereby new developments draw residents away from surrounding areas rather than attracting migrants from the capital region. This study takes Gimcheon Innovation City in North Gyeongsang Province as a case and empirically estimates the causal impact of its construction on both the host neighborhood (Yulgok-dong) and adjacent eup/myeon/dong units over the period 1997–2024, treating 2013—when public institution relocation began—as the intervention year.

## Methods

The primary method is **Spatial Vertical Regression (SVR)**, a variant of the Synthetic Control Method (SCM) proposed by Grossi et al. (2025) that explicitly models spatial dependence across multiple adjacent treated units via Bayesian priors—specifically, Gaussian process priors with a squared exponential kernel placed on both the coefficient vectors and the error terms.

- **Treatment group design**: Five mutually exclusive and collectively exhaustive (MECE) treated units—the core neighborhood (Yulgok-dong) plus four concentric distance bands at 5 / 10 / 15 / 20 km radii
- **Donor pool construction**: Units from 16 municipalities excluded from the six counties containing treated areas (to prevent interference), with representative eup/myeon/dong selected by pre-treatment population density percentile
- **Posterior inference**: Stan HMC (4 chains, 4,000 iterations, 2,000 warm-up); uncertainty reported as 95% credible intervals
- **Comparison models**: OLS, Bayesian Vertical Regression (BVR), and Event-Study Difference-in-Differences (DiD)
- **Data**: Resident registration population at the eup/myeon/dong level (Ministry of the Interior and Safety); administrative boundary changes (renaming, mergers, splits) resolved prior to analysis

## Results

- **Yulgok-dong (direct treatment)**: Population surged from roughly 7,000 to over 29,000 following the intervention (posterior median: +34.3σ), though the pace of growth slowed noticeably after 2020.
- **0–5 km band (legacy urban core)**: Statistically significant population decline (median: −2.24σ; 95% CI: −4.26, −0.61), consistent with hollowing-out of the traditional downtown as residents relocated to the new development.
- **10–15 km bands**: Credible intervals include zero, precluding firm conclusions, though a weak negative tendency is observed.
- **15–20 km band**: Significant population increase (median: +3.30σ; 95% CI: 1.42, 5.10), though confounding from the nearby Gumi National Industrial Complex Phase 4 cannot be ruled out.
- **Model comparison (MAE / RMSE / Mean CI Width)**: SVR outperforms both OLS and BVR on MAE and produces substantially narrower credible intervals, demonstrating that incorporating spatial structure improves estimation efficiency—particularly under a short pre-treatment window.

## Tools & Skills

- **Languages**: R (Stan / rstan, tidyverse, sf)
- **Methods**: Synthetic Control Method (SCM), Spatial Vertical Regression (SVR), Bayesian Vertical Regression (BVR), Event-Study DiD
- **Spatial Analysis**: Eup/myeon/dong-level GIS (concentric band design, population-density-based donor selection)
- **Data Wrangling**: Administrative boundary change reconciliation (renaming, mergers, splits) across 28 years
- **Visualization**: ggplot2
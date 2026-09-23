# Data-Science-Udacity
# What Gets Patients Home? Predicting Discharge Performance in U.S. Long-Term Care Hospitals

## Repository Description

This repository contains the full technical analysis behind the blog post 
*"Cleaner Hospitals vs. Better Rehab: What Actually Gets Patients Home?"* — 
a data-driven investigation into what separates high-performing long-term 
care hospitals (LTCHs) from low-performing ones in the United States.

## Project Overview

Using publicly available data from the **Centers for Medicare & Medicaid 
Services (CMS) LTCH Quality Reporting Program**, this project applies the 
**CRISP-DM framework** to analyse the discharge-to-community performance 
of 290 U.S. long-term care hospitals.

The central research question:
> *Which clinical and operational factors predict whether a hospital 
> discharges more — or fewer — patients successfully back to the community?*

## Methods & Technical Decisions

### Data Preparation
- Target variable: `discharge_to_community_performance` (Better / Average / Worse)
- Original feature set: 16 features including raw volume metrics 
  (catheter days, eligible cases, treatment episodes)
- **Volume features were removed** — they measure hospital size, 
  not clinical quality, and dominated feature importance in preliminary models
- Final feature set: 7 quality and rate features, all normalised for hospital size

### Models
Two classification models were trained and compared:

| Model | Feature Set | CV Balanced Accuracy |
| Logistic Regression | 16 features (original) | 0.566 |
| **Logistic Regression** | **7 features (quality only)** | **0.537** |
| Random Forest | 16 features (original) | 0.474 |
| Random Forest | 7 features (quality only) | 0.342 |

- **Class imbalance** (76.6% Average, 13.8% Worse, 9.7% Better) was addressed 
  using `class_weight="balanced"` and evaluated with **Balanced Accuracy**
- Random Forest collapsed to near-random performance after volume feature removal, 
  revealing it had been exploiting hospital size as a shortcut
- Logistic Regression remained robust, confirming it learned genuine quality signals

### Predictive Simulation
A hypothetical hospital (*"Midwest General LTCH"*) was created as a baseline 
— currently predicted as *Worse than the National Rate* — and two improvement 
strategies were simulated step by step:
1. **Mobility Score** gradually increased from 4.0 → 10.0 in 0.5 steps
2. **All SIR infection rates** proportionally reduced from 2.0 → 0.4


## Key Findings

- **Cost efficiency (MSPB Score) and mobility improvement** are the strongest 
  predictors of discharge performance — ranking #1 and #2 in feature importance
- **Infection control ranks last** — CLABSI, CAUTI, and MRSA SIR scores 
  show no meaningful separation between performance classes
- **Simulation confirms the finding:**
  - A mobility score improvement of just +0.5 points flipped the prediction 
    from *Worse* to *Average*
  - Reducing all infection rates to best-in-class levels produced 
    **zero prediction flips**

## Known Limitations

- Small dataset: only 290 hospitals, with 28 Better and 40 Worse examples
- Features are correlated — infection rates, readmission rates, and costs 
  influence each other in ways the model cannot fully disentangle
- The MSPB Score includes 30-day post-discharge costs, which may partially 
  reflect the outcome variable rather than predict it (potential data leakage)
- Simulations vary one feature at a time — real-world improvements 
  would likely affect multiple metrics simultaneously


## Data Source

Centers for Medicare & Medicaid Services (CMS)  
*Long-Term Care Hospital Quality Reporting Program*  
[https://data.cms.gov](https://data.cms.gov)  
Publicly available — no license restrictions.


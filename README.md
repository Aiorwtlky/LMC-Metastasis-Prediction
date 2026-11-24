# LMC-Based Lymph Node Metastasis Prediction and Survival Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb)

Reproducible machine learning and clinical survival stratification pipeline using latent methylation component (LMC) deconvolution proportions across **6 TCGA solid tumor cohorts** (`BLCA`, `BRCA`, `COAD`, `HNSC`, `LUAD`, `STAD`) and **2 LMC modeling frameworks** (12 evaluations total):

- **Individual Cancer LMC** (`cancer-specific_LMC`): Cohort-specific deconvolution components (top cohort: **COAD**, *n* = 194, LOOCV AUROC = 0.7209)
- **Pan-Cancer LMC** (`cross-cancer_LMC`): Shared cross-cancer deconvolution components (top cohort: **LUAD**, *n* = 194, LOOCV AUROC = 0.7105)

## Repository Structure

```text
LMC-Metastasis-Prediction/
├── LMC_Metastasis_Survival_EN.ipynb   # Main English notebook (all 12 cohort-model evaluations)
├── LMC_Metastasis_Survival_ZH.ipynb   # Traditional Chinese notebook
├── requirements.txt
└── data/                              # Minimal TSV inputs (~768 KB total)
    ├── sample_list.tsv                # Clinical N status & cohort annotations
    ├── cancer-specific_LMC/           # Cancer-specific LMC proportions (6 cohorts)
    ├── cross-cancer_LMC/              # Pan-cancer shared LMC proportions (6 cohorts)
    └── sample_survival/               # Overall survival time & censoring status (6 cohorts)
```

## Methodology Summary

1. **Nested Cross-Validation & LOOCV**: Within each of the 12 cohort-model pairs, feature standardization (`StandardScaler`) and L1 / Elastic Net penalized logistic regression (`class_weight="balanced"`) are tuned via inner 5×5 `RepeatedStratifiedKFold` (`roc_auc`), followed by outer Leave-One-Out Cross-Validation (LOOCV) to generate leakage-free patient risk scores.
2. **Statistical Evaluation**: Group discrimination (`N0` vs. `N+`) is assessed via ROC AUROC and two-sided Mann–Whitney *U* tests; clinical prognosis is evaluated via Kaplan–Meier log-rank tests (median 50% and extreme top vs. bottom 33% tertiles) and univariate Cox proportional hazards regression (reporting both raw `+1.0` probability-unit HRs and standardized `per 1-SD` HRs).

## Usage

### Option 1: Google Colab (One-Click Cloud Execution)
1. Click the **Open in Colab** badge above (or open `https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb`).
2. Select **Runtime → Run all**; the notebook automatically clones `./data` from GitHub, runs all 12 evaluations (~1–2 minutes), and renders the complete summary table and survival plots.

### Option 2: Local Jupyter / VS Code
```bash
git clone https://github.com/Aiorwtlky/LMC-Metastasis-Prediction.git
cd LMC-Metastasis-Prediction
pip install -r requirements.txt
jupyter notebook LMC_Metastasis_Survival_EN.ipynb
```

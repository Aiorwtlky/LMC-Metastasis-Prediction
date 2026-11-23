# LMC-Based Lymph Node Metastasis Prediction and Survival Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb)

Reproducible machine learning and clinical survival stratification pipeline using latent methylation component (LMC) deconvolution proportions across two representative TCGA cohorts:

- **COAD** (`cancer-specific_LMC`, Individual Cancer LMC model; *n* = 194: 96 N0, 98 N+; LOOCV AUROC = 0.7209)
- **LUAD** (`cross-cancer_LMC`, Pan-Cancer LMC model; *n* = 194: 97 N0, 97 N+; LOOCV AUROC = 0.7105)

## Repository Structure

Only the minimal data files required for the COAD and LUAD models are included:

```text
LMC-Metastasis-Prediction/
├── LMC_Metastasis_Survival_EN.ipynb   # Main English notebook
├── LMC_Metastasis_Survival_ZH.ipynb   # Traditional Chinese notebook
├── requirements.txt
└── data/
    ├── sample_list.tsv                # Clinical annotations (COAD & LUAD)
    ├── cancer-specific_LMC/
    │   └── COAD_proportion.tsv
    ├── cross-cancer_LMC/
    │   └── LUAD_proportion_array.tsv
    └── sample_survival/
        ├── COAD_survival.tsv
        └── LUAD_survival.tsv
```

## Methodology Summary

1. **Nested Cross-Validation & LOOCV**: Within each cohort, feature standardization (`StandardScaler`) and L1 / Elastic Net penalized logistic regression (`class_weight="balanced"`) are tuned via inner 5×5 `RepeatedStratifiedKFold` (`roc_auc`), followed by outer Leave-One-Out Cross-Validation (LOOCV) to obtain leakage-free patient risk scores.
2. **Statistical Evaluation**: Group discrimination is evaluated via ROC AUROC and two-sided Mann–Whitney *U* tests; clinical prognosis is assessed via Kaplan–Meier log-rank tests (median 50% and top vs. bottom 33% tertiles) and univariate Cox proportional hazards regression (reported for both unscaled `+1.0` probability units and standardized `per 1-SD` increments).

## Usage

### Option 1: Google Colab (One-Click Cloud Execution)
1. Click the **Open in Colab** badge above (or open `https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb`).
2. Select **Runtime → Run all**; the notebook automatically clones `./data` from GitHub and reproduces all metrics and plots.

### Option 2: Local Jupyter / VS Code
```bash
git clone https://github.com/Aiorwtlky/LMC-Metastasis-Prediction.git
cd LMC-Metastasis-Prediction
pip install -r requirements.txt
jupyter notebook LMC_Metastasis_Survival_EN.ipynb
```

# LMC-Based Lymph Node Metastasis Prediction and Survival Analysis

Reproducible machine learning and clinical survival stratification pipeline using latent methylation component (LMC) deconvolution proportions across two representative TCGA cohorts:

- **COAD** (`cancer-specific_LMC`, Individual Cancer LMC model; *n* = 194: 96 N0, 98 N+; LOOCV AUROC = 0.7209)
- **LUAD** (`cross-cancer_LMC`, Pan-Cancer LMC model; *n* = 194: 97 N0, 97 N+; LOOCV AUROC = 0.7105)

## Repository Structure

```text
LMC_Metastasis_Prediction/
├── LMC_Metastasis_Survival_EN.ipynb   # Main English notebook
├── LMC_Metastasis_Survival_ZH.ipynb   # Traditional Chinese notebook
├── requirements.txt
└── data/
    ├── sample_list.tsv
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
2. **Statistical Evaluation**: Group discrimination is evaluated via ROC AUROC and two-sided Mann–Whitney *U* tests; clinical prognosis is assessed via Kaplan–Meier log-rank tests (median 50% and top vs. bottom 33% tertiles) and univariate Cox proportional hazards regression (both unscaled `+1.0` probability units and standardized `per 1-SD` increments).

## Usage

### Google Colab
1. Open the notebook via Google Colab directly from GitHub:
   `https://colab.research.google.com/github/<YOUR_USERNAME>/<YOUR_REPO>/blob/main/LMC_Metastasis_Survival_EN.ipynb`
2. Set `GITHUB_REPO = "https://github.com/<YOUR_USERNAME>/<YOUR_REPO>.git"` in Cell 1 so Colab automatically clones `data/`, then select **Runtime → Run all**.

### Local Jupyter / VS Code
```bash
git clone https://github.com/<YOUR_USERNAME>/<YOUR_REPO>.git
cd <YOUR_REPO>
pip install -r requirements.txt
jupyter notebook LMC_Metastasis_Survival_EN.ipynb
```

# LMC Metastasis Prediction and Survival Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb)

Lymph node metastasis classification and overall survival analysis using latent methylation component (LMC) deconvolution proportions across six TCGA cohorts (`BLCA`, `BRCA`, `COAD`, `HNSC`, `LUAD`, `STAD`) under `Individual Cancer LMC` (`cancer-specific_LMC`) and `Pan-Cancer LMC` (`cross-cancer_LMC`) models.

## Files

```text
LMC-Metastasis-Prediction/
├── LMC_Metastasis_Survival_EN.ipynb
├── LMC_Metastasis_Survival_ZH.ipynb
├── requirements.txt
└── data/
    ├── sample_list.tsv
    ├── cancer-specific_LMC/
    ├── cross-cancer_LMC/
    └── sample_survival/
```

## Methods

1. **Classification**: `StandardScaler` with L1 / Elastic Net `LogisticRegression` (`class_weight="balanced"`), tuned via inner 5×5 `RepeatedStratifiedKFold` (`roc_auc`) and evaluated with outer Leave-One-Out Cross-Validation (LOOCV).
2. **Statistics**: ROC AUROC, two-sided Mann–Whitney *U* test, Kaplan–Meier log-rank test (median 50% and extreme top vs. bottom 33% tertiles), and univariate Cox proportional hazards regression (raw `+1.0` unit and standardized `per 1-SD`).

## Usage

### Google Colab
Open `https://colab.research.google.com/github/Aiorwtlky/LMC-Metastasis-Prediction/blob/main/LMC_Metastasis_Survival_EN.ipynb` and select **Runtime → Run all**.

### Local
```bash
git clone https://github.com/Aiorwtlky/LMC-Metastasis-Prediction.git
cd LMC-Metastasis-Prediction
pip install -r requirements.txt
jupyter notebook LMC_Metastasis_Survival_EN.ipynb
```

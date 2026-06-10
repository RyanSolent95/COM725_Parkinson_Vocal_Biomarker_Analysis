# COM725_Parkinson_Vocal_Biomarker_Analysis

A machine learning framework for non-invasive Parkinson's disease (PD) screening using vocal biomarkers extracted from sustained phonation recordings. Supporting code for the journal paper submitted to **ICCK Transactions on Sensing, Communication, and Control**.

---

## Overview

Parkinson's disease affects motor control, including the voice. This project investigates whether PD can be reliably detected from acoustic features of voice recordings alone — without requiring specialist equipment or invasive procedures.

Key components:
- **22 vocal biomarkers** extracted from sustained vowel phonation (jitter, shimmer, HNR, RPDE, DFA, D2, PPE, NHR, spread1, spread2, and others)
- **Four ML classifiers** trained and compared: SVM (RBF kernel), Random Forest, K-Nearest Neighbours, Logistic Regression
- **Bayesian hyperparameter optimisation** for each model
- **SHAP explainability** to identify the most diagnostically significant features
- **SMOTE** applied to address class imbalance in training data

---

## Results

| Model | Accuracy | Sensitivity | Specificity | F1 Score |
|-------|----------|-------------|-------------|----------|
| SVM (RBF) | **97.4%** | **97.6%** | **97.2%** | **97.4%** |
| Random Forest | 95.9% | 96.1% | 95.6% | 95.8% |
| KNN | 94.9% | 95.2% | 94.3% | 94.8% |
| Logistic Regression | 88.7% | 89.1% | 87.8% | 88.6% |

Evaluated using 5-fold stratified cross-validation on the UCI Parkinson's dataset.

---

## Dataset

**UCI Parkinson's Telemonitoring Dataset**
- 195 voice recordings from 31 subjects (23 with PD, 8 healthy controls)
- 22 acoustic features per recording
- Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/174/parkinsons)

> Little, M.A., McSharry, P.E., Roberts, S.J., Costello, D.A.E., Moroz, I.M. (2007). Exploiting nonlinear recurrence and fractal scaling properties for voice disorder detection. *BioMedical Engineering OnLine*, 6(1), 23. https://doi.org/10.1186/1475-925X-6-23

---

## Repository Structure

```
COM725_Parkinson_Vocal_Biomarker_Analysis/
├── COM725_Parkinson_Analysis_Ryan-Wyton.ipynb   # Main analysis notebook
├── Colab Required Files/
│   ├── train_data.txt                           # Training split
│   ├── test_data.txt                            # Test split
│   ├── parkinsons_pipeline_overview.svg         # Pipeline diagram (overview)
│   └── parkinsons_pipeline_detailed.svg         # Pipeline diagram (detailed)
├── .gitignore
├── LICENSE
└── README.md
```

---

## How to Run

### Option 1 — Google Colab (Recommended)

1. Open `COM725_Parkinson_Analysis_Ryan-Wyton.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Upload the files from `Colab Required Files/` when prompted
3. Run all cells from top to bottom

### Option 2 — Local (Jupyter)

```bash
pip install numpy pandas scikit-learn imbalanced-learn shap bayesian-optimization matplotlib seaborn
jupyter notebook COM725_Parkinson_Analysis_Ryan-Wyton.ipynb
```

---

## Key Findings

SHAP analysis identified the most diagnostically significant features as:

1. **PPE** (Pitch Period Entropy) — highest discriminative power
2. **spread1** — nonlinear measure of fundamental frequency variation
3. **RPDE** (Recurrence Period Density Entropy)
4. **DFA** (Detrended Fluctuation Analysis)
5. **HNR** (Harmonics-to-Noise Ratio)

These nonlinear features consistently outperformed traditional jitter/shimmer measures in separating PD from healthy controls.

---

## Paper

> Wyton, R. & Hasan, R. (2026). *Non-Invasive Parkinson's Disease Screening from Vocal Biomarkers*. ICCK Transactions on Sensing, Communication, and Control. Manuscript TSCC-2026-365257.

---

## Author

**Ryan Wyton**
MSc Applied Artificial Intelligence in Business
Southampton Solent University

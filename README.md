COM725_Parkinson_Vocal_Biomarker_Analysis
A subject-level machine learning framework for non-invasive Parkinson's disease (PD) screening from vocal biomarkers. Supporting code for the paper published in ICCK Transactions on Sensing, Communication, and Control (2026).

Overview
Parkinson's disease affects motor control, including the voice, and dopaminergic degeneration produces measurable vocal impairments before overt motor symptoms. This project investigates whether PD can be reliably screened from acoustic features of voice recordings alone, with a deliberate focus on two failures common in prior work: recording-level data leakage and model opacity.

Key components:

Subject-level partitioning via GroupKFold to eliminate recording-level data leakage (multiple recordings per subject never span train/test)
104 participant-level acoustic features derived by multi-statistic aggregation (mean, median, standard deviation, interquartile range) of per-recording measures
Bayesian hyperparameter optimisation with Optuna
Models compared: SVM (RBF kernel) - champion - plus Random Forest, XGBoost, Logistic Regression, and an ensemble stack (SVM + XGBoost + RF)
SHAP explainability to identify the most diagnostically significant features
A permutation test on the regression task (features → motor severity) that motivated the shift to binary classification
Results
Optimised SVM, subject-level GroupKFold cross-validation:

Metric	Value
Cross-validated accuracy	90.00%
Sensitivity	95.00%
Specificity	85.00%
Youden's J	0.80
Brier score	0.1049
Benchmark (baseline)	77.50%
External validation (held-out vowel-only cohort) sensitivity	85.71%
The optimised SVM improved on the 77.50% benchmark by 12.5 percentage points. A permutation test (p = 0.349) found no significant linear mapping between acoustic features and motor severity, motivating the binary screening formulation over regression.

Dataset
Parkinson's Speech Dataset with Multiple Types of Sound Recordings (Sakar et al., 2013), UCI Machine Learning Repository (dataset 301).

40 training subjects and 28 blind-test subjects
Multiple recording types per subject (sustained vowels, words, sentences)
Source: https://archive.ics.uci.edu/dataset/301/parkinson+speech+dataset+with+multiple+types+of+sound+recordings
Sakar, B. E., Isenkul, M. E., Sakar, C. O., Sertbas, A., Gurgen, F., Delil, S., ... & Kursun, O. (2013). Collection and analysis of a Parkinson speech dataset with multiple types of sound recordings. IEEE Journal of Biomedical and Health Informatics, 17(4), 828–834. https://doi.org/10.1109/JBHI.2013.2245674

Repository Structure
COM725_Parkinson_Vocal_Biomarker_Analysis/
├── COM725_Parkinson_Analysis_Ryan-Wyton.ipynb   # Main analysis notebook (four-phase framework)
├── Colab Required Files/
│   ├── train_data.txt                           # Sakar 2013 training subjects
│   ├── test_data.txt                            # Sakar 2013 blind-test subjects
│   ├── parkinsons_pipeline_overview.svg         # Pipeline diagram (overview)
│   └── parkinsons_pipeline_detailed.svg         # Pipeline diagram (detailed)
├── .gitignore
├── LICENSE
└── README.md
How to Run
Option 1 — Google Colab (recommended)
Open COM725_Parkinson_Analysis_Ryan-Wyton.ipynb in Google Colab
Upload the files from Colab Required Files/ when prompted
Run all cells from top to bottom
Option 2 — Local (Jupyter)
pip install numpy pandas scikit-learn xgboost optuna shap scipy matplotlib seaborn
jupyter notebook COM725_Parkinson_Analysis_Ryan-Wyton.ipynb
Key Findings
SHAP analysis identified the primary diagnostic drivers as:

Interquartile range of degree-of-voice-breaks
Shimmer amplitude variability
These aperiodic-phonation measures aligned with neuroacoustic evidence and outweighed conventional single-value jitter/shimmer summaries, underlining the value of the variance-sensitive, participant-level feature aggregation.

Paper
Wyton, R., & Hasan, R. (2026). Non-Invasive Parkinson's Disease Screening from Vocal Biomarkers: A Subject-Level Machine Learning Framework with Bayesian Optimisation and Explainable AI. ICCK Transactions on Sensing, Communication, and Control, 3(3), 197–209. https://doi.org/10.62762/TSCC.2026.365257

The analysis code, feature-engineering pipeline, and supporting data files in this repository are the resources referenced in the paper's Data Availability Statement.

Author
Ryan Wyton, MSc Applied AI & Data Science, Southampton Solent University

License
Released under the MIT License. See LICENSE.

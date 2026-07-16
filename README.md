# Parkinson's Disease Detection

Machine learning project for detecting Parkinson's disease from biomedical voice measurements.

## Overview

This repository contains a dataset and analysis pipeline for classifying whether a subject has Parkinson's disease based on a set of biomedical voice measurements. The dataset consists of voice recordings taken from multiple subjects, with several sustained phonations recorded per individual. Each row represents one voice recording, and the associated features capture various acoustic properties known to be affected by Parkinson's disease, such as frequency variation, amplitude variation, and signal noise characteristics.

## Dataset

**File:** `Parkinsson_disease.csv`

- **Rows:** 195 voice recordings
- **Subjects:** 31 individuals (23 with Parkinson's disease, 8 healthy controls), each contributing multiple recordings
- **Features:** 22 numeric acoustic measurements, plus a `name` identifier and a binary `status` label

### Column Description

| Column | Description |
|---|---|
| `name` | Subject identifier and recording number |
| `MDVP:Fo(Hz)` | Average vocal fundamental frequency |
| `MDVP:Fhi(Hz)` | Maximum vocal fundamental frequency |
| `MDVP:Flo(Hz)` | Minimum vocal fundamental frequency |
| `MDVP:Jitter(%)`, `MDVP:Jitter(Abs)`, `MDVP:RAP`, `MDVP:PPQ`, `Jitter:DDP` | Measures of variation in fundamental frequency |
| `MDVP:Shimmer`, `MDVP:Shimmer(dB)`, `Shimmer:APQ3`, `Shimmer:APQ5`, `MDVP:APQ`, `Shimmer:DDA` | Measures of variation in amplitude |
| `NHR`, `HNR` | Ratio of noise to tonal components in the voice |
| `status` | Health status of the subject (1 = Parkinson's, 0 = healthy) |
| `RPDE`, `D2` | Nonlinear dynamical complexity measures |
| `DFA` | Signal fractal scaling exponent |
| `spread1`, `spread2`, `PPE` | Nonlinear measures of fundamental frequency variation |

### Target Variable

`status`: `1` indicates the subject has Parkinson's disease, `0` indicates a healthy subject.

## Objective

The goal of this project is to build and evaluate classification models that can accurately distinguish between individuals with Parkinson's disease and healthy individuals using only voice measurement features. This has practical relevance for non-invasive, low-cost screening tools that could support early detection.

## Project Structure

```
.
├── Parkinsson_disease.csv     # Raw dataset
├── notebooks/                 # Exploratory data analysis and modeling notebooks
├── src/                       # Source code for preprocessing, training, and evaluation
├── models/                    # Saved trained models
├── requirements.txt           # Python dependencies
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.8 or higher
- pip

### Installation

```bash
git clone https://github.com/<your-username>/parkinsons-disease-detection.git
cd parkinsons-disease-detection
pip install -r requirements.txt
```

### Usage

Load the dataset and run the analysis or training script:

```python
import pandas as pd

df = pd.read_csv("Parkinsson_disease.csv")
X = df.drop(columns=["name", "status"])
y = df["status"]
```

Refer to the scripts in `src/` or the notebooks in `notebooks/` for full preprocessing, model training, and evaluation workflows.

## Methodology

A typical workflow for this dataset includes:

1. **Data cleaning and exploration** — checking for missing values, class imbalance, and feature distributions.
2. **Feature scaling** — normalizing or standardizing the acoustic measurements, which vary widely in scale.
3. **Train/test split** — with attention to grouping by subject, since multiple recordings per subject can otherwise leak information between training and test sets.
4. **Model training** — using classification algorithms such as logistic regression, support vector machines, random forests, or gradient boosting.
5. **Evaluation** — using metrics appropriate for an imbalanced dataset, such as precision, recall, F1-score, and ROC-AUC, rather than accuracy alone.

## Notes on Class Imbalance

The dataset is imbalanced, with roughly 75 percent of recordings belonging to subjects with Parkinson's disease. This should be accounted for during model evaluation and, where appropriate, addressed through techniques such as class weighting or resampling.

## Dataset Source

This dataset is based on the Parkinson's Disease Data Set originally created by Max Little of the University of Oxford, in collaboration with the National Centre for Voice and Speech, Denver, Colorado, and distributed via the UCI Machine Learning Repository.

## License

Specify the license for this repository here (for example, MIT License).

## Disclaimer

This project is intended for educational and research purposes only. It is not a diagnostic tool and should not be used as a substitute for professional medical advice or diagnosis.

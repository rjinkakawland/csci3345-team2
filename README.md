# Evaluating SMS Spam Classifiers Under Distribution Shift: Robustness and Adaptation

**CSCI 3345: Machine Learning | Fall 2026 | Boston College**

**Team 2:** Jacelyn Tay, Rou Jing Chan, Vansh Puri

## Project Overview

This project investigates the robustness of SMS spam classifiers under cross-corpus distribution shift. We examine whether classifiers trained on historical SMS messages can generalize to non-overlapping messages from a second dataset, and whether alternative classifiers, feature representations, and limited-data adaptation improve performance.

## Datasets

We use the following publicly available datasets:

1. **UCI SMS Spam Collection:** [Download](https://archive.ics.uci.edu/dataset/228/sms+spam+collection)
   - 5,574 original messages
   - Binary labels: ham and spam
   - Used for training, validation, and in-domain testing

2. **Mendeley SMS Phishing Dataset:** [Download](https://data.mendeley.com/datasets/f45bkkt8pr/1)
   - 5,971 original messages
   - Labels: ham, spam, and smishing
   - Used for cross-corpus evaluation and limited-data adaptation

After normalizing text for duplicate detection, removing duplicates, and excluding cross-dataset overlap, 5,159 UCI messages and 945 Mendeley messages remain.

The datasets are not included in this repository. Download them from the links above.

## Baseline Checkpoint

The baseline uses L2-regularized logistic regression with binary bag-of-words features.

We compare it against a majority-class classifier and a preliminary decision tree classifier.

**Data splitting:**
- UCI: 70% training, 15% validation, 15% test
- Mendeley: 50% adaptation, 50% held-out test
- Random seed: 3345

The test sets are reserved for final evaluation.

### Initial Results

Performance on the UCI validation set:

| Model | AP | Precision | Recall | F1 | FPR |
|---|---|---|---|---|---|
| Majority Class | 0.1240 | 0.0000 | 0.0000 | 0.0000 | 0.0000 |
| Logistic Regression | 0.9611 | 0.9882 | 0.8750 | 0.9282 | 0.0015 |
| Decision Tree | 0.7649 | 0.8778 | 0.8229 | 0.8495 | 0.0162 |

Logistic regression achieves the highest validation performance among the preliminary configurations tested.

## Reproducing the Results

The experiments are implemented in Python using NumPy, pandas, matplotlib, and scikit-learn.

1. Install the dependencies listed in `requirements.txt`.
2. Download the UCI and Mendeley datasets using the links above.
3. Extract `SMSSpamCollection` and `Dataset_5971.csv`.
4. Open `Team2_BaselineCheckpoint.ipynb` in Google Colab or Jupyter Notebook.
5. Place both dataset files in the notebook's working directory. In Colab, upload them using the Files sidebar.
6. Run all notebook cells in order.

The notebook contains data preprocessing, model training, evaluation, error analysis, and reproducibility checks.

## Planned Experiments

1. **Classifier Comparison:** Logistic regression, k-nearest neighbors, and decision trees.
2. **Feature Comparison:** Binary bag-of-words, word-level TF-IDF, and character n-grams.
3. **Limited-Data Adaptation:** Incorporating labelled examples from the Mendeley adaptation pool.

## Team Responsibilities

- **Jacelyn Tay:** Data preparation and feature comparison
- **Rou Jing Chan:** Baseline implementation and classifier comparison
- **Vansh Puri:** Limited-data adaptation and final evaluation

All team members contribute to the report and presentation.

## Limitations

The original datasets contain substantial overlap. After duplicate and overlap removal, only 945 Mendeley messages remain.

The cleaned datasets also differ in class distribution. Publication dates do not necessarily correspond to message collection dates, so cross-corpus evaluation should not be interpreted as a strictly temporal evaluation.

# Predicting Breast Cancer Relapse Using Gene Expression and Machine Learning

This project uses gene expression data and machine learning to predict **breast cancer relapse** and identify potential **relapse-associated biomarkers**.

We work with the **GSE2034** breast cancer dataset, which contains microarray gene expression profiles and relapse information for **286 patients**. Each sample has ~22,000 gene features.

The project is implemented in Python with a **clean OOP pipeline** for data loading and preprocessing, and multiple ML models for prediction and interpretation.

---

## Project Goals

1. **Predict relapse vs non-relapse** using gene expression:
   - Class 0: Non-relapse  
   - Class 1: Relapse  

2. **Identify genes associated with relapse risk** using:
   - Logistic Regression coefficients  
   - Random Forest feature importances  

3. **Compare multiple machine learning models**:
   - Logistic Regression  
   - Random Forest  
   - SVM (RBF kernel)  
   - Linear SVM (`LinearSVC`)  

4. **Visualize model performance and biological patterns**:
   - Class distribution
   - Confusion matrices
   - ROC curves
   - Top predictive genes

5. **Use an OOP design** for reproducibility and clarity.

---

## Dataset

- **Name:** GSE2034 (breast cancer gene expression)
- **Format used in this project:** `GSE2034_series_matrix.txt`
- **Size:**
  - ~286 patients
  - ~22,000 genes (probes)
- **Target label:** “bone relapses (1=yes, 0=no)” extracted from `!Sample_characteristics_ch1` metadata lines.

After preprocessing, the class distribution is:

- **Non-relapse (0):** 217 patients  
- **Relapse (1):** 69 patients  

This strong class imbalance is central to the analysis and interpretation.

> ⚠️ You must download `GSE2034_series_matrix.txt` (GEO Series Matrix file) and place it in the project directory, or update the `DATA_PATH` variable to point to its location.

---

## Methods & Design

### 1. OOP Pipeline: `GSE2034Pipeline`

The core of the preprocessing is encapsulated in a single class:

```python
class GSE2034Pipeline:
    """Pipeline for loading, preprocessing, and splitting GSE2034."""

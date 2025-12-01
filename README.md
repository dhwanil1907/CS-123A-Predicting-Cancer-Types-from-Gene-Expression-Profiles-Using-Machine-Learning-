# Predicting Breast Cancer Relapse Using Gene Expression and Machine Learning

This project uses gene expression data and machine learning to predict
**breast cancer relapse** and identify potential relapse-associated gene
biomarkers. Using the **GSE2034** dataset, we evaluate multiple models
and analyze their ability to detect relapse in an imbalanced biomedical
dataset.

The workflow is fully reproducible and built around a clean **OOP
preprocessing pipeline**.

------------------------------------------------------------------------

## 📁 Dataset Overview

-   **Dataset:** GSE2034 breast cancer gene expression (GEO)
-   **Samples:** 286 patients
-   **Genes:** \~22,000 (Affymetrix probe IDs)
-   **Target:** `"bone relapses (1=yes, 0=no)"`

Class distribution:

-   **Non-Relapse:** 217\
-   **Relapse:** 69

The imbalance is critical and heavily influences model performance.

You must download the dataset from GEO as:

    GSE2034_series_matrix.txt

Place it in your project directory or update `DATA_PATH` accordingly.

------------------------------------------------------------------------

## 🚀 Project Goals

1.  Predict relapse vs non-relapse from gene expression data\
2.  Train and compare four machine learning models:
    -   Logistic Regression\
    -   Random Forest\
    -   SVM (RBF)\
    -   Linear SVM (LinearSVC)\
3.  Identify biologically meaningful genes using:
    -   Logistic Regression coefficients\
    -   Random Forest importances\
4.  Visualize:
    -   Class imbalance\
    -   Confusion matrices\
    -   ROC curves\
    -   Top predictive genes\
5.  Use a clean and modular **object-oriented pipeline** for
    reproducibility

------------------------------------------------------------------------

## 🧱 Code Architecture

### **GSE2034Pipeline Class**

A modular pipeline that handles:

-   Loading GEO series matrix files\
-   Removing metadata/annotation lines\
-   Constructing the gene expression matrix\
-   Parsing metadata into a clean table\
-   Identifying the relapse target column\
-   Variance filtering\
-   Train/test splitting\
-   Standard Scaling

This class **does NOT** train models or make plots.\
Its goal is preprocessing only.

Usage:

``` python
pipe = GSE2034Pipeline("GSE2034_series_matrix.txt")

(
    X_train, X_test,
    y_train, y_test,
    X_train_scaled, X_test_scaled
) = pipe.run()
```

------------------------------------------------------------------------

## 📊 Modeling & Evaluation

We evaluate four models:

### **1. Logistic Regression**

-   Best recall for relapse\
-   F1 ≈ 0.57\
-   AUC ≈ 0.70\
-   Clinically meaningful because it detects relapse

### **2. Random Forest**

-   High accuracy (≈0.76)\
-   **Fails completely to detect relapse (F1 = 0)**\
-   Misled by class imbalance

### **3. SVM (RBF Kernel)**

-   Also fails to detect relapse despite strong accuracy\
-   Demonstrates limitations of nonlinear SVMs on imbalanced biomedical
    datasets

### **4. Linear SVM (LinearSVC)**

-   Comparable to Logistic Regression\
-   F1 ≈ 0.57\
-   Recall ≈ 0.86\
-   AUC ≈ 0.70

### 📌 Key Lesson

**High accuracy DOES NOT mean a good model** in imbalanced datasets.\
Recall, F1-score, and class-specific confusion matrices are essential.

------------------------------------------------------------------------

## 🔬 Gene Importance & Biomarker Discovery

### Logistic Regression

-   Coefficients indicate:
    -   Positive → more relapse-associated\
    -   Negative → protective

### Random Forest

-   Feature importances highlight nonlinear gene contributions

### Overlapping Genes (Top 100 LR ∩ Top 100 RF)

    203218_at
    218787_x_at
    222077_s_at
    209380_s_at
    219756_s_at

These cross-model genes are strong biomarker candidates because they
appear in the top rankings of two very different ML methods.

------------------------------------------------------------------------

## 📈 Visualizations

The project produces:

-   Class distribution bar plot\
-   Confusion matrices for all models\
-   ROC curves with AUC\
-   Top 20 genes (LR coefficients & RF importances)\
-   Pipeline workflow diagram (Graphviz)

------------------------------------------------------------------------

## 🛠️ Installation

### 1. Clone the repository

``` bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2. (Optional but recommended) Create a virtual environment

``` bash
python -m venv .venv
source .venv/bin/activate    # macOS/Linux
# OR
.\.venv\Scriptsctivate     # Windows
```

### 3. Install dependencies

``` bash
pip install -r requirements.txt
```

### 4. Ensure Graphviz is installed on your system

On macOS:

``` bash
brew install graphviz
```

On Ubuntu:

``` bash
sudo apt-get install graphviz
```

Windows installers: https://graphviz.org/download/

------------------------------------------------------------------------

## ▶️ Running the Project

### Option A --- Jupyter Notebook

``` bash
jupyter notebook
```

Open your `.ipynb` file and run all cells in order.

### Option B --- Python Script

``` bash
python main.py
```

------------------------------------------------------------------------

## 📌 Limitations

-   Small dataset (286 samples)
-   High feature dimensionality (\~22k genes)
-   Severe class imbalance
-   No external validation cohort
-   Microarray data may contain batch effects

------------------------------------------------------------------------

## 🧾 Conclusion

This project demonstrates how machine learning and gene expression data
can predict breast cancer relapse. **Logistic Regression and LinearSVC**
provide the best clinical performance, while Random Forest and SVM
struggle with class imbalance.

Cross-model gene importance analysis highlights robust candidate
biomarkers that may play a role in relapse biology.

The project showcases: - Clean OOP pipeline design\
- Rigorous model evaluation\
- Biological interpretability\
- Machine learning workflow best practices

------------------------------------------------------------------------

## 📄 License

Specify your license here.

------------------------------------------------------------------------

## 🙏 Acknowledgements

-   GSE2034 microarray dataset\
-   scikit-learn, matplotlib, seaborn, numpy, pandas\
-   Graphviz for workflow visualization

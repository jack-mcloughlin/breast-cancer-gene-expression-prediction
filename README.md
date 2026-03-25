# Breast Cancer Gene Expression Response Prediction

## Overview
Predicting treatment response in breast cancer is difficult due to high-dimensional genomic data and small patient cohorts. This project explores whether a subset of 10 key genes can reliably predict patient outcomes using regularized logistic regression.

## Dataset
- Source: [Breast Cancer Gene Expression Dataset](https://huggingface.co/datasets/mubashir1837/Breast-Cancer-Gen-Expression-Dataset)
- 51 patient samples with gene expression features and response labels.

## Approach
1. **Data Cleaning & Preprocessing**
   - Selected numeric features and imputed missing values.
2. **Exploratory Data Analysis (EDA)**
   - Plotted response distribution, correlation heatmaps, and gene expression trends.
3. **Feature Selection**
   - Variance threshold to remove low-variance genes.
   - ANOVA F-score (`SelectKBest`) to select top 10 genes most associated with response.
4. **Modeling**
   - Logistic Regression with L2 regularization (`liblinear` solver) for classification.
   - Train-test split with scaling.
5. **Evaluation**
   - Test accuracy, confusion matrix, classification report.
   - 5-Fold stratified cross-validation for robust performance.
6. **Interpretation**
   - Top genes identified and coefficients visualized for insight into biological relevance.

## Results
- **Top 10 genes** most predictive of treatment response were identified using ANOVA F-score. These genes were: ABCA7, ALDH16A1, CDCA8, H2AC11, H2BC11, H2BC12, LRRC37A4P, PAQR6, SOX15 and TMNT2.
- **Test accuracy:** Logistic regression achieved ~91% test accuracy.
- **Cross-validation accuracy:** ~58% (reflects small sample size and need for robust evaluation).

## Key Insights
Using predictive modeling, potential biomarkers can be highlighted but small sample sizes mean that careful feature selection and regularization is necessary. The logistic regression coefficients give key insights into which genes can contribute to treatment responses. 

## Limitations
The divergence between test accuracy and cross-validation performance suggests high sensitivity to the train-test split, likely due to the small N=51 sample size. This highlights the risk of overfitting in high-dimensional biological data.

## Next Steps
- Expand to larger datasets for more robust models.  
- Explore other classifiers like RandomForest or XGBoost.  
- Conduct pathway analysis to link top genes to biological mechanisms.

## Notebook
The full analysis is in the `Breast_Cancer_Gene_Expression_Prediction.ipynb` notebook.

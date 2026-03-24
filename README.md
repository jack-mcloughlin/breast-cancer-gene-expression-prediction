# Breast Cancer Gene Expression Response Prediction

## Overview
This project uses gene expression data to predict patient response to treatment. It demonstrates a complete data analysis workflow including feature selection, model building, evaluation, and interpretation - useful for bioinformatics and precision medicine applications.

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
- **Top 10 genes** identified as predictive.
- **Test accuracy:** ~91%.
- **Cross-validation accuracy:** ~58% (reflects small sample size and need for robust evaluation).

## Key Insights
- Predictive modeling can highlight potential biomarkers.
- Small sample sizes require careful feature selection and regularization.
- Logistic regression coefficients provide interpretable insights into gene contributions.

## Requirements
- Python 3.x  
- pandas, numpy, matplotlib, seaborn  
- scikit-learn

## Next Steps
- Expand to larger datasets for more robust models.  
- Explore other classifiers like RandomForest or XGBoost.  
- Conduct pathway analysis to link top genes to biological mechanisms.

## Notebook
The full analysis is in the `Breast_Cancer_Gene_Expression_Prediction.ipynb` notebook.

# Breast Cancer Gene Expression Analysis & Treatment Response Classification

## Overview

This project explores the relationship between gene-expression patterns and treatment response in breast cancer patients using statistical analysis and machine learning.

The objective was to identify genes exhibiting differences in expression between treatment responders and non-responders and investigate whether these features could help distinguish between the two groups using logistic regression.

The project demonstrates high-dimensional data preprocessing, statistical feature selection, binary classification, model evaluation, and interpretation of gene-level associations using Python.

## Dataset

- **Source:** [Breast Cancer Gene Expression Dataset](https://huggingface.co/datasets/mubashir1837/Breast-Cancer-Gen-Expression-Dataset)
- **Patient samples:** 51
- **Gene-expression features:** 28,278 before preprocessing
- **Target variable:** `Response` (binary classification: 0 or 1)

The dataset contains substantially more gene-expression features than patient observations, presenting a high-dimensional modeling challenge.

## Methodology

### 1. Data Preparation

- Loaded gene-expression data using Pandas.
- Separated the binary treatment-response variable from gene-expression predictors.
- Removed sample identifiers from the predictor dataset.
- Applied median imputation for missing values.
- Used variance threshold filtering to remove low-variance features.

### 2. Exploratory Data Analysis

- Examined the distribution of treatment-response outcomes.
- Investigated variation across gene-expression features.
- Visualized expression distributions for selected genes.
- Examined the relationship between gene expression and treatment-response classification.

### 3. Statistical Feature Selection

Applied ANOVA F-score feature selection (`SelectKBest` with `f_classif`) to identify the 10 genes exhibiting the strongest differences in expression between treatment-response groups.

The ANOVA F-statistic measures between-group variation relative to within-group variation.

The top 10 genes identified using the full dataset were:

| Gene | ANOVA F-Score |
|---|---:|
| H2AC11 | 18.86 |
| H2BC12 | 17.47 |
| TNNT2 | 16.63 |
| CDCA8 | 16.36 |
| LRRC37A4P | 15.76 |
| SOX15 | 15.33 |
| ABCA7 | 15.08 |
| PAQR6 | 14.93 |
| H2BC11 | 14.43 |
| ALDH16A1 | 13.97 |

These genes exhibited the strongest univariate differences in expression between the two response groups in the full dataset.

### 4. Logistic Regression Modeling

Developed a binary classification model using L2-regularized logistic regression.

- Standardized selected gene-expression features.
- Applied L2 regularization to help control model complexity and reduce overfitting.
- Examined regression coefficients to understand the direction of each gene's modeled association with treatment response.

Positive coefficients indicate higher modeled odds of `Response = 1`, while negative coefficients indicate lower modeled odds, holding the other selected genes constant.

### 5. Model Evaluation

Evaluated predictive performance using repeated stratified 5-fold cross-validation, with 10 repetitions.

Preprocessing, variance filtering, ANOVA feature selection, and standardization were incorporated into a Scikit-learn pipeline. These steps were independently fitted within each training fold to prevent information leakage into validation samples.

**Cross-validation results:**

| Evaluation Metric | Mean Score | Standard Deviation |
|---|---:|---:|
| Accuracy | 0.597 | 0.153 |
| ROC-AUC | 0.597 | 0.157 |
| Balanced Accuracy | 0.597 | 0.152 |

The results indicate modest predictive discrimination, with substantial variability across validation folds.

## Results & Interpretation

### Gene Expression Differences

ANOVA feature selection identified 10 genes exhibiting the strongest differences in expression between the two treatment-response groups.

H2AC11, H2BC12, and TNNT2 had the highest F-scores, indicating comparatively strong differences in expression between the groups.

### Logistic Regression Coefficients

The fitted logistic regression model produced both positive and negative coefficients.

PAQR6, TNNT2, and SOX15 had the largest positive coefficients, while H2BC11 and H2BC12 had negative coefficients.

These coefficients represent conditional statistical associations within the fitted model, rather than evidence of causal biological relationships.

### Predictive Performance

The model achieved:

- **59.7% mean cross-validation accuracy**
- **0.597 mean ROC-AUC**
- **59.7% mean balanced accuracy**

The results suggest that the selected gene-expression features provide limited classification performance in this small dataset.

The difference between the original train-test evaluation and corrected cross-validation results highlighted the importance of preventing data leakage during feature selection and model evaluation.

## Visualizations

The analysis includes the following visualizations:

1. **Treatment Response Distribution:** Distribution of responder and non-responder samples.
2. **ANOVA Feature Selection:** Top 10 genes ranked by ANOVA F-score.
3. **Logistic Regression Coefficients:** Direction and magnitude of gene-level model coefficients.
4. **Gene Expression Distributions:** Comparison of expression levels for the five highest-ranked genes across treatment-response groups.
5. **Cross-Validation Performance:** Distribution of accuracy and ROC-AUC scores across repeated validation folds.

## Limitations

- **Small sample size:** The analysis includes only 51 patient samples, limiting statistical power and model generalizability.
- **High dimensionality:** The number of gene-expression features substantially exceeds the number of patient observations.
- **Model variability:** Cross-validation results demonstrate considerable sensitivity to the composition of training and validation folds.
- **Feature-selection stability:** Selected genes may vary across different training samples.
- **External validation:** Independent patient datasets would be necessary to evaluate generalizability.
- **Biological validation:** Additional research would be required to establish the biological significance of identified genes.

The findings should be interpreted as exploratory statistical associations rather than validated predictive biomarkers or clinically actionable results.

## Future Improvements

- Evaluate feature-selection stability across cross-validation folds.
- Compare logistic regression with alternative classification algorithms.
- Investigate relationships between selected genes and established biological pathways.
- Explore larger independent gene-expression datasets.
- Evaluate model performance using external validation data.

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Statistical Analysis
- ANOVA Feature Selection
- Logistic Regression
- Machine Learning

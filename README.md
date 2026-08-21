# Machine Learning Modeling for Obesity Risk Assessment in Latin America

## Project Overview & Context
Adult obesity in Latin America and the Caribbean has tripled since 1975, affecting 24% of the regional population and impacting the lives of hundreds of thousands (UNICEF, 2019). In Mexico, Peru, and Colombia, this explosive rise is driven by a complex interplay of socioeconomic status, rapid urbanization, behavioral dietary shifts toward processed foods, and environmental influences. Addressing this epidemic requires multi-faceted interventions targeting both individual and societal behaviors.

### Objectives
* Exploratory Analytics: Perform statistical summaries and generate data visualizations to uncover underlying patterns and relationships prior to modeling.
* Predictive Classification: Develop and evaluate machine learning models capable of accurately classifying individuals into distinct obesity risk categories based on demographic, dietary, and physical lifestyle factors.
* Feature Determinants: Identify the primary lifestyle predictors and determinants that contribute most significantly to obesity levels.

## Dataset Overview
* Source: UCI Machine Learning Repository (Palechor & de la Hoz Manotas, 2019)
* Sample Size: 2,111 individual instances across Mexico, Peru, and Colombia
* Target Variable: `NObeyesdad` (7 distinct risk categories: Insufficient Weight, Normal Weight, Overweight Level I, Overweight Level II, Obesity Type I, Obesity Type II, Obesity Type III)
* Feature Set: 16 attributes covering demographics, eating habits and physical condition

## Methodology and Technical Pipeline
* Exploratory Data Analysis (EDA): Cleaned raw data, handled categorical variables, and generated 11 univariate and multivariate plots to uncover behavioural correlations.
* Feature Engineering & Selection: Derived the continuous BMI metric and applied F-Score testing and Random Forest feature importance to isolate top predictive drivers.
* Data Preprocessing: Standardised continuous features using StandardScaler and applied LabelEncoder / get_dummies for categorical encoding.
* Model Tuning & Optimisation: Evaluated four classification algorithms—Multinomial Logistic Regression, Decision Trees, K-Nearest Neighbours (KNN), and Neural Networks (MLP)—using RandomizedSearchCV / GridSearchCV with 5-fold cross-validation.
* Statistical Validation: Conducted paired sample t-tests across cross-validation folds to confirm whether performance differences were statistically significant.

## Model Performance
| Model | Test Accuracy | Precision (Macro) | Recall (Macro) | F1-Score (Macro) | Key Status |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Decision Tree (DT)** | **98.11%** | 0.9812 | 0.9821 | 0.9815 | High Overfitting Risk |
| **Neural Network (MLP)** | **97.32%** | 0.9711 | 0.9711 | 0.9710 | Black-Box / Low Interpretability |
| **Multinomial Logistic Regression (MLR)** | **96.69%** | 0.9675 | 0.9663 | 0.9660 | **Selected Model (Best Balance)** |
| **K-Nearest Neighbours (KNN)** | **90.54%** | 0.9011 | 0.9016 | 0.9012 | Statistically Inferior |

## Model Selection & Comparative Verdict
Based on the detailed performance metrics, RandomizedSearchCV hyperparameter tuning, confusion matrices, and paired t-tests across 5-fold cross-validation, Multinomial Logistic Regression (MLR) is selected as the optimal model for deployment.

### Summary of Model Evaluations
* Decision Tree (DT) — Test Accuracy: 98.11%
  * Achieved the highest raw accuracy and near-perfect classification across Obesity Types II and III.
  * Limitation: Near-perfect F1-scores suggest a high risk of overfitting, meaning it may not generalise well to unseen real-world populations.

* Neural Network (MLP) — Test Accuracy: 97.32%
  * Effectively captured complex non-linear relationships with high overall accuracy.
  * Limitation: Suffers from "black-box" interpretability issues—a major constraint in medical and public health applications where clinical transparency is required.

* K-Nearest Neighbors (KNN) — Test Accuracy: 90.54%
  * Showed no signs of overfitting and demonstrated strong generalization potential.
  * Limitation: Statistically inferior performance (p<10−16) compared to all other candidate models.

* Multinomial Logistic Regression (MLR) — Test Accuracy: 96.69%
  * Achieved highly balanced precision and recall across all 7 risk categories, particularly for nuanced boundaries like Normal Weight and Overweight Level I.
  * Offers full model interpretability, fast computational inference, and transparent decision boundaries.

## Statistical Validation & Final Verdict
While Decision Tree (98.11%) and Neural Network (97.32%) achieved slightly higher raw test accuracy, Multinomial Logistic Regression (MLR at 96.69%) is the optimal choice for real-world deployment.
* Statistically Equivalent: Paired t-tests (p=0.561) prove the accuracy gap between MLR and Decision Trees is statistically insignificant.
* Resistant to Overfitting: Avoids the near-perfect scores of complex models that risk failing on unseen regional populations
* Clinical Transparency: Unlike black-box Neural Networks, MLR yields interpretable feature weights—essential for healthcare providers and public health policymakers.
* Lightweight & Scalable: Enables fast, low-cost inference in resource-constrained public health systems.

Conclusion: MLR provides the best operational balance of high predictive accuracy, verified statistical stability, and complete model transparency.

## How to Reproduce
1. Clone the Repository & Install Dependencies:
   ```bash
   git clone [https://github.com/priyankaapk/obesity-risk-prediction-ml.git](https://github.com/priyankaapk/obesity-risk-prediction-ml.git)
   cd obesity-risk-prediction-ml
   pip install -r requirements.txt
2. Execute 01_data_cleaning_and_eda.ipynb to process raw data in /data and generate cleaned dataset with explanatory data analysis.
3. Execute 02_model_building_and_evaluation.ipynb to run hyperparameter searches and cross-validation pipelines.

## References
UCI Machine Learning Repository. (2019, August 26). Estimation of obesity levels based on eating habits and physical condition in individuals from Colombia, Peru and Mexico. Archive.ics.uci.edu. https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition

United Nations calls for urgent action to curb the rise in hunger and obesity in Latin America and the Caribbean. UNICEF (2019). Www.unicef.org. https://www.unicef.org/lac/en/press-releases/united-nations-calls-urgent-action-curb-rise-hunger-and-obesity-latin-america-and

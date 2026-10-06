# BCG Data Science Project

## Project Overview
This project was completed as part of the BCG Data Science Virtual Experience.
The project focuses on analysing customer churn for an energy business and developing a machine learning model to predict customer churn.
The analysis follows an end-to-end data science workflow:

- Exploratory Data Analysis
- Data Cleaning and Preparation
- Feature Engineering
- Machine Learning Modelling
- Model Evaluation
- Business Interpretation
- Recommendations

The primary objective is to understand customer churn patterns, investigate factors associated with churn, and build a predictive model that can help identify customers who may be at risk of churning.

##  Business Problem
Customer churn is an important business problem because losing customers can negatively affect revenue and long-term customer relationships.
The business needs to understand:

- Which customers are more likely to churn?
- What factors are associated with customer churn?
- Is customer price sensitivity related to churn?
- Can customer churn be predicted using available customer and pricing information?
- Which customers may require proactive retention efforts?
- How can analytical and machine learning results support business decisions?

  ### Business Objective
The objective of this project is to use customer, consumption and pricing information to understand churn behaviour and develop a machine learning model that can help identify customers at higher risk of churn.


## Model Evaluation
- Accuracy
- Precision
- Recall
- F1 Score

## Tools & Technologies
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

##  Data
The project uses two main sources of information:

### Customer Data
The customer dataset contains information related to:

- Customer ID
- Sales channel
- Consumption
- Forecasted consumption
- Energy discount
- Meter rent
- Energy prices
- Power prices
- Gas availability
- Installed power
- Product information
- Net margin
- Customer tenure
- Customer origin
- Churn status

### Pricing Data
The pricing dataset contains historical pricing information including:

- Customer ID
- Price date
- Off-peak variable price
- Peak variable price
- Mid-peak variable price
- Off-peak fixed price
- Peak fixed price
- Mid-peak fixed price

### Dataset Size
The customer dataset contains:

- **14,606 customers**
- **26 original customer-level columns**

The pricing dataset contains:
- **193,002 pricing records**
- **8 columns**

The customer and pricing information were combined using the customer ID to support the analysis.

---

## Target Variable
The target variable is:

`churn`
Where:

- `0` = Customer retained
- `1` = Customer churned

### Churn Distribution

The dataset contains:

- **13,187 retained customers (90.28%)**
- **1,419 churned customers (9.72%)**

This shows that the dataset is imbalanced, with substantially fewer churned customers than retained customers.
This class imbalance is important when interpreting model performance.

---

## Data Preparation

The data preparation process included:

- Loading customer and pricing datasets
- Inspecting the structure of the datasets
- Reviewing data types
- Checking the available variables
- Preparing customer and pricing data for analysis
- Converting date fields into appropriate date formats
- Grouping pricing information by customer
- Calculating customer-level pricing measures
- Combining customer and pricing information
- Preparing the cleaned dataset for feature engineering
- Preparing the final dataset for machine learning

The customer dataset contained 14,606 records and the pricing dataset contained 193,002 records.

---

## Exploratory Data Analysis

The exploratory analysis was performed to understand the customer base and investigate relationships between customer characteristics, pricing information and churn.

### Key Questions Investigated

1. What proportion of customers churn?
2. What does the customer dataset contain?
3. What are the distributions of the numerical variables?
4. How does churn vary across customer characteristics?
5. Are pricing variables associated with churn?
6. Is price sensitivity related to customer churn?
7. Which numerical variables show the strongest relationship with churn?

---

## Churn Analysis
The analysis identified the following churn distribution:

| Customer Status | Customers | Percentage |
|---|---:|---:|
| Retained | 13,187 | 90.28% |
| Churned | 1,419 | 9.72% |
| Total | 14,606 | 100% |

### Key Finding
Approximately **9.72% of customers in the dataset churned**, while **90.28% were retained**.
The relatively small proportion of churned customers creates a class imbalance that must be considered when evaluating the machine learning model.

---

## Pricing Analysis

The pricing information was aggregated at customer level.
Average pricing variables were calculated for:

- Off-peak variable price
- Peak variable price
- Mid-peak variable price
- Off-peak fixed price
- Peak fixed price
- Mid-peak fixed price

The resulting customer-level pricing data was merged with the customer dataset.
The combined dataset contained **14,606 customers and 32 columns** before the additional feature-engineering stage.

---

## Correlation Analysis

The numerical variables were analysed to understand their relationship with churn.

The strongest positive correlations with churn in the analysis were:

| Variable | Correlation with Churn |
|---|---:|
| margin_net_pow_ele | 0.0958 |
| margin_gross_pow_ele | 0.0957 |
| price_peak_fix | 0.0472 |
| price_mid_peak_var | 0.0465 |
| price_mid_peak_fix | 0.0448 |
| forecast_meter_rent_12m | 0.0442 |
| net_margin | 0.0411 |
| pow_max | 0.0304 |
| price_peak_var | 0.0296 |
| forecast_price_energy_peak | 0.0293 |

The analysis also showed negative correlations for variables such as:

- `num_years_antig`
- `cons_12m`
- `cons_last_month`
- `cons_gas_12m`

### Interpretation

The correlations suggest that several customer financial, pricing and consumption variables have some relationship with churn.

However, the correlations are relatively small, so they should not be interpreted as proof that these variables directly cause churn.

---

## Feature Engineering

Feature engineering was performed to create additional variables that could provide useful predictive information for the churn model.

###  December-January Off-Peak Price Difference

The project recreated the required feature representing the difference between December and January off-peak prices.

Two features were created:

- `offpeak_diff_dec_january_energy`
- `offpeak_diff_dec_january_power`

These features capture changes in off-peak energy and power prices between the relevant December and January periods.

---

## Off-Peak Variable Price Range

The following feature was created:

`offpeak_var_price_range`

This represents the range of off-peak variable prices for each customer.

**Formula:**

`offpeak_var_price_range = Maximum off-peak variable price - Minimum off-peak variable price`

---

## Baseline Model

Because the churn dataset is highly imbalanced, a majority-class baseline provides an important reference point.
The majority class is retained customers, representing 90.28% of the dataset.
This demonstrates why accuracy alone is not sufficient for evaluating a churn prediction model. The final Random Forest model should therefore be compared using precision, recall and F1 score in addition to accuracy.        

## Evaluation Methodology
The model was evaluated on the unseen test dataset using multiple classification metrics.
The following measures were considered:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix
- Feature Importance

Because the churn dataset is imbalanced, particular attention was given to precision, recall and F1 score rather than relying only on accuracy.

| Metric | Score |
|--------|-------|
| Accuracy | 90.39% |
| Precision | 82.61% |
| Recall | 5.19% |
| F1 Score | 9.77% |

### Interpretation

The model achieved an accuracy of approximately 90.39% and a precision of 82.61%. However, the recall was only 5.19%, and the F1-score was 9.77%.The high accuracy is influenced by the large number of non-churn customers correctly classified by the model. However, the low recall indicates that the model is missing a large proportion of customers who actually churn.For a customer churn prediction problem, recall is particularly important because identifying customers who are likely to churn can help the business take preventive actions.

### Areas for Improvement

The model performance could be improved by addressing class imbalance, tuning the Random Forest hyperparameters, and experimenting with additional feature engineering techniques.

## Confusion Matrix

The confusion matrix was used to evaluate how well the Random Forest model classified retained and churned customers.

It consists of:

- True Negatives (TN)
- False Positives (FP)
- False Negatives (FN)
- True Positives (TP)

The confusion matrix is particularly important for this project because the churn class represents only 9.72% of customers.

The confusion matrix for the Random Forest model is:

| | Predicted Retained | Predicted Churn |
|---|---:|---:|
| **Actual Retained** | 3,282 | 4 |
| **Actual Churn** | 347 | 19 |

The confusion matrix consists of:

- True Negatives (TN): 3,282
- False Positives (FP): 4
- False Negatives (FN): 347
- True Positives (TP): 19

The model correctly identified 19 churned customers but missed 347 actual churned customers. This explains the low recall of 5.19% and indicates that improving the identification of actual churners is an important area for future model improvement.

## Model Evaluation

The Random Forest Classifier was evaluated using a confusion matrix, accuracy, precision, recall, and F1-score.

### Confusion Matrix

The confusion matrix obtained from the test dataset is:

| | Predicted: No Churn | Predicted: Churn |
|--------------------|---------------------|------------------|
| Actual: No Churn | 3282 | 4 |
| Actual: Churn | 347 | 19 |

The model correctly predicted 3,282 customers who did not churn and 19 customers who actually churned. However, it incorrectly classified 347 actual churners as non-churners.


## Feature Importance

The Random Forest model provides feature importance values that show which variables contributed most to the model's predictions.
Feature importance helps identify the variables that were most useful for predicting customer churn.
These values should be interpreted as model-based predictive importance and should not be considered proof of causation.

## Connecting Model Output to the Business Problem

The business objective is to identify customers who may be at risk of churning so that the business can take proactive retention actions.The Random Forest model achieved 90.39% accuracy and 82.61% precision. However, its recall was only 5.19%, indicating that the model identifies only a small proportion of customers who actually churn.Therefore, the current model should not be used as a standalone churn-detection system.

The model can instead be used as a decision-support tool together with:

- Customer behaviour
- Consumption patterns
- Pricing information
- Customer tenure
- Financial indicators
- Business knowledge

Improving recall should be a key priority because missing an actual churner can result in a missed opportunity for customer retention.
Future model improvements should therefore focus on identifying more actual churners while maintaining an acceptable level of precision.


## Challenges

During the analysis and modelling process, several challenges were considered:

- The churn dataset was imbalanced, with only 9.72% of customers classified as churned.
- The class imbalance makes accuracy alone insufficient for evaluating model performance.
- Customer and pricing data had to be combined to create a suitable modelling dataset.
- Additional pricing and consumption features had to be engineered to improve the information available to the model.
- The model achieved high accuracy but relatively low recall, showing that identifying the majority of actual churners remains challenging.
- Feature importance and model results need to be interpreted carefully because statistical association does not necessarily imply causation.
- The model requires further improvement before it can be considered a reliable standalone churn-detection system.

---

## Business Recommendations

Based on the customer churn analysis, pricing analysis, feature engineering and machine learning results, the following business recommendations are proposed:

### 1. Develop Targeted Customer Retention Strategies

The business should identify customers with characteristics associated with higher churn risk and develop targeted retention strategies.

### 2. Monitor Pricing Changes

Pricing-related variables showed measurable relationships with customer churn.

The business should regularly monitor changes in:

- Off-peak variable prices
- Peak variable prices
- Mid-peak variable prices
- Fixed prices
- Changes in energy and power prices

Customers experiencing significant pricing changes can be monitored more closely for potential churn risk.

### 3. Analyse Customer Price Sensitivity

The engineered pricing features can be used to identify customers who may be more sensitive to changes in energy prices.

### 4. Monitor Changes in Customer Consumption

The project created features such as:

- `consumption_change`
- `consumption_ratio`

These measures can help identify changes in customer consumption behaviour.

### 5. Prioritise High-Risk Customers

The churn model can be used as a decision-support tool to help prioritise customers who may require additional attention. However, the current model has low recall, so predictions should not be used as the sole basis for retention decisions.

### 6. Improve the Churn Prediction Model

The current model achieved:

- Accuracy: 90.39%
- Precision: 82.61%
- Recall: 5.19%
- F1 Score: 9.77%

Although accuracy and precision are relatively high, the low recall indicates that the model is missing a large proportion of actual churners.

Possible improvements include:

- Addressing class imbalance
- Testing different classification thresholds
- Evaluating class-weighted models
- Testing additional machine-learning algorithms
- Comparing different model performance metrics
- Optimising for improved recall while maintaining acceptable precision

### 7. Focus on Retention Rather Than Reactive Customer Management

The business can use the results of the analysis to move towards proactive customer retention.

### 8. Use Customer-Level Insights for Personalised Retention

Retention strategies should be tailored to customer characteristics rather than using a single approach for all customers.

### 9. Continuously Monitor Customer and Pricing Data

Customer behaviour and energy prices can change over time.

The business should periodically monitor:

- Customer consumption
- Energy and power prices
- Customer tenure
- Customer financial indicators
- Churn rates
- Model performance

Regular monitoring can help identify changes in churn patterns and ensure that retention strategies remain relevant.

### 10. Use Data-Driven Retention Decisions

The analysis should be used as a decision-support framework rather than as an automatic decision-making system.

Business teams should combine:

- Churn predictions
- Customer behaviour
- Pricing information
- Consumption patterns
- Customer value
- Business knowledge

---

## Model Limitations

- The churn dataset is highly imbalanced, with only 9.72% of customers classified as churned.
- The model achieved high accuracy of 90.39%, but recall was only 5.19%, meaning that many actual churners were not identified.
- Accuracy alone is not sufficient for evaluating this imbalanced classification problem.
- The Random Forest model may require further hyperparameter tuning and comparison with other machine-learning algorithms.
- The model was evaluated using a 75:25 train-test split; additional cross-validation could provide a more robust evaluation.
- Statistical associations identified during the analysis should not be interpreted as causal relationships.
- The current model should be used as a decision-support tool rather than as a standalone automated churn-detection system.
- Further improvement using class-imbalance techniques, classification-threshold optimisation and additional evaluation metrics is recommended.

## GitHub Repository Link:
https://github.com/Mahanand4/BCG_Data_Science_Project

## Certificate Link:
[BCG Data Science Virtual Experience Certificate](BCG%20Certificate.pdf)



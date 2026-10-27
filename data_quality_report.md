# Data Quality and Exploratory Analysis — Customer Churn

## 1. Executive summary
The supplied dataset contains **15 rows and 11 columns**. It is a small synthetic sample, so findings are descriptive and should not be generalized to a real customer population. No missing values, exact duplicate rows, duplicate customer IDs, invalid values in the checked ranges, or invalid category labels were found. All rows were retained. The supplied `TotalCharges` values match `MonthlyCharges × TenureMonths` to two decimal places.

## 2. Dataset profile
- Rows: 15
- Columns: 11
- Exact duplicate rows: 0
- Duplicate CustomerID values: 0
- Missing cells: 0
- Churn: 7 Yes / 8 No
- Observed churn rate: 46.7%

### Data types
- `CustomerID`: string
- `Gender`: string
- `Age`: int64
- `TenureMonths`: int64
- `SubscriptionType`: string
- `MonthlyCharges`: float64
- `TotalCharges`: float64
- `ContractType`: string
- `SupportTickets`: int64
- `PaymentMethod`: string
- `Churn`: string

## 3. Data-quality checks and decisions
| Check | Result | Decision |
|---|---:|---|
| Missing values | 0 cells | No imputation needed. |
| Exact duplicate rows | 0 | No rows removed. |
| Duplicate CustomerID values | 0 | No IDs removed. |
| Invalid category labels | 0 | Category values match the expected labels. |
| Age outside 18–100 | 0 | No age correction needed under this validation rule. |
| Tenure below zero | 0 | No correction needed. |
| Monthly charges <= 0 | 0 | No correction needed. |
| Total charges < 0 | 0 | No correction needed. |
| Support tickets < 0 | 0 | No correction needed. |
| TotalCharges arithmetic mismatch | 0 | Values match the rule `MonthlyCharges × TenureMonths`, rounded to 2 decimals. |

Text columns were trimmed for leading/trailing whitespace. Numeric fields were retained in their existing numeric types. Outlier candidates were identified with the 1.5×IQR rule and are listed in the notebook; they were not automatically deleted because a statistical flag is not, by itself, proof of a data error.

## 4. Summary statistics
- Mean age: 39.1 years; range: 23–60.
- Mean tenure: 18.8 months; range: 2–48.
- Mean monthly charges: 84.66.
- Mean total charges: 2088.48.
- Mean support tickets: 2.53.

## 5. Initial patterns
### Churn by contract type
                sum  count  mean
ContractType                    
Month-to-Month    7      7 100.0
One Year          0      4   0.0
Two Year          0      4   0.0

### Churn by subscription type
                  sum  count  mean
SubscriptionType                  
Basic               5      7  71.4
Enterprise          0      4   0.0
Pro                 2      4  50.0

### Mean support tickets by churn status
- No: 1.00
- Yes: 4.29

These are small-sample descriptive patterns, not evidence of causation. Group percentages can change substantially with one customer.

## 6. Limitations
- Only 15 synthetic customer records are provided.
- No date/time field or customer acquisition context is available.
- Outlier thresholds are screening tools and require domain review.
- Results should not be used to make production retention decisions.

## 7. Reproducibility
Run `Customer_Churn_EDA.ipynb` from top to bottom in Jupyter Notebook or JupyterLab. The notebook reads `customer_churn_sample.csv` from the same folder and exports `cleaned_customer_churn.csv` and `data_dictionary.csv`.

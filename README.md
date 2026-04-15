# Lab 6 – Linear Regression
**Course:** ARTI308 – Machine Learning

---

## Project Overview

This lab applies **Linear Regression** to predict how much money a customer spends yearly on an e-commerce platform, based on their behavioral data (time on app, time on website, session length, and membership duration). The goal is to understand which features drive yearly spending and build a model that generalizes well on unseen data.

---

## Datasets

### 1. `Ecommerce_Customers` *(primary dataset)*
**Size:** 500 rows × 8 columns

| Feature | Description |
|---|---|
| `Email` | Customer email (not used in modeling) |
| `Address` | Customer address (not used in modeling) |
| `Avatar` | Avatar color (not used in modeling) |
| `Avg. Session Length` | Average length of in-store style advice sessions (minutes) |
| `Time on App` | Average time spent on the mobile app (minutes) |
| `Time on Website` | Average time spent on the website (minutes) |
| `Length of Membership` | Number of years the customer has been a member |
| `Yearly Amount Spent` | **Target variable** – total yearly spending in USD |

### 2. `USA_Housing.csv` *(supplementary dataset)*
**Size:** 5,000 rows × 7 columns

| Feature | Description |
|---|---|
| `Avg. Area Income` | Average income of residents in the area |
| `Avg. Area House Age` | Average age of houses in the area |
| `Avg. Area Number of Rooms` | Average number of rooms per house |
| `Avg. Area Number of Bedrooms` | Average number of bedrooms per house |
| `Area Population` | Population of the area |
| `Price` | **Target variable** – house price |
| `Address` | House address (not used in modeling) |

---

## Techniques Applied

### Task 1 – Data Loading & Exploration
- Loaded the Ecommerce dataset and inspected it using `.info()` and `.describe()`
- Identified text columns (`Email`, `Address`, `Avatar`) to exclude from modeling
- Confirmed no missing values or duplicate rows — no cleaning required

### Task 2 – Exploratory Data Analysis (EDA)
- **Pairplot** – Visualized relationships between all numerical features and the target variable
- **Correlation Heatmap** – Measured linear correlation between features and `Yearly Amount Spent`
- Key findings:
  - `Length of Membership` has the **strongest** correlation with yearly spending
  - `Time on App` shows a strong positive relationship
  - `Time on Website` has minimal impact on spending

### Task 3 – Feature Engineering
- No new features were created; the numerical columns were already meaningful and usable
- Dropped text columns (`Email`, `Address`, `Avatar`) which cannot be used in linear regression

### Task 4 – Model Training
- Features used: `Avg. Session Length`, `Time on App`, `Time on Website`, `Length of Membership`
- Target: `Yearly Amount Spent`
- Split: **70% training / 30% testing** (`random_state=101`)
- Trained a `LinearRegression` model using `scikit-learn`

### Task 5 – Coefficient Interpretation
| Feature | Coefficient | Interpretation |
|---|---|---|
| `Avg. Session Length` | ~$25.98 | Each extra minute in-session → +$25.98/year |
| `Time on App` | ~$38.59 | Each extra minute on app → +$38.59/year |
| `Time on Website` | ~$0.19 | Almost no effect on spending |
| `Length of Membership` | ~$61.28 | Strongest predictor — each extra year → +$61.28/year |

### Task 6 – Predictions & Residual Analysis
- **Actual vs. Predicted scatter plot** – Points fall close to the diagonal, indicating accurate predictions
- **Residuals histogram** – Residuals are normally distributed and centered around 0, confirming linear regression assumptions are satisfied

### Task 7 – Model Evaluation

| Metric | Value |
|---|---|
| MAE (Mean Absolute Error) | ~$7.23 |
| MSE (Mean Squared Error) | ~79.81 |
| RMSE (Root Mean Squared Error) | ~$8.93 |
| R² (R-squared) | ~0.989 |



---

## Conclusion

The Linear Regression model achieved an **R² of 0.989**, explaining nearly 99% of the variance in yearly customer spending — an excellent result. The analysis revealed that **Length of Membership** and **Time on App** are the two most influential predictors, while **Time on Website** contributes almost nothing. These insights could help the business decide whether to invest more in improving the mobile app experience or focus on retaining long-term members.

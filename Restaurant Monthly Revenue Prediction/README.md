# Restaurant Monthly Revenue Prediction

**Status:** EDA and preprocessing complete. Model training in progress.

## Problem Statement

Predict a restaurant's monthly revenue from measurable business characteristics (customer volume, pricing, marketing spend, cuisine type, promotions, reviews). This is a **supervised regression** problem.

## Dataset Description

[Restaurant Revenue Prediction](https://www.kaggle.com/datasets/mrsimple07/restaurants-revenue-prediction/data) — 1000 restaurants, 7 features + 1 target.

| Feature | Type | Description |
|---|---|---|
| Number_of_Customers | int | Customers visiting the restaurant |
| Menu_Price | float | Average menu item price |
| Marketing_Spend | float | Amount spent on marketing |
| Cuisine_Type | categorical | Italian / Japanese / Mexican / American |
| Average_Customer_Spending | float | Average spend per customer |
| Promotions | binary (0/1) | Whether a promotion was active |
| Reviews | int | Review score/count |
| Monthly_Revenue | float | **Target** |

No missing values, no duplicate rows.

## Exploratory Data Analysis

- Target distribution is approximately symmetric (skew ≈ 0) — no transform needed.
- 5 rows had negative revenue, all tied to restaurants with very few customers (10-17) — treated as invalid data, not a real business scenario.
- Correlation with target: `Number_of_Customers` (r≈0.75, dominant), `Marketing_Spend` (r≈0.27), `Menu_Price` (r≈0.26). `Reviews` and `Average_Customer_Spending` showed no relationship (r ≈ -0.02 to -0.04), confirmed by scatter plots as well as correlation.
- Categorical features tested with ANOVA (`Cuisine_Type`, p≈0.85) and t-test (`Promotions`, p≈0.64) — neither showed a statistically significant effect on revenue, despite `Cuisine_Type`'s group-average bar chart initially suggesting otherwise.

## Data Preprocessing

- Dropped the 5 rows with negative `Monthly_Revenue`.
- Dropped `Cuisine_Type` (no significant relationship with target, confirmed statistically, not just visually).
- No further encoding needed — remaining features are all numeric.
- Final shape: 995 rows × 7 columns (6 features + target).

## Model Implementation *(in progress)*

Plan: train and compare two Linear Regression models on an identical train/test split:
- **Model A** — all remaining features.
- **Model B** — only the features EDA showed a real relationship with (`Number_of_Customers`, `Menu_Price`, `Marketing_Spend`).

## Evaluation Metrics *(pending)*

Will use MAE, RMSE, and R² — to be filled in once training is complete.

## Results & Discussion *(pending)*

## Future Improvements *(pending — candidates so far)*

- Try regularized models (Ridge/Lasso) to see if they down-weight the weak features automatically.
- Try non-linear models (e.g. polynomial features, tree-based models) in case `Reviews`/`Average_Customer_Spending` have a non-linear relationship EDA's linear correlation missed.

## Files

- `Restaurant_Monthly_Revenue_Prediction.ipynb` — full notebook
- `Restaurant_revenue_.csv` — dataset

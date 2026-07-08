# Marketing Mix Modelling & Budget Allocation

An end-to-end predictive analytics project that analyses marketing channel performance, predicts purchasing outcomes, and simulates incremental budget allocation strategies to maximise revenue.

## Project Overview

Digital marketers allocate budgets across multiple channels, including paid search, shopping campaigns, and social media. However, historical spending patterns alone may not provide sufficient guidance for future budget allocation.

This project develops an end-to-end predictive modelling workflow to:

- Analyse the relationship between marketing activity and purchasing outcomes
- Build and compare regression models for revenue prediction
- Evaluate model performance using time-aware validation
- Estimate the marginal effectiveness of different marketing channels
- Simulate incremental marketing spend scenarios
- Recommend data-driven budget allocation strategies

## Business Problem

The project addresses the following business question:

> If additional marketing budget becomes available, which channels should receive the investment, and how should the budget be allocated to maximise revenue?

The problem is formulated as a supervised regression task using historical marketing activity and purchasing behaviour.

## Dataset

The project uses the **Multi-Region Marketing Mix Modelling (MMM) Dataset for Several eCommerce Brands**.

The dataset contains daily marketing performance data, including:

- Marketing spend across digital channels
- Paid clicks and impressions
- Non-paid engagement metrics
- First purchases and total purchases
- Organisational verticals
- Time-based observations

The dataset covers marketing activity from 2021 to 2024.

## Project Workflow

### 1. Exploratory Data Analysis

Exploratory analysis was conducted to understand:

- Data quality and missing values
- Correlations between marketing variables and purchasing outcomes
- Time-series patterns in marketing activity
- Differences in purchasing behaviour across organisational verticals

The analysis identified substantial fluctuations and extreme spikes in marketing activity and purchases, highlighting the importance of time-aware modelling.

### 2. Data Preparation

The preprocessing pipeline included:

- Handling missing marketing activity values
- Aggregating marketing exposure variables
- Creating total paid spend, clicks, and impressions features
- Validating feature distributions
- Preserving chronological order during model development

A time-based train-validation-test split was used to prevent data leakage:

| Dataset | Period | Observations |
|---|---|---:|
| Training | Aug 2021 – Jul 2023 | 701 |
| Validation | Jul 2023 – Dec 2023 | 150 |
| Test | Dec 2023 – May 2024 | 151 |

## Model Development

Four predictive models were developed and compared:

- Seasonal Naive Baseline
- Ridge Regression
- ElasticNet Regression
- Bootstrapped Ridge Regression

Tree-based models, including Random Forest and Histogram Gradient Boosting, were also explored during development but were excluded from the final comparison due to weaker validation performance.

Regularised regression models were prioritised because of their ability to handle multicollinearity among marketing variables while maintaining model interpretability.

## Model Performance

The models were evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- Mean Absolute Percentage Error (MAPE)
- R² on the log scale

| Model | MAE | RMSE | MAPE | R² |
|---|---:|---:|---:|---:|
| Bootstrapped Ridge | **2,051.79** | **2,912.04** | 0.1622 | **0.8059** |
| Ridge Regression | 2,067.59 | 2,934.60 | **0.1620** | 0.8033 |
| Seasonal Naive | 2,470.81 | 3,435.31 | 0.2241 | 0.6963 |
| ElasticNet | 3,885.63 | 4,436.08 | 0.4149 | 0.3776 |

The **Bootstrapped Ridge Regression model** achieved the strongest overall predictive performance and was selected as the final model.

## Marketing Channel Analysis

The final model was used to estimate the marginal effectiveness of additional marketing spend across channels.

The analysis found that:

- `META_OTHER_SPEND` generated the highest predicted marginal return
- `META_FACEBOOK_SPEND`, `META_INSTAGRAM_SPEND`, and `GOOGLE_PMAX_SPEND` also showed positive predicted responses
- Some channels showed weak or negative marginal effects under the current model configuration

These results were used to simulate how additional marketing budget could be distributed across channels.

## Budget Allocation Recommendation

Based on the model simulation, the recommended allocation of incremental marketing budget was:

| Marketing Channel | Recommended Allocation |
|---|---:|
| META_OTHER_SPEND | ~83% |
| META_FACEBOOK_SPEND | ~8% |
| META_INSTAGRAM_SPEND | ~6% |
| GOOGLE_PMAX_SPEND | ~3% |
| Other Channels | ~0% |

The results suggest that reallocating incremental budget towards channels with stronger predicted marginal efficiency could improve overall revenue performance.

These recommendations should be interpreted as directional model-based insights rather than definitive causal estimates and should be validated through controlled experiments before large-scale implementation.

## Key Findings

- Regularised regression models significantly outperformed the seasonal baseline
- Bootstrapped Ridge achieved an R² of **0.81** on the log scale
- Marketing channels showed substantial differences in predicted marginal efficiency
- Model-based simulations identified potential opportunities to improve incremental budget allocation
- Residual analysis showed that sudden campaign and revenue spikes remain difficult to predict

## Limitations & Future Work

The current model does not explicitly account for:

- Advertising carryover effects
- Marketing saturation and diminishing returns
- Macroeconomic conditions
- Competitor activity
- Offline marketing campaigns
- Other external factors affecting consumer demand

Future development could incorporate:

- Adstock transformations
- Saturation curves
- Bayesian Marketing Mix Modelling
- Additional contextual and macroeconomic variables
- Controlled experiments for validating budget recommendations

## Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

## Repository Structure

```text
predictive-analytics-MMM/
│
├── data/
│
├── notebooks/
│   ├── 01_data_preparation_eda.ipynb
│   └── 02_modelling_evaluation.ipynb
│
├── outputs/
│
├── requirements.txt
│
└── README.md

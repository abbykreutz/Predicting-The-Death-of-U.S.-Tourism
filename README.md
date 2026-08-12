# Predicting the Death of U.S. Tourism

**DATASCI 207: Applied Machine Learning | Summer 2026 | Final Project**

**Abigail Kreutz** (abigailkreutz@berkeley.edu) | **Peter Huang** (huangpeter@berkeley.edu) | **Hope Tadsen** (hope_tadsen@berkeley.edu)

## Overview

This project investigates whether machine learning can predict monthly U.S. tourist arrivals using socio-political and economic indicators. Our target was monthly I-94 visitor arrivals to the United States, with features derived from tourism statistics, GDP, U.S. political party control, and politically violent events.

We compared baseline models with Random Forest and XGBoost and explored how feature engineering, time-series structure, COVID-19, and differing data availability affected predictive performance.

## Data & Features

The project combines four primary sources of information:

* **I-94 Arrivals:** Monthly international visitor arrivals to the U.S. from 2000–2026, used as the prediction target.
* **Tourism & GDP:** Inbound tourism and economic indicators used to capture broader economic and travel trends.
* **Political Party Control:** U.S. House, Senate, and presidential party control, with features representing political alignment, elections, and changes in control.
* **Armed Conflict & Political Unrest:** Event-level U.S. data from the Armed Conflict Location & Event Data Project (ACLED), filtered to politically violent events and aggregated into monthly event and time-series features.

Because the datasets covered different time periods, we evaluated both a **long-history dataset** and a separate **2020–2026 experiment** to investigate whether armed-conflict features added predictive value and evaluate model robustness to COVID-19 as an extreme outlier affecting multiple features and U.S. tourist arrivals.

## Modeling Approach

We began with a mean-value predictor and linear regression as baseline models before evaluating Random Forest and XGBoost.

Feature engineering and model validation included:

* Lagged I-94 arrival features (1- and 12-month lag)
* 3-month rolling averages
* Sine/cosine transformations for annual seasonality
* Politically violent event counts, lags, and rolling measures
* Political-control and election indicators
* Tourism and GDP features
* Chronological train/test splitting to prevent future-data leakage
* Time-series cross-validation
* Random Forest and XGBoost model comparison
* Hyperparameter tuning using `RandomizedSearchCV` with `TimeSeriesSplit`

Feature engineering ultimately produced substantially larger improvements than hyperparameter tuning. The best-performing model was the **untuned XGBoost long-history model**, which achieved:

* **RMSE:** 557,709
* **MAE:** 406,561
* **R²:** 0.753

Hyperparameter tuning reduced performance for both Random Forest and XGBoost, highlighting the importance of feature engineering and appropriate time-series validation for this problem.

## My Contributions

My primary responsibility was the project's armed-conflict data analysis and feature engineering, alongside broader debugging and validation of the shared modeling.

* Owned EDA, cleaning, validation, and feature engineering for event-level U.S. armed-conflict and political-violence data.
* Rebuilt the conflict dataset using event-level records, restricting observations to the U.S. and politically violent events and validating monthly counts against published ACLED statistics.
* Engineered event-count, lagged, rolling, fatality, geographic, and event-type features for evaluating relationships between political violence and tourist arrivals.
* Diagnosed and corrected a political-data merge issue that was dropping the second year of each two-year congressional period and substantially reducing usable observations.
* Identified and corrected target leakage in annual tourism/GDP features and a global missing-value operation that was unnecessarily restricting the long-history modeling dataset.
* Reduced 14 candidate armed-conflict features to 3 using zero-variance and collinearity screening, incremental cross-validation RMSE, Lasso regularization, and Random Forest permutation importance.
* Added walk-forward time-series validation and matrix-rank checks to evaluate feature selection and model stability.
* Contributed to additional Random Forest and XGBoost experimentation and validation, including comparisons between short-history armed-conflict models and the long-history feature set.

## Repository Structure

### `Abby_EDA/`

EDA, cleaning, validation, and feature engineering for armed-conflict and political-unrest data.

### `Hope_EDA/`

EDA and cleaning for inbound tourism and GDP data.

### `Peter_EDA/`

EDA and cleaning for I-94 arrival target data and U.S. political party-control features.

### `Model_Testing.ipynb`

Primary modeling notebook containing baseline analysis, shared feature engineering, and Random Forest/XGBoost modeling using the longer historical dataset.

### `Additional_Modeling.ipynb`

Additional feature engineering, model refinement, validation, and experiments investigating armed-conflict features over the shorter period for which ACLED was available.

## Key Takeaways

Feature engineering and data validation had a larger impact on model performance than hyperparameter tuning. Time-based features—particularly lagged arrivals, rolling averages, and seasonal transformations—were the strongest predictors of future U.S. tourist arrivals.

The shorter history of armed-conflict data limited its usefulness for predictive modeling. Although politically violent events were negatively correlated with arrivals, this relationship was driven by COVID-19: conflict-event counts spiked around George Floyd and the BLM movement as tourism collapsed amid U.S. travel restrictions, causing the ACLED features to inadvertently encode information about the pandemic era rather than isolate an independent effect on tourism. The long-history feature set, which excluded ACLED, ultimately generalized better.

## 📄 Full Report

For complete methodology, results, figures, limitations, and references, see:

[**Predicting The Death of US Tourism — Final Report**](Predicting%20The%20Death%20of%20US%20Tourism_Final%20Report.pdf)

## Team Contributions

* **Peter Huang:** I-94 EDA and data cleaning, initial feature engineering, baseline modeling, and initial Random Forest/XGBoost modeling.
* **Abigail Kreutz:** Armed-conflict EDA and data cleaning, feature engineering and validation, data/model debugging, and additional Random Forest/XGBoost modeling and experimentation.
* **Hope Tadsen:** Repository creation, inbound tourism and GDP EDA and data cleaning, visual revisions for our final presentation and report.

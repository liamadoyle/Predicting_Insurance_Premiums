# Predicting Insurance Premiums

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset Description](#dataset-description)
3. [Methods and Approach](#methods-and-approach)
4. [Key Findings](#key-findings)
5. [Limitations and Future Work](#limitations-and-future-work)
6. [Repository Structure](#repository-structure)
7. [Technical Skills Demonstrated](#technical-skills-demonstrated)

## Project Overview

This project involved predicting insurance premiums (`premium_amount`) using machine learning models. The goal was to build an effective model that outperforms a baseline (mean prediction) and provides insights into the importance of various features. In addition, this project was completed to demonstrate a sample `tidymodels` workflow from start to finish.

## Dataset Description

The dataset used for this project was lifted from a [Kaggle dataset](https://www.kaggle.com/competitions/playground-series-s4e12/data) that was used for a recent competition on the website. This dataset consists of 1,200,000 observations and includes both numeric (e.g., ``) and categorical (e.g., ``) features. A random sample of 5,000 rows was used for this project to manage computational constraints. The target variable was `premium_amount`, representing the insurance premium that an individual pays.

## Methods and Approach

1. **Data Cleaning**:
   - Cleaned variable names using `janitor`.
   - Transformed `character` variables to `factor` using `dplyr`.
2. **Exploratory Data Analysis**:
   - Used summary statistics and visualizations to examine the structure and characteristics of the data.
3. **Preprocessing and Feature Engineering**:
   - Handled missing data with median (numeric) and mode (categorical) imputation.
   - Applied log10 transformation to reduce skewness in `annual_income`.
   - Normalized numeric features and dummy-coded categorical features.
   - Extracted time-based features (i.e., day-of-week, month, year) from a POSIXct variable (`policy_start_date`).
   - Removed irrelevant features (e.g., `id`) and features with near-zero variance.
4. **Modelling**:
   - Specified and trained three models: Elastic Net, Random Forest, and XGBoost.
   - Used 5-fold cross-validation and hyperparameter tuning using a racing method.
   - Evaluated model performance using MAE and R<sup>2</sup>.
5. **Post-Hoc Analyses**:
   - Conducted permutation-based variable importance analysis using `DALEXtra`.
   - Generated plots to examine model residuals using `DALEX` and `ggplot2`.

## Key Findings

- The XGBoost model achieved the best performance of the three models (MAE = 634.38, R<sup>2</sup> = .002). That being said, these metrics indicate that the model only marginally outperforms the baseline model of predicting the mean and that the accuracy is rather poor.
- Permutation-based feature importance analysis revealed that features such as `annual_income`, `health_score`, and `insurance_duration` were key predictors of `premium_amount`.
- Visualization of the model residuals suggested several areas for improvement. Specifically, the model appeared to have a limited range for predictions and displayed a systematic tendency to under/overpredict in certain value ranges.

## Limitations and Future Directions

- **Limitations**:
  -  In order to use my personal computer, only a subsample of the dataset was utilized. This may have affected the performance and tuning of the model and may limit the generalizability of the final model to the full dataset.
  -  All three models showed only marginal improvement over the baseline, suggesting potential feature limitations.
  -  Analysis of the residuals indicated some systematic errors with the predictions made by thye final model. It is possible that these could be addressed using more advanced techniques.
- **Future Directions**:
  -  Explore ensemble stacking in order to leverage the strengths of multiple different models.
  -  Investigate additional feature engineering methods to maximize performance.
  -  Use cloud computing resources for model training.   

## Repository Structure

- `data/`: Contains web links to the dataset and related documentation.
- `analysis/`: Includes analysis scripts (`.qmd`) and rendered outputs (`.html`).

## Technical Skills Demonstrated

- **Data Wrangling and Preprocessing**: Used `dplyr`, `janitor`, and `recipes` to clean, transform, and engineer features.
- **Exploratory Data Analysis**: Used `skimr`, `stats`, and `ggplot2` to explore the data through summary statistics and visualizations.
- **Machine Learning**: Developed, tuned, and tested several ML models using the `tidymodels` workflow.
- **Parallel Processing**: Leveraged `doParallel` to speed up computation.
- **Model Evaluation**: Used `tidymodels` and `DALEXtra` to evaluate models using loss functions and feature importance analysis.
- **Quarto**: For report generation and sharing insights.

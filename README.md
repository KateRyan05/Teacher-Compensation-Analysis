# Early Childcare Workforce Wage Analysis

## Project Overview: 
This project analyzes ICPSR Study 27491 - National Survey of Early Care and Education (NSECE), Wave 9 data to investigate wage determinants among childcare workers in the United States with a focus on the relationship between depression scores, education, experience, and hourly wages. The workflow is organization into numbers notebooks that run sequentially from data extraction through modeling and model interpretation. 
Author: Kate Ryan 
Course: QSS 45

## Research Question
To what extent do institutional factors predict early childhood teacher compensation beyond individual qualifications? 

## Directory Layout
```text
wage_project/
├── code/ 
│ ├── 00_pull.ipynb 
│ ├── 01_merge.ipynb 
│ ├── 02_eda.ipynb 
│ ├── 03_model.ipynb 
│ └── 04_shap.ipynb 
│ 
├── data/ 
│ ├── 37941-0005-Data.dta 
│ ├── raw_selected.csv 
│ └── analysis_clean.csv 
│ 
├── output/ 
│ ├── figures 
│ ├── model results 
│ └── SHAP visualizations 
│ 
└── README.md
```
---

##  Notebook Workflow
### `00_pull.ipynb` 

### Input
- data/37941-0005-Data.dta
- ICPSR Wave 9 Stata dataset

### Function
- Reads the raw Stata dataset
- Select the variables required for analysis
- Renames variables using a variable mapping dictionary
- Converts negative missing-value codes to NaN
- Produces a reducted dataset for downstream analysis

### Output
- data/raw_selected.csv

### Key Functions
- load_stata()
- select_vars()

---

### `01_merge.ipynb` 

### Input
- data/raw_selected.csv
- Output from 00_pull.ipynb

### Function
- Loads the selected variables dataset
- Cleans and prepares the data for modeling
- Converts variables to approrpiate data types
- Encodes categorical variables
- Removes observations with missing target values
- Produces a model-ready dataset

### Output
- data/analysis_clean.csv

### Key Functions
- load_raw()
- clean_types()
- encode_categoricals()
- drop_missing_target()

---

### `02_eda.ipynb` 

### Input
- data/analysis_clean.csv
- Output from 01-merge.ipynb

### Function
- Performs exploratory data analysis
- Examines distributions of key variables
- Visualizes wage and depression measures
- Evaluates correlations among predictors
- Creates bivariate visualizations

### Output
- output/fig_wage_dist.png
- output/fig_log_wage.png
- output/fig_depression.png
- output/fig_education.png
- output/fig_hours.png
- output/fig_wage_by_educ.png
- output/fig_depression_vs_wage.png
- output/fig_correlation.png

### Key Functions
- load_clean()
- save_fig()
- plot_heat_map()
- plot_wage_distribution()
- plot_log_wage()
- plot_depression()
- plot_education()
- plot_hours()
- plot_wage_by_education()
- plot_depression_vs_wage()

---

### `03_model.ipynb` 

### Input
- data/analysis_clean.csv
- Output from 01-merge.ipynb

### Function
- Builds feature matrix and target variable
- Splits data into training and testing sets
- Trains multiple predictive models:
- OLS Regression
- Logistic Regression
- Gradient Boosting
- LightGBM
- XGBoost
- CatBoost
- Compares model performance using test and cross-validation metrics
- Visualizes OLS coefficient estimates

### Output
- output/model_scores.csv
- output/fig_r2_comparison.png
- output/fig_ols_forest.png

### Key Functions
- load_clean()
- load_clean()
- prep_model_data()
- save_fig()
- fit_ols()
- fit_gb()
- fit_lgbm()
- fit_xgb()
- fit_cat()
- fit_logit()
- plot_ols_forest()
- plot_r2_comparison()

---

### `04_shap.ipynb` 

### Input
- data/analysis_clean.csv
- Trained tree-based models from the modeling window

### Function
- Computes SHAP values for model interpretation
- Evaluates feature importance
- Produces global explanation visualizations
- Compares feature contributions across tree-based models

### Output
- output/fig_shap_xgb_bar.png
- output/fig_shap_xgb_beeswarm.png
- output/fig_shap_cat_bar.png
- output/fig_shap_cat_beeswarm.png
- output/fig_shap_lgbm_bar.png
- output/fig_shap_lgbm_beeswarm.png
- output/fig_shap_gb_bar.png

### Key Functions
- load_and_prep()
- refit_models()
- save_fig()
- shap_bar()
- shap_beeswarm()

---

## Running the Project 
Run notebooks in the following order: 
1. 00_pull.ipynb
2. 01_merge.ipynb
3. 02_eda.ipynb
4. 03_model.ipynb
5. 04_shap.ipynb

The output of each notebook serves as the input to the next stage of the workflow.



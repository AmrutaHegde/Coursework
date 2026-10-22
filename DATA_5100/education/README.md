## Data analysis

**Question.** Is school performance, measured by the average ACT score, predicted by socioeconomic factors? The analysis also tests an added predictor, the charter status of the school.

**Steps taken**
1. Loaded the EdGap data (`EdGap_data.xlsx`) and the NCES school information file (`ccd_sch_029_1617_w_1a_11212017.csv`) and inspected them.
2. Selected the relevant columns, renamed them to lowercase snake_case, and cast the school ID to a common type.
3. Joined the two data sets on the school ID, set out-of-range values (negative ACT scores and negative lunch percentages) to missing, kept only high schools, checked for duplicates, and dropped schools without an ACT score.
4. Imputed the remaining missing values of the socioeconomic predictors with an iterative imputer and exported the clean data set.
5. Explored the clean data with a correlation matrix, pair plots and box plots to check relationships, overlap among the predictors, and outliers.
6. Fit single-input regression models (linear and quadratic) for each socioeconomic predictor, a multiple linear regression with all five predictors, and a reduced model with the significant predictors. Checked the models with R-squared, mean absolute error, residual plots, F-tests (ANOVA) and variance inflation factors, and standardized the predictors to compare coefficients.
7. Added charter status as an extra predictor and tested whether it improves the model.

**Notebooks that perform the analysis (run in this order):**
1. `education_data_preparation.ipynb`: loading, cleaning, joining, imputation and export
2. `education_eda.ipynb`: exploratory data analysis
3. `education_modeling.ipynb`: modeling, evaluation and conclusion

**Clean data file:** `education_clean.csv`

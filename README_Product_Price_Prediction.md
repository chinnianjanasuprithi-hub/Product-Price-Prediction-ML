# Product Price Prediction and Comparison Using Machine Learning

## 1. Project Overview

This project implements a machine-learning-based approach for **product
price prediction and comparison across online shopping platforms**.

The selected dataset contains dated product prices collected from
multiple online platforms. The original Excel file is organized as a
wide table, where products are rows and online platforms are columns.
For machine-learning implementation, the data is transformed into a
supervised-learning format in which each row represents one observed
**product-platform-date price**.

The project evaluates multiple regression models and compares the
obtained results with a published product-price-prediction study.

------------------------------------------------------------------------

## 2. Student Details

-   **Student Name:** Chinni Anjana Suprithi
-   **USN:** 23BTRCO053
-   **Department:** Computer Science and Engineering
-   **Academic Year:** 2026--2027

------------------------------------------------------------------------

## 3. Problem Statement

Online product prices can vary across platforms and change over time. A
machine-learning model can use historical product prices, platform
information, date-related features, and competitor prices to estimate
the price of a product.

The problem addressed in this project is:

> **Product Price Prediction and Comparison Using Machine Learning**

The implementation treats price prediction as a **regression problem**,
where the target variable is the observed product price.

------------------------------------------------------------------------

## 4. Objectives

The main objectives are:

1.  Collect and prepare the selected product-price dataset.
2.  Clean and transform the original Excel data into an ML-ready
    dataset.
3.  Perform exploratory data analysis.
4.  Engineer historical, date-based, product, platform, and
    competitor-price features.
5.  Train and evaluate multiple machine-learning regression models.
6.  Compare models using MAE, RMSE, and R².
7.  Implement a prediction-fusion/stacking approach inspired by the
    selected research paper.
8.  Compare the project results with the results reported in the
    selected research paper.
9.  Evaluate the models using both a random split and a chronological
    split.
10. Document the complete implementation so that it can be reproduced.

------------------------------------------------------------------------

## 5. Dataset

### Dataset Source

**Kaggle dataset:**
`moinak05/comparing-product-price-on-various-online-platform`

**File:** `product prices.xlsx`

The dataset contains dated prices for products across multiple online
platforms.

### Dataset Summary

The processed dataset contains:

-   **12 products**
-   **10 online platforms**
-   **39 dates**
-   **3,237 observed price records**
-   Historical product-platform price observations

The original Excel file uses a two-row header. The notebook cleans this
structure before performing machine-learning preprocessing.

------------------------------------------------------------------------

## 6. Data Preprocessing

The notebook performs the following preprocessing steps:

### 6.1 Excel Header Cleaning

The source Excel sheet contains:

-   Date
-   Serial number
-   Product name
-   Platform price columns

The two-row platform header is converted into a single clean header.

### 6.2 Date Processing

Dates are converted to Pandas datetime values.

The source sheet records the date once for a block of products, so
missing date cells are forward-filled.

### 6.3 Price Conversion

Platform price values are converted to numeric values.

Non-numeric values such as `-` are treated as missing values rather than
as zero prices.

### 6.4 Long-Format Transformation

The original wide table is converted into a long ML table.

Each row represents:

`Date + Product + Platform + Price`

This makes the dataset suitable for supervised regression.

### 6.5 Missing Values

Missing platform prices are treated as unavailable observations.

They are not converted into zero because zero would incorrectly
represent a free product.

------------------------------------------------------------------------

## 7. Feature Engineering

The following features are created.

### Categorical Features

-   Product Name
-   Platform

### Date Features

-   Date index
-   Day of week
-   Month
-   Day of month

### Historical Feature

-   Previous price for the same product-platform pair

The previous price is generated using the earlier observation only.

### Competitor Features

For the same product and date, the notebook calculates:

-   Competitor mean price
-   Competitor median price
-   Competitor minimum price
-   Competitor maximum price
-   Number of available competitor prices

The target platform's own price is excluded from these competitor
statistics.

------------------------------------------------------------------------

## 8. Exploratory Data Analysis

The notebook performs basic exploratory analysis including:

-   Missing-value inspection
-   Descriptive statistics
-   Platform-wise price statistics
-   Average observed price by platform
-   Price visualization

The platform summary includes:

-   Number of observations
-   Average price
-   Minimum price
-   Maximum price

------------------------------------------------------------------------

## 9. Machine Learning Models

The following regression models are implemented:

### 9.1 Linear Regression

Used as a simple baseline regression model.

### 9.2 Decision Tree Regressor

Uses decision rules to model nonlinear relationships between the input
features and product price.

### 9.3 Random Forest Regressor

Combines multiple decision trees and is suitable for nonlinear
structured/tabular data.

### 9.4 Gradient Boosting Regressor

Builds an ensemble of trees sequentially to reduce prediction error.

### 9.5 Support Vector Regression

SVR is included as another regression approach and uses feature scaling.

### 9.6 Prediction Fusion / Stacking

A stacking model is implemented using:

-   Linear Regression
-   Random Forest
-   Gradient Boosting

Their predictions are combined through a Random Forest meta-model.

This is inspired by the prediction-fusion approach used in the selected
reference study.

------------------------------------------------------------------------

## 10. Evaluation Strategy

Two evaluation settings are used.

### 10.1 Random 70/30 Split

The dataset is divided into:

-   70% training
-   30% testing

`random_state = 42`

This follows the split style reported in the selected reference study
and is therefore used for the primary methodological comparison.

### 10.2 Chronological 80/20 Split

The data is split according to time:

-   First 80% of dates → training
-   Final 20% of dates → testing

This provides a more realistic check for future-price prediction because
later observations are not mixed into the training set.

------------------------------------------------------------------------

## 11. Evaluation Metrics

### MAE --- Mean Absolute Error

Measures the average absolute difference between actual and predicted
prices.

Lower MAE indicates smaller average prediction errors.

### RMSE --- Root Mean Squared Error

Measures prediction error while giving greater weight to larger errors.

Lower RMSE indicates better prediction performance.

### R² --- Coefficient of Determination

Measures how much of the variation in the target price is explained by
the model.

Higher R² generally indicates a better fit.

------------------------------------------------------------------------

## 12. Results

### Random 70/30 Evaluation

The notebook produced the following results:

  Model                                 MAE     RMSE       R²
  --------------------------------- ------- -------- --------
  Linear Regression                   8.584   11.544   0.9947
  Decision Tree                       2.578    5.828   0.9986
  Random Forest                       2.169    4.759   0.9991
  Gradient Boosting                   2.895    4.811   0.9991
  SVR                                 3.979    6.074   0.9985
  Prediction Fusion (Stacking RF)     2.481    4.973   0.9990

These values are produced from the selected dataset and the
implementation in the notebook.

------------------------------------------------------------------------

## 13. Comparison With the Selected Research Paper

The selected reference study is:

> Zhu, D., Chen, X., & Gan, Y. (2022). *A Multi-Model Output Fusion
> Strategy Based on Various Machine Learning Techniques for Product
> Price Prediction*. Journal of Electronic & Information Systems, 4(1),
> 42--51. DOI: 10.30564/jeis.v4i1.7566.

The paper reports:

  Model                 Reference MAE   Reference RMSE   Reference R²
  ------------------- --------------- ---------------- --------------
  Linear Regression           153.644          191.737       0.999584
  Decision Tree               232.261          291.451       0.999039
  Random Forest               173.225          215.311       0.999476
  Gradient Boosting           165.275          204.514       0.999527
  SVR                        7777.552         9686.280      -0.061316
  Prediction Fusion           149.665          189.099       0.999881

### Important comparison note

The reference paper and this project do **not** use the same dataset.

The published study uses a **1,000-row laptop-price dataset**, while
this project uses the selected multi-platform product-price dataset.

Therefore, the numerical results should be treated as a **methodological
comparison**, not as a direct replication of the paper.

The project follows the same general model families and evaluation
metrics so that the behavior of the approaches can be compared.

------------------------------------------------------------------------

## 14. Results Interpretation

The project results show that the tree-based models and the
prediction-fusion approach achieve very high R² values on the random
70/30 split.

Random Forest produced an RMSE of **4.759** and an R² of **0.9991** in
this implementation.

Gradient Boosting produced an RMSE of **4.811** and an R² of **0.9991**.

The stacking prediction-fusion model produced an RMSE of **4.973** and
an R² of **0.9990**.

The Linear Regression model provided a useful baseline with an RMSE of
**11.544** and an R² of **0.9947**.

These results are specific to this dataset and feature construction.
They should not be interpreted as universal performance values for
product-price prediction.

------------------------------------------------------------------------

## 15. Reproducibility

The notebook uses:

`random_state = 42`

This makes the randomized model experiments reproducible.

The notebook also ensures that:

-   Missing prices are not treated as zero.
-   The target platform is excluded from same-day competitor statistics.
-   Historical previous-price features use earlier observations.
-   Unknown categorical values can be handled through one-hot encoding.
-   Numerical missing values are imputed using the training pipeline.
-   Both random and chronological evaluation are performed.

------------------------------------------------------------------------

## 16. Project Files

The recommended repository structure is:

``` text
Product-Price-Prediction/
│
├── product prices.xlsx
├── Product_Price_Prediction_ML_Notebook_FINAL.ipynb
├── README.md
└── Literature_Review.pdf
```

### File descriptions

**`product prices.xlsx`**

The selected Kaggle dataset used for the project.

**`Product_Price_Prediction_ML_Notebook_FINAL.ipynb`**

Contains the complete Python implementation, preprocessing, feature
engineering, model training, evaluation, comparison, and visualizations.

**`README.md`**

Provides project documentation, methodology, results, and instructions.

**`Literature_Review.pdf`**

Contains the dataset collection and literature-review component of the
project.

------------------------------------------------------------------------

## 17. How to Run

### Option 1 --- Google Colab

1.  Open Google Colab.
2.  Upload `Product_Price_Prediction_ML_Notebook_FINAL.ipynb`.
3.  Upload `product prices.xlsx` if it is not available through
    KaggleHub.
4.  Run the notebook cells from top to bottom.
5.  Check the generated tables and graphs.

### Option 2 --- Kaggle Notebook

1.  Create a Kaggle Notebook.
2.  Add the selected dataset as an input.
3.  Upload/import the notebook.
4.  Run the cells from top to bottom.
5.  Save the completed notebook with the generated results.

### Option 3 --- Local Jupyter

Install the required packages:

``` bash
pip install pandas numpy matplotlib scikit-learn openpyxl kagglehub
```

Then open the notebook using Jupyter Notebook or JupyterLab and run all
cells.

------------------------------------------------------------------------

## 18. Expected Output

After successful execution, the notebook produces:

-   Dataset information
-   Data-cleaning results
-   Missing-value analysis
-   Platform price statistics
-   Price visualization
-   Random 70/30 model comparison
-   Chronological 80/20 model comparison
-   Prediction-fusion results
-   Comparison with the reference paper
-   RMSE and R² graphs
-   Actual-vs-predicted price visualization
-   Final findings

------------------------------------------------------------------------

## 19. Limitations

1.  The dataset covers a limited historical period.
2.  Some platform-product combinations have missing prices.
3.  The reference paper uses a different dataset, so direct numerical
    replication is not possible.
4.  Random train/test splitting can give optimistic results for
    time-dependent data.
5.  The chronological evaluation is therefore included as an additional
    future-price validation.
6.  The project predicts observed prices; it does not optimize prices or
    automatically determine the best selling price.
7.  Results depend on the available historical data and selected
    features.

------------------------------------------------------------------------

## 20. Future Scope

Future improvements can include:

-   Longer historical price collection
-   Real-time price collection through APIs
-   More online platforms
-   Price-change prediction
-   Time-series forecasting models
-   XGBoost and LightGBM comparison
-   LSTM-based sequential price forecasting
-   Hyperparameter optimization
-   Real-time price monitoring dashboard
-   Price-alert system
-   Explainable AI for price predictions

------------------------------------------------------------------------

## 21. Conclusion

This project implements a complete machine-learning workflow for product
price prediction using a multi-platform historical price dataset.

The workflow includes data cleaning, restructuring, feature engineering,
exploratory analysis, regression modeling, evaluation, and comparison
with a published product-price-prediction study.

Multiple models are evaluated using MAE, RMSE, and R². A
prediction-fusion/stacking model is also implemented to reflect the main
methodological idea of the selected reference paper.

The final notebook provides a reproducible implementation that can be
used for the project submission and further extended into a real-time
product-price monitoring and prediction system.

------------------------------------------------------------------------

## 22. Reference

Zhu, D., Chen, X., & Gan, Y. (2022). *A Multi-Model Output Fusion
Strategy Based on Various Machine Learning Techniques for Product Price
Prediction*. Journal of Electronic & Information Systems, 4(1), 42--51.
DOI: **10.30564/jeis.v4i1.7566**.

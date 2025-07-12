-----

# Walmart Product Price Prediction

This repository contains a machine learning project focused on predicting current product prices from Walmart's grocery data. The project utilizes various data analysis, visualization, preprocessing, and machine learning techniques to build and evaluate predictive models.

-----

## Table of Contents

  - Installation
  - Dataset
  - Exploratory Data Analysis (EDA)
  - Data Preprocessing
  - Model Training and Evaluation
  - Usage
  - Dependencies
  - License
  - Contact

-----

## Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/walmart-price-prediction.git
    cd walmart-price-prediction
    ```

2.  **Create a virtual environment (recommended):**

    ```bash
    python -m venv env
    source env/bin/activate  # On Windows, use `env\Scripts\activate`
    ```

3.  **Install the required packages:**

    ```bash
    pip install -r requirements.txt
    ```

    *Note: A `requirements.txt` file is not provided in the snippet, but it's good practice to create one with the listed libraries.*

-----

## Dataset

The dataset used in this project is `WMT_Grocery_202209.csv`, which contains product prices and sizes from Walmart Grocery as of September 2022. It includes features such as:

  * `SHIPPING_LOCATION`
  * `DEPARTMENT`
  * `CATEGORY`
  * `SUBCATEGORY`
  * `BREADCRUMBS`
  * `SKU`
  * `PRODUCT_URL`
  * `PRODUCT_NAME`
  * `BRAND`
  * `PRICE_RETAIL`
  * `PRICE_CURRENT`
  * `PRODUCT_SIZE`
  * `PROMOTION`
  * `RunDate`
  * `tid`

The dataset can be found in the `../input/product-prices-and-sizes-from-walmart-grocery/` directory in a Kaggle environment.

-----

## Exploratory Data Analysis (EDA)

The EDA phase involved:

  * Loading the dataset and initial inspection (`df.head()`, `df.info()`).
  * Checking for and handling duplicate rows.
  * Identifying and analyzing null values in columns like `SUBCATEGORY`, `BRAND`, `PRODUCT_SIZE`, and `PROMOTION`. The `PROMOTION` column was dropped due to all null values.
  * Visualizing the distribution of numerical features using histograms (`draw_hist`), box plots (`draw_boxplot`), and distribution plots (`draw_dist`).
  * Analyzing the distribution of categorical features such as `DEPARTMENT`, `BRAND`, `SUBCATEGORY`, and `SHIPPING_LOCATION` using pie charts and bar plots.
  * Extracting `day`, `month`, and `year` from the `RunDate` column.
  * Generating a pair plot to visualize relationships between numerical variables.
  * Calculating the correlation matrix and identifying features most correlated with `PRICE_CURRENT`. `SKU` was dropped due to low correlation.

-----

## Data Preprocessing

The following preprocessing steps were performed:

  * Converted `SUBCATEGORY` to lowercase for consistency.
  * Transformed `PRODUCT_SIZE` from object to numeric, coercing errors.
  * Applied log transformation to `PRICE_RETAIL` and `PRODUCT_SIZE` to normalize their distributions.
  * Dropped the `index`, `PROMOTION`, `SKU`, `PRODUCT_URL`, `tid`, `day`, `month`, `year`, and `Date` columns.
  * Cleaned the `PRODUCT_NAME` column by splitting and retaining only the first part.
  * Handled missing values:
      * `PRODUCT_SIZE` nulls were filled with the mean of the column.
      * `SUBCATEGORY` nulls were filled with the mode of the column.
  * Feature Engineering:
      * Filtered `DEPARTMENT` to include only the top 10 most frequent categories.
      * Filtered `CATEGORY` to include only the top 70 most frequent categories.
      * Filtered `BREADCRUMBS` to include only the top 70 most frequent entries.
      * Filtered `BRAND` to include only the top 2000 most frequent brands.
      * Filtered `SUBCATEGORY` to include only the top 60 most frequent subcategories.
      * Filtered `PRODUCT_NAME` to include only the top 14000 most frequent product names.
  * Encoded categorical features (`DEPARTMENT`, `CATEGORY`, `SUBCATEGORY`, `BREADCRUMBS`, `PRODUCT_NAME`, `BRAND`) using `OrdinalEncoder`.

-----

## Model Training and Evaluation

1.  **Splitting the data:** The dataset was split into training and testing sets with a 70/30 ratio, respectively, using `train_test_split`.

      * Features ($X$): All preprocessed columns except `PRICE_CURRENT`.
      * Target ($y$): `PRICE_CURRENT`.

2.  **Model Training:**

      * **Linear Regression:**

          * Trained a `LinearRegression` model on the training data.
          * Made predictions on the test set.
          * Evaluated performance using Mean Squared Error (MSE), Mean Absolute Error (MAE), and R-squared ($R^2$) score.

        <!-- end list -->

        ```
        MSE 3.8733297734115455
        MAE 1.1556481773565348
        R2 Score 0.7451419967793593
        ```

      * **Random Forest Regressor:**

          * Trained a `RandomForestRegressor` model on the training data.
          * Made predictions on the test set.
          * Evaluated performance using Mean Squared Error (MSE), Mean Absolute Error (MAE), and R-squared ($R^2$) score.

        <!-- end list -->

        ```
        MSE 0.007172832289304745
        MAE 0.002409002769809072
        R2 Score 0.9995280407758623
        ```

-----

## Usage

To run this project:

1.  Ensure you have the required dependencies installed.
2.  Place the `WMT_Grocery_202209.csv` file in the appropriate input directory or update the `pd.read_csv` path.
3.  Execute the Python script containing the code.

-----

## Dependencies

  * Python 3
  * `numpy`
  * `pandas`
  * `matplotlib`
  * `seaborn`
  * `scipy`
  * `sklearn` (specifically `OrdinalEncoder`, `train_test_split`, `LinearRegression`, `mean_absolute_error`, `mean_squared_error`, `r2_score`, `RandomForestRegressor`)

-----

## License

This project is open-source and available under the MIT License.

-----

## Contact

For any questions or suggestions, please contact \[Your Name/Email/GitHub Profile].

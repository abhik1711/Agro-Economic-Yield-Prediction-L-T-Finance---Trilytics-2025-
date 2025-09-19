# Farmer Income Prediction for L\&T Finance

## 🚀 Overview

This repository contains the solution for the **LTF Challenge on Farmer Income Prediction**. The primary goal of this project is to predict the income of farmers in India to help L\&T Finance (LTF) improve their credit assessment process for the unbanked agricultural population. By leveraging a rich dataset encompassing demographic, landholding, and climatic data, this project employs a sophisticated machine learning pipeline to generate accurate income predictions.

The solution is implemented in a Jupyter Notebook (`Trilytics.ipynb`) and uses a stacked ensemble of multiple gradient boosting and tree-based models to achieve high accuracy.

-----

## 🎯 Problem Statement

Access to credit is a significant challenge for individuals in the farming sector due to a lack of sufficient credit history. This often leads to exploitation by untrustworthy lenders. L\&T Finance aims to address this by using alternative data sources to assess the creditworthiness of farmers. This challenge seeks to develop a model that can accurately predict farmer income, thereby minimizing the rejection of loan applications for deserving individuals.

-----

## 📊 Dataset

The dataset provided for this challenge includes the following files:

  * **Training Data**: Contains farmer demography, landholding information, local climatic profiles, and indicators of the local living index. The target variable is `Target_Variable/Total Income`.
  * **Test Data**: A similar dataset for which income predictions are to be made.
  * **Data Dictionary**: Provides detailed descriptions of all variables in the datasets.
  * **Sample Submission File**: A sample prediction file for reference.

The project also uses the `Trilytics Dataset.csv` which contains the final predictions.

-----

## 🛠️ Methodology

The solution follows a structured machine learning pipeline, as detailed in the `Trilytics.ipynb` notebook.

### 1\. Data Loading and Preparation

  * The training and test datasets are loaded from the provided Excel file (`LTF Challenge data with dictionary.xlsx`).
  * A preliminary analysis is performed to understand the structure of the data, including the number of features and data types.

### 2\. Data Cleaning and Preprocessing

  * **Handling Missing Values**: Missing values in numerical columns are imputed using the median, while missing values in categorical columns are filled with the string "Unknown".
  * **Categorical Feature Encoding**:
      * Categorical features with 20 or fewer unique values are encoded using **Label Encoding**.
      * High-cardinality categorical features (more than 20 unique values) are encoded using **Frequency Encoding** to manage the dimensionality of the data.
  * **Target Variable Transformation**: The target variable, `Total Income`, is log-transformed (`log_income`) to handle its skewness and stabilize variance, which often improves model performance.

### 3\. Feature Engineering

Several new features were created to enhance the predictive power of the models:

  * `income_per_hectare`: Ratio of total income to the total land for agriculture.
  * `agri_income_ratio`: The proportion of agricultural income to the total income.
  * `land_productivity`: A measure of income generated per unit of land.
  * `agro_econ_score`: An aggregated score based on agricultural scores, socio-economic parameters, and night light index.
  * `access_score`: A composite score representing a farmer's access to markets and transportation, based on proximity to mandis (markets), railway stations, and road density.

### 4\. Modeling and Stacking

A stacked ensemble approach was used to combine the predictions of multiple models, leading to a more robust and accurate final prediction. The following base models were trained:

  * **LightGBM Regressor**
  * **XGBoost Regressor**
  * **CatBoost Regressor**
  * **Random Forest Regressor**
  * **Extra Trees Regressor**

The predictions from these base models were then used as input features for a **Ridge Regressor** meta-model, which produced the final income predictions.

-----

## 📈 Results

The stacked ensemble model demonstrated strong performance on the validation set, achieving:

  * **Mean Absolute Percentage Error (MAPE)**: **0.68%**
  * **R² Score**: **0.9968**
  * **Accuracy within 10% error**: **99.55%**

The final predictions on the test set are saved in the `ltf_final_predictions_stacked_extended.csv` file.

-----

## ⚙️ How to Run

To reproduce the results, follow these steps:

1.  Ensure you have a Python environment with the required dependencies installed (see below).
2.  Place the `LTF Challenge data with dictionary.xlsx` file in the same directory as the `Trilytics.ipynb` notebook.
3.  Open and run the `Trilytics.ipynb` notebook in a Jupyter environment like Jupyter Lab or Google Colab.

The notebook will handle all the steps from data loading to generating the final prediction file.

-----

## 📚 Dependencies

The following Python libraries are required to run the code:

```
pandas
numpy
scikit-learn
lightgbm
xgboost
catboost
matplotlib
seaborn
openpyxl
```

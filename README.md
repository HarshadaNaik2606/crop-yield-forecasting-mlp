🌾 Crop Yield Forecasting using Multilayer Perceptron (MLP)
1) Project Overview

This project focuses on forecasting crop yield one year ahead using a Multilayer Perceptron (MLP) regression model. The goal is to predict future crop yields at the country–year level by learning relationships between historical environmental conditions and agricultural outcomes.

The model integrates data from multiple sources, including soil conditions, climate variables, vegetation activity, and land cover, along with contextual categorical information such as country and crop type. A time-based validation strategy is used to closely simulate a real-world forecasting scenario.

2) Data & Target Construction

The target variable is crop yield for a given country and year, sourced from the Yield_and_Production_data.csv file.

Only rows where element == "Yield" were retained

Production-related records were removed

Yield values were taken from the value column

The target was shifted by one year so that features from year t predict yield in year t+1

All data was aggregated to the country–year level to ensure alignment between input features and the prediction target.

3) Features (Examples)

The model uses a combination of numerical environmental variables and categorical context features.

Numerical Features (Annual Averages)

Rainfall and Snowfall

Soil Moisture (0–10 cm, 10–40 cm, 40–100 cm, 100–200 cm)

Soil Temperature (multiple depths)

Evaporation and Soil Water Loss (ESoil)

Terrestrial Water Storage (TWS)

Vegetation Activity (TVeg)

Dominant Land Cover Percentage (land_cover_max)

Monthly measurements were converted into annual averages to reduce noise and improve stability.

Categorical Features

Country (One-Hot Encoded)

Crop Type / Item (One-Hot Encoded)

These features allow the model to capture country-specific and crop-specific yield patterns.

4) Preprocessing

Several preprocessing steps were applied to prepare the data for modelling:

Filtered yield data to retain only relevant records

Computed annual averages from monthly environmental variables

Aggregated spatial grid data to country-year level using nearest country centroid matching

Merged all datasets using country and year as keys

Handled missing values using forward fill, backward fill, and row removal where necessary

Removed duplicate records

Applied One-Hot Encoding to categorical variables

Standardized numerical features using StandardScaler

Used a chronological train–validation split (train < 2021, validate on 2021)

This pipeline ensured data consistency and prevented information leakage.

5) Model

A Multilayer Perceptron (MLP) was used for regression due to its ability to model complex non-linear relationships.

Architecture

Input Layer: All numerical and encoded categorical features

Hidden Layer 1: 64 neurons, ReLU activation

Hidden Layer 2: 32 neurons, ReLU activation

Output Layer: 1 neuron with ReLU activation to ensure non-negative predictions

The architecture was intentionally kept simple to balance learning capacity and generalization.

6) Training & Hyperparameters

Optimizer: Adam

Learning Rate: 0.0001

Loss Function: Mean Squared Error (MSE)

Batch Size: 32

Epochs: 10

Training was monitored using validation loss, and the model weights corresponding to the best validation performance were selected. This acted as a manual early stopping mechanism to reduce overfitting.

7) Evaluation

Model performance was evaluated on unseen data from the year 2021 using standard regression metrics.

Metric	Value
R² Score	0.7596
RMSE	7441.73
MAE	5715.68

The R² score indicates that approximately 76% of the variance in crop yield is explained by the model

RMSE and MAE reflect reasonably low prediction errors at the country-year level

Overall, the results demonstrate that the model generalizes well and is effective for real-world crop yield forecasting.

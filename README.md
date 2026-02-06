# 🌾 Crop Yield Forecasting using Multilayer Perceptron (MLP)

## 1) Project Overview

This project focuses on forecasting crop yield one year ahead using a Multilayer Perceptron (MLP) regression model. The objective is to predict future crop yields at the country–year level by learning relationships between historical environmental conditions and agricultural outcomes. The model integrates climate, soil, vegetation, and land cover data along with categorical context such as country and crop type. A time-based validation strategy is used to simulate a real-world forecasting scenario.

---

## 2) Data & Target Construction

The target variable is crop yield for a given country and year, sourced from the `Yield_and_Production_data.csv` file.

- Only records where `element == "Yield"` were retained  
- Production-related entries were removed  
- Yield values were taken from the `value` column  
- The target was shifted by one year so that features from year *t* predict yield in year *t+1*

All datasets were aggregated to the country–year level to ensure alignment between features and the prediction target.

---

## 3) Features (Examples)

### Numerical Features (Annual Averages)
- Rainfall and Snowfall  
- Soil Moisture (0–10 cm, 10–40 cm, 40–100 cm, 100–200 cm)  
- Soil Temperature (multiple depths)  
- Evaporation and Soil Water Loss (ESoil)  
- Terrestrial Water Storage (TWS)  
- Vegetation Activity (TVeg)  
- Dominant Land Cover Percentage (`land_cover_max`)  

Monthly measurements were converted into annual averages to reduce noise and improve model stability.

### Categorical Features
- Country (One-Hot Encoded)  
- Crop Type / Item (One-Hot Encoded)  

---

## 4) Preprocessing

The following preprocessing steps were applied:

- Filtered yield data to retain only relevant records  
- Converted monthly environmental variables into annual averages  
- Aggregated spatial grid-level data to the country-year level using nearest centroid matching  
- Merged all datasets using country and year as keys  
- Handled missing values using forward fill, backward fill, and row removal  
- Removed duplicate entries  
- Applied One-Hot Encoding to categorical variables  
- Standardized numerical features using `StandardScaler`  
- Used a chronological train–validation split (training data before 2021, validation on 2021)

---

## 5) Model

A Multilayer Perceptron (MLP) neural network was used for regression.

- Input Layer: Numerical and encoded categorical features  
- Hidden Layer 1: 64 neurons with ReLU activation  
- Hidden Layer 2: 32 neurons with ReLU activation  
- Output Layer: 1 neuron with ReLU activation to ensure non-negative yield predictions  

The architecture was kept simple to balance learning capacity and generalization.

---

## 6) Training & Hyperparameters

- Optimizer: Adam  
- Learning Rate: 0.0001  
- Loss Function: Mean Squared Error (MSE)  
- Batch Size: 32  
- Epochs: 10  

Validation loss was monitored during training, and the model with the best validation performance was selected to reduce overfitting.

---

## 7) Evaluation

The model was evaluated on unseen data from the year 2021 using standard regression metrics.

| Metric | Value |
|------|------|
| R² Score | 0.7596 |
| RMSE | 7441.73 |
| MAE | 5715.68 |

The results indicate that the model explains approximately 76% of the variance in crop yield and demonstrates strong generalization for future yield forecasting tasks.

---

### Data Availability

Due to dataset size, raw data files are not included in this repository.  
Please download the datasets separately and update the data directory path in the notebook before running the code.

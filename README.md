# ⚡ Time Series Forecasting of Hourly Energy Consumption

This repository contains an **end-to-end time series forecasting project** for **hourly electricity consumption**, covering the full pipeline from **exploratory data analysis** to **classical and deep learning models**.

The objective of this project is to compare **traditional statistical approaches** with **modern deep learning methods** under a **realistic and leakage-free forecasting setup**.

---

## 📌 Project Overview

The project follows a structured workflow:

1. Exploratory Data Analysis (EDA)
2. Feature Engineering
3. Baseline Model: SARIMAX
4. Deep Learning Model: Temporal Fusion Transformer (TFT)
5. Model Evaluation and Comparison

All experiments are conducted on **hourly energy consumption data** enriched with **calendar, lagged, rolling, and weather-related features**.

---

## 📂 Repository Structure

```
multivariate_energy_consumption_forecasting/
│
├── dataa
│    ├── LD2011_2014.txt
│    ├── electricity_features_hourly.csv   
│ 
├── notebooks
│    ├── EDA.ipynb
│    ├── feature_Eng.ipynb
│    ├── model_sarımax.ipynb
│    ├── model_tft2.ipynb
│    ├── electricity_features_hourly.csv
├── venv
├──.gitignore
└── README.md

```
---

## 🔍 Exploratory Data Analysis (EDA)

**Notebook:** `EDA.ipynb`

The EDA phase focuses on understanding the structure and behavior of the time series:

- Long-term trends and seasonal patterns
- Hourly, daily, and weekly consumption behavior
- Distribution analysis and anomaly detection
- Correlation between energy consumption and external variables

Key insights include strong **daily and weekly seasonality** and clear **hour-of-day consumption patterns**.

---

## 🛠️ Feature Engineering

**Notebook:** `feature_Eng.ipynb`

Feature engineering is designed to enrich the dataset while preventing data leakage.

### Engineered Features

**Temporal & Calendar Features**
- Hour of day
- Day of week
- Month
- Weekend indicator
- Holiday indicator

**Cyclical Encoding**
- `hour_sin`, `hour_cos`
- `month_sin`, `month_cos`

**Lag Features (Leakage-Free)**
- `lag_1h`
- `lag_24h`
- `lag_168h`

**Rolling Statistics (Leakage-Free)**
- `rolling_mean_24h`
- `rolling_mean_7d`

> Lagged and rolling features are computed **after the temporal train-validation split** to prevent information leakage.

---

## 📊 Baseline Model – SARIMAX

**Notebook:** `model_sarımax.ipynb`

A **SARIMAX** model is implemented as a classical statistical baseline:

- Seasonal and non-seasonal components are included
- Exogenous variables are used
- Performance evaluated using MAE and RMSE

**Results:**
- MAE ≈ 75,000  
- RMSE ≈ 99,000  

This model serves as a reference point for comparison with deep learning methods.

---

## 🤖 Deep Learning Model – Temporal Fusion Transformer (TFT)

**Notebook:** `model_tft2.ipynb`

The **Temporal Fusion Transformer (TFT)** is implemented using the **Darts** library.

### Model Highlights
- Encoder–decoder architecture
- LSTM-based temporal modeling
- Multi-head attention mechanism
- Support for past and future covariates
- Early stopping for regularization

### Covariate Design
- **Past covariates:** weather variables, lag features, rolling statistics  
- **Future covariates:** calendar and cyclical features (known in advance)

### Final Performance
- **MAE:** 7,921  
- **RMSE:** 11,175  

This corresponds to approximately **6% relative error**, indicating strong performance for hourly energy consumption forecasting.

---

## 📈 Model Comparison

| Model   | MAE       | RMSE      |
|--------|-----------|-----------|
| SARIMAX | ~75,000   | ~99,000   |
| TFT     | **7,896** | **9,668** |

The TFT model significantly outperforms the classical baseline by capturing nonlinear relationships and complex temporal dependencies.

---

## 🧠 Key Takeaways

- Proper feature engineering is crucial for time series forecasting
- Preventing data leakage leads to more reliable evaluation
- Classical models have limitations in capturing nonlinear dynamics
- TFT provides a powerful and flexible framework for real-world forecasting problems

---

## 🚀 Future Work

- Probabilistic forecasting with quantile regression
- Walk-forward validation
- Attention weight visualization for interpretability
- Multi-horizon forecasting evaluation
- Deployment-ready inference pipeline

---

## 👤 Author

**Mert Genç**  
Computer Engineering  
Interests: Time Series Forecasting, Deep Learning, Data Science

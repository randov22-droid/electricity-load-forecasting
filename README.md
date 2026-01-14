# Electricity Load Forecasting (2019-2024)

## 📌 Project Overview
This project addresses the financial risk and operational instability caused by inaccurate load forecasts for utility companies. Using a dataset of ~46,000 hourly records, we developed a 24-hour forecasting pipeline to minimize power purchase costs and resource waste. We compared traditional statistical methods (SARIMA) against modern Machine Learning algorithms.

## 🚀 Key Results (Update with your final numbers)
- **Best Model:** [Insert e.g., XGBoost] 
- **Predictive Power:** Achieved an R² of [Insert e.g., 0.98], proving high reliability.
- **Benchmark:** Outperformed the Persistence (Lag-24) baseline by [Insert %] in RMSE.
- **Economic Impact:** Reduced average daily forecasting error by [Insert MWh] MWh.

## 📂 Project Structure
- `data/raw`: Original hourly electricity consumption and production dataset.
- `data/processed`: Cleaned dataset including engineered lag, rolling, and cyclic features.
- `notebooks`: `Electricity_Forecasting_Analysis.ipynb` - The complete end-to-end pipeline.
- `outputs`: 
    - `01-03`: EDA plots (Daily trends, seasonality, and time-series).
    - `04-06`: Statistical tables (Performance summary, Bias analysis).
    - `07-08`: Model visualizations (Leaderboard and Forecast vs. Actual charts).

## 🛠 Feature Engineering
To capture the complex patterns of the energy grid, we implemented:
- **Temporal:** Cyclic Sine/Cosine transformations for Hours and Months to capture periodic seasonality; Weekend indicators.
- **Auto-regressive:** Lags (1h, 24h, 168h) and Rolling Averages (3h, 24h) to capture momentum.
- **Seasonal:** One-hot encoded seasonal categories (Spring, Summer, Fall, Winter).

## 📊 Models Evaluated
- **Statistical:** SARIMA (Seasonal AutoRegressive Integrated Moving Average).
- **Linear:** Ridge/Linear Regression (Baseline).
- **Distance-Based:** k-Nearest Neighbors (k-NN).
- **Ensemble/Boosting:** Random Forest, XGBoost, and LightGBM.
- **Baseline:** Persistence Model (Lag-24) to measure true model value.
# ⚡ Electricity Load Forecasting: 24-Hour Horizon 

## 📌 Project Overview
Energy utility companies face significant financial risk due to the volatility of electricity demand. This project develops a **Multi-Output Forecasting Pipeline** designed to predict the next **24 hours of consumption simultaneously**. By moving beyond simple "next-hour" predictions, this project provides a tool for day-ahead market planning and grid stability.

## 🚀 Key Results
* **Top Performer:** [Insert Best Model]
* **Validation Strategy:** Used a 5-fold `TimeSeriesSplit` to ensure models generalize to future data without look-ahead bias.
* **Feature Drivers:** XGBoost importance scores identified [Insert Feature 1] and [Insert Feature 2] as the primary drivers of consumption.
* **Error Analysis:** Conducted a Bias Analysis to evaluate the Mean Error (MW) across the 24-hour horizon, comparing tree-based ensembles against statistical SARIMA.

## 🛠 Feature Engineering (The "Forecast-Legal" Approach)
To ensure the model is viable for real-world day-ahead planning, we implemented:
- **Cyclic Encoding:** Hour and Month transformed into **Sine/Cosine components** to map temporal continuity (recognizing that Hour 23 and Hour 00 are adjacent).
- **Lagged Consumption:** 24h, 48h, and 1-week (168h) lags to capture daily and weekly periodicity.
- **Shifted Rolling Statistics:** 24-hour and 7-day moving averages, shifted by 24 hours to prevent look-ahead bias.
- **Exogenous Drivers:** Lagged production data and seasonal dummy variables to account for varying weather patterns.

## 📊 Modeling Strategy
We utilized a **Multi-Output Regression** framework, where a single model predicts a vector of 24 values for the upcoming day.

| Category | Models Evaluated |
| :--- | :--- |
| **Baselines** | Persistence (Lag-24), Linear Regression |
| **Statistical** | SARIMA (Seasonal ARIMA) with $m=24$ |
| **Non-Linear** | k-Nearest Neighbors (k-NN) |
| **Tree-Ensembles** | Random Forest, XGBoost, LightGBM, HistGradientBoosting |

## 🧪 Evaluation Methodology
- **Time-Series Cross-Validation:** 5-fold expanding window validation (`TimeSeriesSplit`) to respect temporal order.
- **Bias Analysis:** Evaluated "Mean Bias" to determine if models consistently over-predict or under-predict (critical for balancing grid load).
- **Operational Metrics:** Calculated Daily Energy Uncertainty reduction in **MWh/day**.

## 📂 Project Structure
- `data/raw`: Original hourly electricity dataset.
- `data/processed`: Cleaned data with engineered features.
- `outputs/`: 
    - `04_model_performance_summary.csv`: The final model leaderboard.
    - `05_feature_importance.png`: Top drivers of demand according to XGBoost.
    - `08_final_forecast_comparison.png`: Visualizing the "Hero" plot (Best Model vs. S
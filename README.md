## 🧠 Technical Highlights & Feature Engineering

Initially, the dataset contained only two columns: `datetime` and `num_orders`. To enable the machine learning models to identify complex temporal patterns, I engineered a robust set of predictive features:

* **Time-based Extraction:** Extracted `hour` and `dayofweek` to capture daily and weekly seasonality (e.g., peak rush hours vs. weekends).
* **Lagged Features (`max_lag=24`):** Created historical lag features for the past 24 hours. This allowed the models to "look back" and identify autoregressive patterns (e.g., matching today's demand with yesterday's exact same hour).
* **Rolling Window Statistics:** Implemented a 24-hour moving average (`rolling_mean_size=24`). This smoothed out short-term random noise (anomalous spikes) and helped the neural network capture the overarching global trend of the demand.

## 🏆 Model Progression & Business Results

To prove the value of complex architectures, we established a strict baseline. Simply predicting the next hour based on the previous hour yielded a highly inefficient **RMSE of 58 orders**.

I led the technical evaluation of multiple architectures to beat the internal KPI of RMSE < 40:
1. **Linear Regression (RMSE = 40.5):** Captured basic trends but failed on non-linear spikes.
2. **CatBoost (RMSE = 39.5):** Successfully handled categorical data and daily seasonality.
3. **Random Forest (RMSE = 37.6):** Good performance but limited by its inability to extrapolate trends beyond historical data.
4. **Deep Neural Network (RMSE = 7.9):** The absolute winner. By utilizing early stopping and regularization, the NN successfully generalized the complex sequential patterns across all engineered lags and window features.

**Business Impact:** Reduced forecasting error by 86% compared to the baseline, providing a highly reliable tool for fleet management, surge pricing optimization, and reducing driver idle times.

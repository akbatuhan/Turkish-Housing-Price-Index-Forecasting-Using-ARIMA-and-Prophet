# Turkish Housing Price Index Forecasting Using ARIMA and Prophet

## Overview
This study analyzes and forecasts the **Turkish Housing Price Index (HPI)** using classical and modern time series methodologies. Specifically, **ARIMA** and **Prophet** models are implemented and systematically compared in terms of their short-term forecasting performance, residual behavior, and ability to capture structural changes.

The project is conducted within an academic framework and aims to contribute to the housing price forecasting literature by evaluating model performance on the same dataset using consistent evaluation criteria.

## Data Description
The dataset is obtained from the **Central Bank of the Republic of Turkey (CBRT)** through the **Electronic Data Distribution System (EVDS)**.  
Monthly Housing Price Index (HPI) values are used, covering the period **2010–2025**.

- Frequency: Monthly  
- Base year: 2023 = 100  
- Variables:
  - `Date`
  - `TP KFE TR` (Housing Price Index)

## Methodology
The analysis follows a structured time series modeling pipeline:

1. **Exploratory Data Analysis**
   - Visual inspection of trends and regime changes
   - Period-based segmentation (2010–2015, 2015–2020, post-2020)

2. **Seasonality and Trend Analysis**
   - STL decomposition
   - No statistically significant seasonality detected

3. **Stationarity Tests**
   - Augmented Dickey-Fuller (ADF)
   - KPSS
   - Results indicate a non-stationary series

4. **Structural Break Analysis**
   - Zivot–Andrews test (single break)
   - Ruptures (PELT algorithm) for multiple structural breaks  
   - Breakpoints identified around **2015, 2020, and 2022**

5. **Modeling Approaches**
   - **ARIMA**: Parameter selection via `auto_arima`, resulting in ARIMA(2,2,4)
   - **Prophet**:
     - No seasonality components
     - Manually defined changepoints based on structural break analysis
     - `changepoint_prior_scale = 0.1`

6. **Model Diagnostics**
   - Residual analysis using Ljung–Box test
   - ARIMA residuals are close to white noise
   - Prophet residuals exhibit autocorrelation (consistent with its deterministic structure)

## Model Evaluation
Models are evaluated on a **hold-out test set (last 24 months)** using standard error metrics:

- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- Mean Absolute Percentage Error (MAPE)

### Summary of Results
- **Prophet** achieves lower RMSE, MAE, and MAPE values than ARIMA
- Prophet better captures rapid post-2020 trend acceleration
- ARIMA provides more conservative uncertainty intervals
- Prophet produces narrower confidence intervals, indicating limited uncertainty estimation

## Key Findings
- The Turkish Housing Price Index exhibits strong non-stationarity and multiple structural breaks
- Prophet outperforms ARIMA in short-term point forecasting under regime changes
- ARIMA remains effective in modeling stochastic dependence and residual behavior
- Manual changepoint specification significantly improves Prophet’s performance

## Technologies and Libraries
- Python
- pandas, numpy
- matplotlib
- statsmodels
- pmdarima
- prophet
- ruptures
- scikit-learn

## Conclusion
For housing price indices characterized by strong trends and structural breaks—particularly after 2020—**Prophet** provides superior short-term forecasting accuracy. However, **ARIMA** remains a robust benchmark model, especially when residual diagnostics and stochastic structure are of primary interest.

## Future Work
- Incorporating macroeconomic variables (interest rates, inflation, credit volume)
- Sensitivity analysis of Prophet uncertainty parameters
- Comparison with machine learning models (LSTM, XGBoost)
- Ensemble forecasting approaches

## References
Box, G. E. P., Jenkins, G. M., Reinsel, G. C., & Ljung, G. M. (2015). *Time Series Analysis: Forecasting and Control* (5th ed.). Wiley.  
Taylor, S. J., & Letham, B. (2018). Forecasting at scale. *The American Statistician*, 72(1), 37–45.  
Zivot, E., & Andrews, D. W. K. (1992). Further evidence on the great crash, the oil-price shock, and the unit-root hypothesis.  
Truong, C., Oudre, L., & Vayatis, N. (2020). Selective review of offline change point detection methods.

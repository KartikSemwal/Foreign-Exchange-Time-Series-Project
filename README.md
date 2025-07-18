## USD/INR Exchange Rate Forecasting using Time Series Models
This project presents a comprehensive time series analysis and forecasting of the USD to INR exchange rate using historical data from 1998 to 2025. The primary goal is to explore and model the behavior of the exchange rate using multiple statistical models and compare their forecasting performances.
## Problem Statement:
The USD to INR conversion rate is a volatile market, and it can be difficult to predict how the exchange rate will change over time. This can make it difficult for businesses and individuals to make informed decisions about currency exchange
## Solution Approach:
One way to improve the predictability of the Euro to USD exchange rate is to use time series analysis. Time series analysis is a statistical technique that can be used to identify patterns in data over time. By identifying these patterns, it is possible to make more accurate predictions about the future value of the exchange rate.
## Key Steps and Methodologies
**_1. Data Collection & Preprocessing_**
* Source: RBI’s Daily Reference Rate CSV dataset.
* Transformed to daily, weekly, monthly and yearly frequency to examine temporal patterns, and took the weekly resampled data as the final dataset for modelling as it has more clear peak and perks among all resample data.
* Handled missing values, ensured proper datetime formatting, and set date as index.
 
**_2. Exploratory Data Analysis (EDA)_**
* Visualized long-term trends in exchange rate using matplotlib and seaborn.
* Plotted histogram, kde plots, distribution plot.
* Applied GARCH(1,1) model to examine volatility over time.
* Conducted ADF Test to check stationarity.
 
**_3. Time Series Decomposition_**
* Decomposed the series into Trend, Seasonality, and Residual using seasonal_decompose().

## Forecasting Models:
**_1. ARIMA Model_**
* Used auto_arima() to select optimal (p, d, q) parameters.
* Fitted ARIMA on the training data and evaluated using: **_RMSE, MAE, MAPE, R² Score._**
* Produced forecast for future exchange rates.

**_2. GARCH Model_**
* Modeled volatility on ARIMA residuals using arch library.
* Applied GARCH(1,1) to capture conditional heteroskedasticity (time-varying volatility).
* Generated ±1 standard deviation prediction intervals.

**_3. Exponential Smoothing_**
* Applied Holt-Winters additive model (trend='add', seasonal='add').
* Forecasted weekly values and captured short-term trends.

## Hybrid Forecasting Model (ETS + GARCH)
* Combined Exponential Smoothing forecasts with GARCH-modeled volatility.
* Added prediction intervals using standard deviation bounds from GARCH.
* **_Final graph displayed:_**
  * Historical exchange rates.
  * Forecasted mean (ETS).
  * Uncertainty bounds (GARCH).

## Evaluation Metrics:
* RMSE, MAE, MAPE, and R² used to compare model performance.
* Hybrid model provided better interpretability with volatility-adjusted forecasts.

## Findings
* The histogram and KDE plot of the exchange rate revealed unimodal distribution, suggesting a central tendency with slight skewness.
* The Augmented Dickey-Fuller (ADF) test showed the original series is non-stationary. After applying first differencing, the p-value dropped significantly, confirming stationarity of the transformed series.
  
**_Time Series Decomposition (Seasonal Decompose):_**
  * Trend: Shows a clear upward trajectory over years (i.e., INR depreciates gradually).
  * Seasonality: Mild periodic effects, likely annual patterns.
  * Residual: Random white noise with no obvious pattern — indicates good decomposition.

**_ARIMA Modeling:_**
  * The model was trained on stationary data.
  * Forecasting showed smooth continuation, but didn’t capture volatility well.
  * Future forecasting using ARIMA model gave repeated values for every week, which showed shortcoming in our ARIMA modelling, whose root cause may be Mean Reversion.
  * ARIMA models assume the series will revert to its long-run mean over time. For longer horizons, forecasts converge to a constant value (usually the historical mean), thus giving us a flatten out graph.
    
**_GARCH Modeling:_**
* The plot perfectly demonstrated the volatility clustering which the GARCH parameters (α₁ + β₁ = 0.98) predicted:
  * Calm periods (low volatility) persist for months/years
  * Turbulent periods (high volatility) cluster together
  * Transitions between regimes are clearly visible  
* **_Major Economic Events Captured:_**
  * 2004: Early economic liberalization volatility.
  * 2008-2009: Global Financial Crisis impact on INR.
  * 2013: The famous "Taper Tantrum" - massive spike to ~2.3 (highest in the data).
  * 2020: COVID-19 pandemic uncertainty.
  * Recent years: Relatively stable with occasional spikes.

**_Hybrid Model – Exponential Smoothing + GARCH_**
* Exponential Smoothing (ETS) captured level, trend, and seasonality.
* Residuals of ETS were passed into GARCH.
* Final forecast = ETS forecast + GARCH forecast of residuals.
* Result: Improved accuracy and better alignment with volatility seen in real-world exchange rates.
* The final visualization showed a stable trend with realistic uncertainty, thanks to volatility modeling.

## Insights
* This project offers valuable insights into the patterns and volatility of the USD to INR exchange rate, which can be critical for policymakers, businesses, investors, and individuals engaged in international trade or currency exchange.
* The analysis highlights how the Indian Rupee (INR) has shown a general long-term depreciation trend against the US Dollar (USD), with identifiable seasonal variations and clustered volatility periods. Through time series modeling and volatility estimation using ARIMA, Exponential Smoothing (ETS), and GARCH models, the project effectively demonstrates the behavior of exchange rate movements and the risks associated with unpredictable fluctuations.
* While the historical analysis and modeling provide a reliable basis for short- to medium-term forecasting, it is important to recognize that currency exchange rates are influenced by dynamic macroeconomic and geopolitical factors, and the future may deviate from past trends.
* Overall, this project demonstrates the practical utility of combining classical and volatility models for exchange rate forecasting and offers a valuable tool for data-driven financial decision-making in an uncertain economic landscape.











 

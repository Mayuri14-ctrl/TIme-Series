# Time-Series

What are the components of time series?
Trend: movement of data , it could be upward or downward
Seasonality: regural patterns occuring at fixed intervals
Irregular movement: Unexpected fluctuations that do not follow a pattern
Cyclic: not fixed, can occur over longer period. example: Recession

Types of times series model
1. Moving Average: Averaging past values over a fixed window to smooth fluctuations
2. Autoregressive model: Predicts future values based on the past values using a linear relationship
3. ARMA: Combines Movie Avergage and Autoregressive
4. ARIMA : Handle non stationary time series by differencing the data to remove trends
5. SARIMA: It extends ARIMA  y including seasonal components
6. ETS (Exponential smoothening):  Give more weights to recent data for foreascting
7. Holt's Linear Trend method
8. Holts winter method
9. LSTM : Deep neural network for long term dependencies

### Step by step guide
step 1.Observe the data for any trend and seasonality, handle both in forecasting using STL

step 2. check for stationarity in data using 
if mean and variance do not change over time
we use Augmented Dicky Fuller test
If p-value > 0.05, the time series is not stationary. We need to apply differencing.
what is ADF? 
It checks for the presence of unit root
A time series with unit root will show
1. Upward or downward trend
2. Strong autocorrelation with past values
3. mean and variance that change over time
4. slow decay of autocorrelation over time
   example: Yt=Y(t-1)+a
   here next value is based on past value plus random noise , this will drift over time
   why it is a problem?
   variacne increase over time
   ARIMA requires staionarity
   unrelaible predictions
How to apply ADF?
apply differencing
delta Y=Y(t)-Y(t-1)
``` y_diff=np.diff(y)```
y_lag=y[:-1] 
It regresses the lagged data with differenced data
delta y=a+by(t-1)+cy(t-2)
model=sm.OLS(y_diff,x)
check t statistic

STep 3: Handle stationarity
1. Apply differencing
2. Log transformation
3. Use seasonal ARIMA
   
Periodogram: Identify dominant frequencies. It is computed by Fourier transform
In the series with high periodicity , it should exhibit clear peaks at frequencies

Handle multiple Periodicities
Seasonal Decomposition: Use STL, what is STL-> trends, seasonality and residual component
a Hybrid or Ensemble Model: Sarima or prophet

Step 4 Find best parameters for ARIMA
ACF and PACF
To understand correlation between past observations and current observations
ACF: It checks correlation between time series and its own lagged values
The bar represents correlation at different lag
A slow decay suggests a non stationary process
If the ACF cuts off after  a certain lag , it indicates an MA(q) model
If ACF does not cut off sharply, it might not be an MA(q) model.

PACF helps identify Auto-Regressive model
It measures direct relationship between an observation and its lagged values without any influence of intermediate lags

Step 5  Model evaluation
MAE
RMSE
MAPE: when units matter, % for better interpretability


I worked on the demand forecasting project where we needed to prdict demand at SKU, catgoery, distributer and retailer for Middle East countries
The company was facing overstockinga dn understoking which let to lost in sales and high inventory cost
Demand was highly seasonal and influnced by external factors at SKU level, so we followed bottom to up approach to forecast at retailer level
Our task was to build accurate forcastig mothods to help company optimized their inventory. We needed to test multiple models to identify best forcasting methods and evalaute 
W gathered historical sales data for each SKU, marketing and promotion spends, external factors
the data has missing value , treated threm using interpolation
Removing outliers using IQR and STL
feature engineering

Model selection, we had 12 different model, statitics based, Machine Learning based Deep learning
I also tried ensemble approach where I checked mape using all , best 3 and few selected algorithms to check MAPE, We figured in 80% of the data ensemble methods were working better
I read multiple papers and found top to down and bottom to up appoarch, and in our model, bottom to up approach worked better as there was high variable demand  at lower level.
Promotion , pricing, demad shift different SKUs

I evauated method using MAPE to ensure robustness

what is stacking?


```pip install pandas numpy matplotlib statsmodel pmdarima```

1. Import libraries
``` import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import statsmodel.tsa.stattools import adfuller
import statsmodel.tsa.arima.model import ARIMA```

2. Load the times series dataset
```df.head()

3. Check for stationarity
A time series is stationary if its 

4. Periodogram: Check for dominant frequency
Identify seasonal patterns




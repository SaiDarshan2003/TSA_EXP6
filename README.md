## Ex.No: 6  HOLT WINTERS METHOD
### Date: 
### AIM:
To implement Holt-Winters model on National stocks exchange  Data Set and make future predictions
### ALGORITHM:
1. Import necessary libraries: pandas, numpy, matplotlib, and ExponentialSmoothing from statsmodels.
2.Parse the datetime column and set it as the index of the DataFrame.
3. Convert the closing price column to numeric and remove rows with missing values.
4. Extract the closing price column for time series analysis.
5. Apply the Holt-Winters exponential smoothing model with additive trend and seasonal components.
6. Fit the model to the cleaned data.
7. Forecast the closing prices for the next 30 business days.
8. Plot both the historical Ethereum prices and the forecasted prices.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.holtwinters import ExponentialSmoothing
data = pd.read_csv('infy_stock.csv') 
data['dateTime'] = pd.to_datetime(data['Date'])  
data.set_index('dateTime', inplace=True)
print(data.columns)
data['Close'] = pd.to_numeric(data['Close'], errors='coerce')  
clean_data = data.dropna(subset=['Close'])  
close_data_clean = clean_data['Close'] 
model = ExponentialSmoothing(close_data_clean, trend="add", seasonal="add", seasonal_periods=12)
fit = model.fit()
n_steps = 30
forecast = fit.forecast(steps=n_steps)
plt.figure(figsize=(10, 6))
plt.plot(close_data_clean.index, close_data_clean, label='Original Data')
plt.plot(pd.date_range(start=close_data_clean.index[-1], periods=n_steps+1, freq='B')[1:], forecast, label='Forecast', color='orange')
plt.xlabel('Date')
plt.ylabel('Trades')
plt.title('Holt-Winters Forecast for Ethereum Prices')
plt.legend()
plt.show()
```
### OUTPUT:
#### FINAL_PREDICTION
![Screenshot 2024-10-16 152804](https://github.com/user-attachments/assets/17ab98bd-a291-44f7-9052-f96796fd6da8)

### RESULT:
Thus the program run successfully based on the Holt Winters Method model.

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

%matplotlib inline

data = pd.read_csv(r"C:\Users\admin\Desktop\dataset\faang_stock_prices.csv")

data['order_date'] = pd.to_datetime(data['Date'])
data.set_index('order_date', inplace=True)

data['final_price_usd'] = data['Open']

original = data['final_price_usd']

regular_diff = original.diff()

decomposition = seasonal_decompose(original, model='additive', period=12)
seasonal_adjusted = original - decomposition.seasonal

log_transform = np.log(original)

log_reg_diff = log_transform.diff()

final_series = log_reg_diff.diff()

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(original, label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('order_date')
plt.ylabel('final_price_usd')

plt.subplot(6, 1, 2)
plt.plot(regular_diff, label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('order_date')
plt.ylabel('Differenced final_price_usd')

plt.subplot(6, 1, 3)
plt.plot(seasonal_adjusted, label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('order_date')
plt.ylabel('Seasonally Adjusted final_price_usd')

plt.subplot(6, 1, 4)
plt.plot(log_transform, label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('order_date')
plt.ylabel('Log(final_price_usd)')

plt.subplot(6, 1, 5)
plt.plot(log_reg_diff, label='Log + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('order_date')
plt.ylabel('RDiff(Log(final_price_usd))')

plt.subplot(6, 1, 6)
plt.plot(final_series, label='Log + Regular + Seasonal Diff')
plt.legend(loc='best')
plt.title('Log Transformation, Regular & Seasonal Differencing')
plt.xlabel('order_date')
plt.ylabel('SDiff(RDiff(Log(final_price_usd)))')

plt.tight_layout()
plt.show()

data[['final_price_usd']].plot(kind='line', title='Final Price USD Time Series')
plt.show()

### OUTPUT:
<img width="1201" height="196" alt="image" src="https://github.com/user-attachments/assets/64159110-a037-41fa-8dc5-0c613817d8de" />
<img width="1183" height="556" alt="image" src="https://github.com/user-attachments/assets/06ea8af2-be17-40f2-a3f3-ea69921412ad" />
<img width="1247" height="397" alt="image" src="https://github.com/user-attachments/assets/eb3d8ab2-91b3-4e6f-b23e-d9f983f1a3ec" />
<img width="1210" height="510" alt="image" src="https://github.com/user-attachments/assets/998d8c1e-9ae4-4328-8625-03105b3a9a93" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.

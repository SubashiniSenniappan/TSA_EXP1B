# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 
# Developed by :Subashini S
# Reg no:212222240106

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on weather classification.




### ALGORITHM:

1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.



### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller

# Load the data
df = pd.read_csv('/content/weather_classification_data.csv')

# 1. Regular Differencing
df['Temperature_diff'] = df['Temperature'].diff()

# ADF Test for Regular Differencing
adf_result_diff = adfuller(df['Temperature_diff'].dropna())
print('ADF Statistic for Regular Differencing:', adf_result_diff[0])
print('p-value for Regular Differencing:', adf_result_diff[1])

# 2. Seasonal Adjustment (assuming monthly data with a seasonality period of 12)
df['Temperature_seasonal_diff'] = df['Temperature'] - df['Temperature'].shift(12)

# ADF Test for Seasonal Adjustment
adf_result_seasonal = adfuller(df['Temperature_seasonal_diff'].dropna())
print('ADF Statistic for Seasonal Adjustment:', adf_result_seasonal[0])
print('p-value for Seasonal Adjustment:', adf_result_seasonal[1])

# 3. Log Transformation
df['Temperature_log'] = df['Temperature'].apply(lambda x: np.log(x) if x > 0 else np.nan)

# Log Differencing after transformation
df['Temperature_log_diff'] = df['Temperature_log'].diff()

# ADF Test for Log Differencing
adf_result_log_diff = adfuller(df['Temperature_log_diff'].dropna())
print('ADF Statistic for Log Differencing:', adf_result_log_diff[0])
print('p-value for Log Differencing:', adf_result_log_diff[1])

# Plotting the results
plt.figure(figsize=(18, 5))

# Plot Regular Differencing
plt.subplot(1, 3, 1)
plt.plot(df['Temperature_diff'], label='Regular Differencing')
plt.title('Regular Differencing')
plt.legend()

# Plot Seasonal Adjustment
plt.subplot(1, 3, 2)
plt.plot(df['Temperature_seasonal_diff'], label='Seasonal Adjustment')
plt.title('Seasonal Adjustment')
plt.legend()

# Plot Log Transformation and Differencing
plt.subplot(1, 3, 3)
plt.plot(df['Temperature_log_diff'], label='Log Differencing')
plt.title('Log Transformation + Differencing')
plt.legend()

plt.tight_layout()
plt.show()
```

### OUTPUT:

![Screenshot 2024-08-28 095117](https://github.com/user-attachments/assets/ab499e03-26a0-4953-8339-c49906bcf374)

REGULAR DIFFERENCING:

![Screenshot 2024-08-28 095140](https://github.com/user-attachments/assets/5f71e10f-f586-4c0e-9007-63b092002f5b)

SEASONAL ADJUSTMENT:

![Screenshot 2024-08-28 095151](https://github.com/user-attachments/assets/76ffdf44-aeb1-4e6b-962d-342fb36877b0)

LOG TRANSFORMATION:

![Screenshot 2024-08-28 095217](https://github.com/user-attachments/assets/be67e2ca-5f05-41ca-9abd-c99f185484f2)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on weather classification.

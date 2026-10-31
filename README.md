# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# Date: 31-10-2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.
### DataSet:
Silver price prediction.

### Software Used:
Google colab

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv('/content/silver_prices_clean.csv')

data['Date'] = pd.to_datetime(data['Date'], errors='coerce', utc=True)
data = data.dropna(subset=['Date'])
data = data.set_index('Date')

print(type(data.index))

resampled_data = data['Close'].resample('YE').sum().to_frame()

resampled_data.head()

resampled_data.index = resampled_data.index.year
resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Date': 'Year'}, inplace=True)
resampled_data.head()

years = resampled_data['Year'].tolist()
passengers = resampled_data['Close'].tolist()

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, passengers)]

n = len(years)

b = (n * sum(xy) - sum(passengers) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(passengers) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]

# Visualising results

# Trend Equations

# Linear Trend Estimation plot
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, passengers)]

coeff = [
    [len(X), sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

resampled_data['Close'].plot(kind='line', color='blue', marker='o', label='Actual Silver Price')
resampled_data['Linear Trend'].plot(kind='line', color='black', linestyle='--', label='Linear Trend')

plt.title('Linear Trend of Silver Prices')
plt.xlabel('Year')
plt.ylabel('Closing Price')
plt.legend()
plt.grid(True)
plt.show()
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
```

B- POLYNOMIAL TREND ESTIMATION
```python
poly_trend = [
    a_poly + b_poly * X[i] + c_poly * (X[i] ** 2)
    for i in range(n)
]
resampled_data['Close'].plot(kind='line', color='blue', marker='o', label='Actual Silver Price')
resampled_data['Polynomial Trend'].plot(kind='line', color='red', marker='o', label='Polynomial Trend')

plt.title('Polynomial Trend of Silver Prices')
plt.xlabel('Year')
plt.ylabel('Closing Price')
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION

<img width="603" height="378" alt="image" src="https://github.com/user-attachments/assets/ba7cd89b-d77e-442f-bc3a-95306a93fcae" />

B- POLYNOMIAL TREND ESTIMATION

<img width="575" height="367" alt="image" src="https://github.com/user-attachments/assets/36391e70-ba19-4e92-b06f-6d0456abc014" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.

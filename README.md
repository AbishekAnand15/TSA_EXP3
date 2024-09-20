## Name: Abishek Xavier A
## Reg No: 212222230004
## Date: 

# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.

### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.


### PROGRAM:
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Load the furniture store sales data (replace with your actual file and encoding if necessary)
file_path = '/content/Super_Store_data.csv'  # Path to the sales dataset
data = pd.read_csv(file_path, encoding='ISO-8859-1')  # Adjust encoding if necessary

# Print columns to identify the correct column for sales
print(data.columns)

# Extract the sales column (Replace '<correct_column_name>' with the actual column name for sales)
time_series = data['Sales']  # Use the correct column name for sales

# Ensure the sales data is numeric (in case of formatting issues)
time_series = pd.to_numeric(time_series, errors='coerce').dropna()

# Calculate the number of data points and lags
n_data_points = len(time_series)
n_lags = min(35, n_data_points - 1)
acf_values = np.zeros(n_lags)

# Calculate the mean and variance of the sales data
mean = np.mean(time_series)
variance = np.var(time_series)
normalized_data = time_series - mean  # Remove the mean (center the data)

# Compute the ACF
for lag in range(n_lags):
    lagged_data = np.roll(normalized_data, -lag)
    acf_values[lag] = np.sum(normalized_data[:n_data_points-lag] * lagged_data[:n_data_points-lag]) / (variance * (n_data_points - lag))

# Plot the ACF results
plt.figure(figsize=(10, 6))
plt.stem(range(n_lags), acf_values, use_line_collection=True)
plt.title('ACF Plot for Furniture Store Sales')
plt.xlabel('Lag')
plt.ylabel('ACF')
plt.grid(True)
plt.show()

# Print the calculated mean and variance
print("Mean = ", mean)
print("Variance = ", variance)
```

### OUTPUT:
![Screenshot 2024-09-20 183757](https://github.com/user-attachments/assets/149091c3-a70f-4f27-8856-899efb8de975)



### RESULT:
    Thus, the auto correlation function in python is successfully implemented.

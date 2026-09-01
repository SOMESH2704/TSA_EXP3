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
import matplotlib.pyplot as plt
import pandas as pd

# --- Load your dataset (replace with your file/column) ---
# Example: avocado dataset (Total Volume column)
# data = pd.read_csv("avocado.csv")["Total Volume"].values

# Assuming the first column is dates and the second column contains the numerical data for analysis
data_series = pd.read_csv("Month_Value_1.csv").iloc[:, 1]

# Convert to numeric, coercing errors to NaN, then drop NaN values
data = pd.to_numeric(data_series, errors='coerce').dropna().values

# OR use your current list
# data = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Convert to numpy array
# data = np.array(data)

# Parameters
N = len(data)

# Check if data is empty after cleaning
if N == 0:
    print("Error: No valid numerical data found after cleaning.")
else:
    lags = range(min(N - 1, 35))  # number of lags to compute, ensure lags do not exceed data length

    # Mean & variance
    mean_data = np.mean(data)
    variance_data = np.var(data)

    # Compute autocorrelation
    autocorr_values = []
    for lag in lags:
        if lag == 0:
            autocorr_values.append(1)  # correlation at lag 0 is always 1
        else:
            # Ensure we don't go out of bounds for small N or large lag
            if N - lag > 0:
                auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
                autocorr_values.append(auto_cov / variance_data)  # normalize
            else:
                autocorr_values.append(0) # No overlap, autocorrelation is zero

    # --- Plot ---
    plt.figure(figsize=(10, 6))
    plt.stem(lags, autocorr_values)   # ✅ removed use_line_collection
    plt.title("Autocorrelation of Data")
    plt.xlabel("Lag")
    plt.ylabel("Autocorrelation")
    plt.grid(True)
    plt.show()
```

import numpy as np

data = [3, 16, 156, 47, 246, 176, 233, 140, 130,
101, 166, 201, 200, 116, 118, 247,
209, 52, 153, 232, 128, 27, 192, 168, 208,
187, 228, 86, 30, 151, 18, 254,
76, 112, 67, 244, 179, 150, 89, 49, 83, 147, 90,
33, 6, 158, 80, 35, 186, 127]

lags = range(35)



### OUTPUT:
<img width="751" height="480" alt="image" src="https://github.com/user-attachments/assets/9efb42f3-5c99-4144-965d-b635ad78ff71" />


### RESULT:
        Thus we have successfully implemented the auto correlation function in python.

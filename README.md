# Tesla Battery Analysis 🚗🔋

This repository contains Python code for analyzing data related to Tesla batteries. We aim to derive insights from the provided dataset using pandas, matplotlib, and machine learning techniques.

## Data Import
We start by importing the necessary libraries and loading the dataset into a Pandas DataFrame.

```python
import pandas as pd

# Import data into Pandas DataFrame
df = pd.read_excel(r'/content/Tesla Battery Survey.xlsx', sheet_name='All entries')
```

## Data Processing
We perform various data processing tasks such as calculating cumulated energy use, equivalent full cycles, and vehicle age.

```python
# Calculating Cumulated energy use and Equivalent full cycles
df['Cumulated energy use'] = df['Lifetime average [Wh/mi or Wh/km]?'] * df['Your range at 100%']
df['EFC'] = df['Mileage [km]'] * df['Your range at 100%']

# Convert date columns to pd.to_datetime for calculating the difference in days for vehicle age
df[['Date you charged to 100%','Manufacture date']] = df[['Date you charged to 100%','Manufacture date']].apply(pd.to_datetime)
df["Vehicle age"] = abs(df['Date you charged to 100%'] - df['Manufacture date']).dt.days / 356
```

## Data Visualization
We visualize the data using line plots and scatter plots to gain insights into the relationship between relative range and vehicle age.

## Model Estimation
We create a linear model to estimate relative range from vehicle age using least square error optimization.

## Error Analysis
We plot the distribution of model estimation errors and calculate the standard error of the relative range estimates.

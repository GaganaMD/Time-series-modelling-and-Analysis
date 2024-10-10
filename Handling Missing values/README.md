
# Missing Value Handling in Time Series Data

## Project Overview

This project focuses on handling missing values in time series temperature data, leveraging historical trends to fill gaps intelligently. The main goal is to utilize data from previous years and apply statistical techniques like rolling averages to smooth short-term fluctuations, ensuring that the dataset remains as complete and representative as possible for further analysis.

## Data Description

The dataset consists of time series temperature readings (`TEMP`) with associated timestamps. Some entries in the dataset have missing temperature values (`NaN`), which need to be filled in order to maintain data continuity and allow for accurate analysis.

---

## Key Steps and Code Implementation

### 1. Loading the Data

First, load the time series data into a DataFrame. The data is typically sourced from a file or an external database, and the relevant portion of the dataset is indexed by the `datetime` column. Below is an example of extracting data for a specific time range.

```python
aq_df_imp = aq_df['2015-02-21 10':'2015-02-21 23'][['TEMP']]
```

- **Explanation**: The above code selects temperature data for a 13-hour window (from 10:00 to 23:00) on the date 2015-02-21.

### 2. Forward and Backward Fill for Missing Values

To handle missing values (`NaN`), we apply **Forward Fill** and **Backward Fill** techniques. These methods replace missing values by propagating the nearest known values, either forward or backward in time, to fill gaps.

#### Forward Fill (`ffill`)

Forward Fill replaces missing values by using the last observed value. This is useful when the assumption is that the previous value is likely to hold steady for a certain period.

```python
aq_df_imp['TEMP_FFILL'] = aq_df_imp['TEMP'].fillna(method='ffill')
```

- **Example**: If a temperature value at 11:00 is missing, the temperature from 10:00 will be used to fill it.

#### Backward Fill (`bfill`)

Backward Fill fills missing values using the next known value. This method is particularly helpful when future data is expected to influence or correct gaps in the current period.

```python
aq_df_imp['TEMP_BFILL'] = aq_df_imp['TEMP'].fillna(method='bfill')
```

- **Example**: If the temperature value for 11:00 is missing, the temperature from 12:00 will be used to fill it.

---

### 3. Rolling Mean Calculation

To smooth out short-term fluctuations in temperature, we apply a rolling mean over a specified window. This process calculates the average temperature over the current and previous time points, which helps in reducing noise and highlighting long-term trends.

```python
aq_df_imp['TEMP_ROLLING'] = aq_df_imp['TEMP'].rolling(window=2, min_periods=1).mean()
```

- **Window Size**: 2 periods (each point is averaged with the one immediately preceding it).
- **Min Periods**: The minimum number of non-`NaN` values required to calculate the rolling mean. Here, at least one value is needed to compute the mean.

---

### 4. Handling Missing Values Using Previous Year's Data

In some cases, missing temperature values can be filled using data from the same date and time in the previous year. This approach assumes that the temperature pattern is cyclical, particularly in datasets where seasonal effects are prominent.

```python
aq_df_imp['TEMP_PREVY'] = aq_df_imp.apply(
    lambda x: aq_df.loc[x['datetime'] - pd.offsets.DateOffset(years=-1)]['TEMP']
    if pd.isna(x['TEMP']) else x['TEMP'], axis=1)
```

- **Logic**: If the temperature value is `NaN`, the code retrieves the value from the same date exactly one year earlier. Otherwise, the current temperature value is retained.

---

### 5. Index Resetting

To facilitate further operations like data merging or aggregation, we reset the index of the DataFrame. This step converts the `datetime` index into a regular column, which may be required for certain types of data manipulation or visualization.

```python
aq_df_imp = aq_df_imp.reset_index()
```

- **Purpose**: Index resetting ensures that time-based operations are easier to manage and simplifies the process of combining datasets based on common timestamps.

---

### 6. Accessing Previous Year's Temperature Data

To assist in filling missing values or performing analysis based on historical trends, you may need to retrieve temperature data from the same time period but one year earlier.

```python
aq_df.loc[aq_df_imp.index + pd.offsets.DateOffset(years=-1)]['TEMP']
```

- **Explanation**: This code accesses temperature values for the same index positions, shifted by one year backward, helping to impute missing data based on historical trends.

---

## Conclusion

By applying forward and backward fills, rolling averages, and historical data from previous years, this process effectively fills gaps in the temperature dataset while preserving the overall temporal structure. This approach ensures that time-dependent patterns, such as seasonal trends, are respected, making the dataset more reliable for subsequent analysis or modeling.

---

## Future Improvements

- **Interpolation**: Implement interpolation techniques (linear, polynomial, spline, etc.) for a more nuanced approach to filling missing values, particularly when trends are non-linear.
- **Seasonal Decomposition**: Further decompose the time series into trend, seasonal, and residual components to better understand and model the data.
- **Advanced Time Series Models**: Use models like ARIMA or SARIMA to improve temperature trend forecasting and imputation of missing values in more complex scenarios.

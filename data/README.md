## Dataset

The dataset used in this project includes hourly air quality measurements for different pollutants and meteorological features. It provides a comprehensive view of how different pollutants behave over time and under varying weather conditions.

### Attributes

The dataset contains the following key columns:

- **No**: Unique index for each observation.
- **Year, Month, Day, Hour**: Timestamp information to define when the data was collected.
- **PM2.5**: Fine particulate matter with a diameter of 2.5 micrometers or smaller.
- **PM10**: Particulate matter with a diameter of 10 micrometers or smaller.
- **SO2**: Sulfur dioxide levels (µg/m³).
- **NO2**: Nitrogen dioxide levels (µg/m³).
- **CO**: Carbon monoxide levels (mg/m³).
- **O3**: Ozone levels (µg/m³).
- **TEMP**: Temperature (°C).
- **PRES**: Atmospheric pressure (hPa).
- **DEWP**: Dew point temperature (°C).
- **RAIN**: Rainfall (mm).
- **WD**: Wind direction.
- **WSPM**: Wind speed (m/s).
- **Station**: The location/station where the data was collected.
  
### Sources

This dataset can be collected from public repositories that track air quality over time for specific locations, such as government agencies or environmental monitoring organizations. The current data used is a simulated/modified example for demonstration purposes.

For real-world applications, you could retrieve data from sources like:

- [OpenAQ](https://openaq.org/) - A platform for open air quality data.
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php) - Provides real-world datasets for air quality monitoring.

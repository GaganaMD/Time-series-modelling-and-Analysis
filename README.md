# Air Quality Analysis and Visualization 

This project focuses on analyzing and visualizing air quality data using Python libraries such as `pandas`, `matplotlib`, `seaborn`, and `plotly`. The dataset contains air quality measurements like `PM2.5`, `PM10`, `SO2`, `NO2`, `CO`, `O3`, and meteorological features such as temperature (`TEMP`), pressure (`PRES`), and dew point (`DEWP`). The data is visualized through time-series plots, autocorrelations, and various other analyses.

## Table of Contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Data Preparation](#data-preparation)
  - [Visualization](#visualization)
- [Features](#features)
- [Contributing](#contributing)
- [License](#license)

## Requirements

- Python 3.8+
- pandas
- matplotlib
- numpy
- seaborn
- plotly

## Installation

To set up the project, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/air-quality-analysis.git
    cd air-quality-analysis
    ```

2. Install the required Python packages:
    ```bash
    pip install -r requirements.txt
    ```

3. (Optional) Set up a virtual environment for the project:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

## Usage

### Data Preparation

The dataset used in this project contains several air quality measurements such as `PM2.5`, `PM10`, `SO2`, `NO2`, `CO`, and `O3` along with meteorological factors like `TEMP`, `PRES`, `DEWP`, and `RAIN`.

Before visualizing, the data is preprocessed to handle missing values, extract relevant time periods, and aggregate necessary columns.

### Visualization

You can visualize various aspects of the air quality data using the following commands:

1. **Time-series Plot**:
    ```python
    aq_df['2014':'2015'][['PM2.5','O3']].plot(figsize=(15,8), linewidth=3, fontsize=15)
    plt.xlabel('year_month_day_hour', fontsize=20)
    ```

2. **Autocorrelation Plot**:
    ```python
    pd.plotting.autocorrelation_plot(aq_df_na['2014':'2016']['TEMP'])
    ```

3. **Multi-variable Plot**:
    ```python
    multi_data = aq_df[['TEMP','PRES','DEWP', 'RAIN','PM2.5']]
    multi_data.plot(subplots=True)
    ```

4. **Seaborn and Plotly Visualizations**:
    - Create heatmaps, pair plots, and interactive visualizations using seaborn and plotly.

## Features

- **Air Quality Analysis**: Analyze and compare various air pollutants such as PM2.5, SO2, NO2, etc.
- **Time-series Visualization**: Visualize the air quality data over different years.
- **Autocorrelation Analysis**: Check for seasonality or time-based dependencies in temperature data.
- **Multi-variable Plots**: Plot multiple air quality factors and meteorological features side by side.
- **Interactive Plots**: Use `plotly` for dynamic, interactive data visualizations.

## Contributing

Contributions are welcome! If you'd like to contribute, please fork the repository, make changes, and submit a pull request. You can also open an issue to discuss potential features or bugs.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

# Project Overview: Stock Time Series Analysis on AWS

This project involves an in-depth time series analysis of stock data using statistical and machine learning methods, specifically focusing on the top 5 stocks sorted by trading volume. The selection criteria can also be adjusted to consider factors such as closing price, market capitalization, and momentum. The entire project is hosted using AWS services, with the original data stored on AWS S3 and all preprocessing carried out on AWS RDS using PostgreSQL and pgAdmin4. Jupyter Notebooks are hosted on Amazon SageMaker, and AWS tools like IAM, Lambda, Secrets, and EC2 are utilized for a complete data science workflow.

*Note: I will soon be updating this repository with Power BI dashboards to provide deeper insights to readers and interested stakeholders.*

## Quick Summary

![AWS Architecture Overview](placeholder_for_aws_architecture_overview.png)
*Image: Overview of the AWS architecture used for data storage, processing, and analysis, highlighting the interaction between different services.*

![Summary of Stock Analysis](placeholder_for_summary_image.png)
*Image: A chart summarizing the top 5 stocks by volume.*

The analysis identifies the most valuable stocks by volume, providing insights through visualizations and metrics. The data pipeline and hosting on AWS make this project scalable, allowing for real-time analysis to support informed investment decisions.

## Table of Contents

- [Project Overview](#project-overview-stock-time-series-analysis-on-aws)
- [Data Source](#data-source)
- [AWS Infrastructure](#aws-infrastructure)
- [Data Preprocessing](#data-preprocessing)
- [Stock Selection Criteria](#stock-selection-criteria)
- [Metrics and Analysis](#metrics-and-analysis)
- [Model Details](#model-details)
- [Visualizations](#visualizations)
- [How to Run the Project](#how-to-run-the-project)
- [Conclusion](#conclusion)

## Data Source

- **Original Data**: Stored in AWS S3, providing raw stock time series data, including identifiers, closing prices, and trading volume.
- **Altered Data**: Stored in AWS RDS (PostgreSQL), post preprocessing and cleaning using pgAdmin4.

The data is extracted, transformed, and loaded using a data pipeline that ensures quality and consistency across each step.

## AWS Infrastructure

The project utilizes a variety of AWS services to ensure scalability and reliability:

- **AWS S3**: Stores raw stock data for analysis.
- **AWS RDS**: Stores altered and preprocessed data using PostgreSQL.
- **Amazon SageMaker**: Hosts the Jupyter Notebooks for data exploration, preprocessing, and modeling.
- **IAM, Lambda, Secrets, EC2**: Used to automate tasks, secure access, and manage instances.

![AWS Architecture Overview](placeholder_for_aws_architecture_image.png)
*Image: Diagram showing how AWS services interact to facilitate data storage, processing, and analysis.*

## Data Preprocessing

Data preprocessing is essential to ensure data quality and accuracy in analysis. The preprocessing steps include:

- **Loading Data**: Original data is loaded from AWS S3.
- **Data Cleaning**: Handled on AWS RDS using PostgreSQL and pgAdmin4. Includes handling missing values, normalization, and date parsing.
- **Grouping and Aggregation**: Data is grouped by stock identifier, and metrics like volume are summed.

## Stock Selection Criteria

The project initially selects the top 5 stocks based on trading volume. However, the selection criteria can be adjusted to fit different investor requirements. Possible criteria include:

- **Trading Volume**: Identifies stocks with the highest liquidity.
- **Closing Price**: Highlights high-value stocks.
- **Market Capitalization**: Differentiates between large-cap, mid-cap, and small-cap companies.
- **Price Growth or Momentum**: Helps identify stocks with strong growth trends.

## Metrics and Analysis

The following metrics were calculated during the analysis:

- **Total Volume**: Summed for each stock to identify the top 5 stocks.
- **Closing Price Statistics**: Provides an overview of the average and variance in closing prices.
- **ARIMA Modeling**: Implemented to forecast future stock prices and identify trends. Metrics used include:
  - **Mean Absolute Error (MAE)**
  - **Mean Squared Error (MSE)**
  - **Root Mean Squared Error (RMSE)**

**Key Insights**:

- The top 5 stocks by volume are AAPL, INTC, MSFT, CSCO, and BAC.
- **Performance Metrics for ARIMA Model**:
  - **AAPL Stock**:
    - **Mean Absolute Error (MAE)**: 0.262
    - **Mean Squared Error (MSE)**: 0.097
    - **Root Mean Squared Error (RMSE)**: 0.311
  - **BAC Stock**:
    - **Mean Absolute Error (MAE)**: 0.175
    - **Mean Squared Error (MSE)**: 0.055
    - **Root Mean Squared Error (RMSE)**: 0.234
  - **CSCO Stock**:
    - **Mean Absolute Error (MAE)**: 0.295
    - **Mean Squared Error (MSE)**: 0.097
    - **Root Mean Squared Error (RMSE)**: 0.311
  - **INTC Stock**:
    - **Mean Absolute Error (MAE)**: 0.205
    - **Mean Squared Error (MSE)**: 0.072
    - **Root Mean Squared Error (RMSE)**: 0.268
  - **MSFT Stock**:
    - **Mean Absolute Error (MAE)**: 0.189
    - **Mean Squared Error (MSE)**: 0.060
    - **Root Mean Squared Error (RMSE)**: 0.245

- The stationarity of the time series was evaluated using rolling mean and standard deviation. Most stocks indicated non-stationary behavior, requiring further preprocessing like differencing.

## Model Details

### ARIMA Model

The ARIMA (AutoRegressive Integrated Moving Average) model was used to forecast stock prices. The ARIMA model includes:

- **AutoRegression (AR)**: Utilizes the dependency between an observation and a number of lagged observations.
- **Integrated (I)**: Differencing of raw observations to achieve stationarity.
- **Moving Average (MA)**: Incorporates the dependency between an observation and a residual error from a moving average model applied to lagged observations.

The model parameters were tuned to achieve optimal accuracy, evaluated using the following metrics:

- **Mean Absolute Error (MAE)**: Measures the average magnitude of errors without considering direction.
- **Mean Squared Error (MSE)**: Squares the errors before averaging, penalizing larger errors more than MAE.
- **Root Mean Squared Error (RMSE)**: The square root of MSE, providing error metrics in the same units as the original data.

![Rolling Mean and Standard Deviation for CSCO](placeholder_for_rolling_mean_csco_image.png)
*Image: Plot showing rolling mean and standard deviation for CSCO, providing insights into the stationarity of the time series.*

**Pros of ARIMA**:
- Effective for short-term forecasting when historical data is available.
- Simple to implement and understand, especially for univariate time series.

**Cons of ARIMA**:
- Limited to linear relationships and may not perform well for non-linear patterns.
- Requires the time series to be stationary, necessitating preprocessing steps like differencing.

## Visualizations

### Top 5 Stocks by Volume

![Top 5 Stocks by Volume](placeholder_for_top_5_stocks_volume_image.png)
*Image: Bar chart displaying the top 5 stocks based on volume, providing an overview of market activity.*

### Top 5 ETFs by Volume

![Top 5 ETFs by Volume](placeholder_for_top_5_etfs_volume_image.png)
*Image: Bar chart displaying the top 5 ETFs based on volume.*

### KDE of Closing Prices for Top 5 Stocks

![KDE of Close Prices for Top 5 Stocks](placeholder_for_kde_closing_prices_image.png)
*Image: KDE plot showing the distribution of closing prices for the top 5 stocks, providing insights into value distribution.*

### Time Series Forecasting

![ARIMA Forecasting for AAPL](placeholder_for_arima_forecasting_aapl_image.png)
*Image: Forecasted stock prices for AAPL using the ARIMA model, with confidence intervals showing the predicted trend.*

![ARIMA Forecasting for BAC](placeholder_for_arima_forecasting_bac_image.png)
*Image: Forecasted stock prices for BAC using the ARIMA model.*

![ARIMA Forecasting for INTC](placeholder_for_arima_forecasting_intc_image.png)
*Image: Forecasted stock prices for INTC using the ARIMA model.*

![ARIMA Forecasting for MSFT](placeholder_for_arima_forecasting_msft_image.png)
*Image: Forecasted stock prices for MSFT using the ARIMA model.*

### Seasonal Decomposition of Time Series

![Seasonal Decomposition for CSCO](placeholder_for_seasonal_decomposition_csco_image.png)
*Image: Seasonal decomposition of the time series for CSCO, showing the trend, seasonal, and residual components.*

![Seasonal Decomposition for INTC](placeholder_for_seasonal_decomposition_intc_image.png)
*Image: Seasonal decomposition of the time series for INTC.*

![Seasonal Decomposition for MSFT](placeholder_for_seasonal_decomposition_msft_image.png)
*Image: Seasonal decomposition of the time series for MSFT.*

### Error Metrics Visualization

![Error Metrics](placeholder_for_error_metrics_image.png)
*Image: Visualization of MAE, MSE, and RMSE for the ARIMA model, providing insights into the model's accuracy.*

The visualizations offer investors a clear picture of which stocks have the highest trading volume and potential future trends.

## How to Run the Project

1. **AWS Setup**: Ensure you have access to AWS S3, RDS, and SageMaker.
   - Set up necessary permissions using IAM.
   - Configure AWS Lambda and Secrets for automated tasks.

2. **Data Access**: Load the original data from AWS S3 and connect to AWS RDS to access the altered data.
   - Use environment variables to securely manage your database credentials.

3. **Running the Notebook**: Open Amazon SageMaker and run the Jupyter Notebook.
   - Execute each cell to perform data preprocessing, analysis, and visualizations.

4. **Customizing Criteria**: Update the code to modify the stock selection criteria based on different metrics such as market capitalization or momentum.

## Conclusion

This project provides a comprehensive view of stock performance by leveraging AWS cloud services for scalability and efficiency. The combination of metrics such as trading volume, closing price, and ARIMA-based statistical modeling helps in identifying valuable investment opportunities.

Future updates will include Power BI dashboards for deeper insights and visualizations. Feel free to adapt and extend this project to incorporate advanced metrics or real-time data streaming for live analysis.

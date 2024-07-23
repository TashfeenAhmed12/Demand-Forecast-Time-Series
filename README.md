# Demand-Forecast-for-the-Upcoming-LEC
This repository contains the implementation of a demand forecast for the upcoming LEC (Local Event Company). The project focuses on analyzing historical sales data to predict future demand using time series forecasting models like ARIMA and Prophet.

## Data
The dataset used in this project contains sales data with the following columns:
- Date
- Units Sold

The dataset is provided in an Excel file named `Sourcing case students excel.xlsx`.

## Methodology

### Data Preprocessing
1. Load the dataset and remove unnecessary columns.
2. Convert the 'Date' column to datetime format and set it as the index.
3. Handle missing values by dropping rows with NaNs.
4. Resample the data to a daily frequency.

### Time Series Decomposition
The time series data was decomposed into three components:
- **Trend Component**: Shows the underlying trend in the data.
- **Seasonal Component**: Shows the repeating patterns or cycles in the data.
- **Residual Component**: Represents the noise or error in the data not captured by the trend and seasonal components.

### Stationarity Test
The Augmented Dickey-Fuller test was performed to check if the time series data is stationary. Stationarity is crucial for many time series forecasting models, including ARIMA.

### Modeling

#### ARIMA Model
The ARIMA model parameters were determined using the SARIMAX function:
- Non-seasonal parameters: p=1, d=1, q=1
- Seasonal parameters: P=1, D=1, Q=1, s=4

The model was fitted to the training data, and the forecast was made for the test period.

#### Prophet Model
The Prophet model by Facebook was also used for forecasting. The data was reformatted to fit the Prophet model requirements, and the forecast was made for the test period.

## Results

### Model Performance

| Model   | MSE   | MAE   |
|---------|-------|-------|
| Prophet | 201.79| 12.41 |
| ARIMA   | 175.78| 10.12 |

### Forecast
Both ARIMA and Prophet models were used to forecast the demand for the next 21 days. The ARIMA model performed better with a lower MSE.

 ![image](https://github.com/user-attachments/assets/72044104-a278-4905-95d5-8a9687811398)

Trend Component:
This shows the underlying trend in your data. From the plot, we observe spikes which suggest that there are times when sales peak significantly. The trend component is relatively stable except for these peaks.
Seasonal Component:
This pattern repeats regularly over the dataset, suggesting strong seasonal trends. The consistent peaks and troughs indicate a predictable pattern of sales that could be linked to specific times of the year or month.
Key Insight: This seasonality must be accounted for in any forecasting models, as it strongly influences sales.
Residual Component:
Residuals represent the error of the model or the information not captured by the trend and seasonal components. Ideally, residuals should be randomly scattered around zero, showing no pattern.
Key Insight: Some significant outliers are visible, suggesting occasional deviations from the predicted values based on trend and seasonality alone. These could be due to unexpected events or anomalies in sales data.

![image](https://github.com/user-attachments/assets/e0893e9f-765b-44e5-a81f-f083134f7ce1)

Arima Plots
1. Standardized Residuals Plot
The standardized residuals plot shows the residuals from the model over time, ideally scattered randomly around the zero line without displaying any clear patterns or systematic structures. From the plot I received, while residuals mostly hover around zero, there are noticeable spikes. These spikes suggest occasional large errors, indicating that the model might not capture some specific data points well or that there are outliers affecting the model’s predictions.

2. Histogram Plus Estimated Density Plot
This plot provides a histogram of the residuals, overlaid with a kernel density estimate (KDE) and a theoretical normal distribution (N(0,1)). The goal here is to check if the residuals are normally distributed—a critical assumption for many statistical tests that may follow model fitting. The KDE suggests that the distribution of residuals has a slight deviation from the normal curve, particularly showing a slight skewness. This observation suggests that the model might benefit from transformations to achieve normality or that certain nonlinear aspects of the data are not captured by the model.

3. Normal Q-Q Plot
The Q-Q (Quantile-Quantile) plot is used to directly compare the quantiles of the residuals against the expected quantiles of a standard normal distribution. Ideally, the points should fall approximately along the red line if the residuals were normally distributed. In the provided plot, most points lie along the line except for the tails, which deviate significantly, especially in the upper tail. This indicates that the residuals have heavier tails than the normal distribution, suggesting the presence of outliers or extreme values the model is not accounting for.

4. Correlogram
The correlogram, or autocorrelation plot, shows the autocorrelation of the residuals up to 10 lags. It's used to determine if there is any leftover pattern in the residuals that should have been captured by the model. In an ideal scenario, all autocorrelations should fall within the blue shaded area, indicating they are not significantly different from zero. The plot I analyzed shows that all autocorrelations are within the confidence interval, suggesting that the model residuals do not exhibit significant autocorrelation, thus confirming that the model has captured the temporal dependencies effectively


## Conclusion
The ARIMA model outperformed the Prophet model in terms of Mean Squared Error (MSE). The forecast indicates the expected demand for the upcoming 21-day LEC period.
![image](https://github.com/user-attachments/assets/7fe6e469-2a57-483f-9e8a-6e5ca2e17106)


![image](https://github.com/user-attachments/assets/501c2ae6-528a-4036-9215-06ec058ed213)

The result of the Dickey-Fuller test provides strong evidence that the time series is stationary. This is crucial because many time series forecasting models, such as ARIMA, require the data to be stationary to provide reliable and meaningful predictions. Stationarity implies that the statistical properties of the series such as mean, variance, and autocorrelation are constant over time, which simplifies the modeling process.



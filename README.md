# Webpage-Traffic-Time-Series
 Exploratory and time series analysis on 6 years of daily data to predict the number of new users on an academic website using Seasonal ARIMA after data differentiation and Facebook Prophet

### Motivation
Often companies want to analyze the brand value they possess in the digital space or qunatify their online user engagement. One of the ways is by monitoring the traffic that their website produces, tracking growth based on new users, analyzing trend of existing users for retention and churn rate, uncovering certain trend patterns and forecasting the traffic that is supposed to follow to be better equiped for the future and take business along with computational decisions accordingly.<br>
This project is based on analyzing the current trend and seasonalitites as well as predict the future traffic landings on a website from new users to quantify growth using machine learning time series model.

### Problem Statement
Forecast the count of new visits on a daily basis for the next one year

### Dataset
The pageviews data is that of the website http://statforecasting.com/ of almost 6 years of data from 2014 to 2020. The data is publicly available and can be downloaded from [Kaggle](https://www.kaggle.com/bobnau/daily-website-visitors).

| Column            | Description                | Data Type |
|:---               |:---                        |:----------|
| Row               | Row number                 | Integer   |
| Day               | Day of the week in text    | String    |
| Day.Of.Week       | Day of the week in numeric | Integer   | 
| Date              | Date in mm/dd/yyyy format  | String    | 
| Page.Loads        | Daily number of pages loaded  | String    | 
| Unique.Visits     | Daily number of visitors from whose IP addresses there haven't been hits on any page in over 6 hours  | String    | 
| First.Time.Visits | Number of unique visitors who do not have a cookie identifying them as a previous customer  | String    | 
| Returning.Visits  | Number of unique visitors minus first time visitors  | String    | 

### Technical Details

#### Libraries
* pandas & numpy - for data wrangling and mathematical operations
* matplotlib and seaborn - for rich data visualization
* statsmodels - for checking data stationarity, trend-seasonal decomposition and ARIMA
* pmdarima - for auto arima
* prophet - for trend-seasonal decompostion, model fitting, cross-validation and evaluation

#### Data Exploration
* The website mostly garners traffic from new users
* All of the metrics seem to be normally distributed as mean and median are very close and display weekly and yearly seasonality
* Weekdays see major traffic as compared to weekends with few outliers.
* The spring season has most page loads and visits as compared to summer and fall. Since this being an academic website, the reason might be that the course is taught in spring
* In the later years, while the page loads and return visits are on decline, the number of new users coming onto the website shows an upward trend
* The page loads(and correspondingly other metrics) in 2017 saw a decline which was consistent from March-December as compared to rest of the years

#### Feature Engineering
* ARIMA
  * Differencing the data on year to take yearly seasonality into account
  * Differencing the data again with the previous value to make the data stationary
* Prophet
  * Defining weekly seasonality differently for on-off season

#### Modeling
* ARIMA
  * checking for stationarity using ADF and KPSS test
  * plotting ACF and PACF for evaluating auto-regressive and moving average parameters
  * using auto arima to do an exhaustive search of best model
* Prophet
  * adding different weekly seasonality for on-off season and yearly seasonality
  * adding US holidays to be considered
  * hyperparameter tuning of trend and seasonality scale along with additive/multiplicative seasonality

#### Evaluation
* ARIMA
  * RMSE on trained data was 228
  * no auto-correlation was found in residuals using Box-Ljung test
  * residuals were normally distributed with mean 0
* Prophet
  * RMSE of 400 on cross-validated data before hyperparameter tuning and 329 after
  * no pattern was found in residuals

#### Result
Decent forecast capturing trend and seasonality at all levels for the next one year

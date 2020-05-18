## Multivariate Temperature Forecasting Using RNN/LSTM 

**Project description:** The problem is a multivariate forecasting problem. Given a historical data of climate conditions, we need to predict the temperature of the next hour based on the climate conditions and temperature over the last 24 hours.

### 1. The Data
There are two data files, one for training and one for testing.

The training dataset has 52566 instances, across 14 variables, excluding datetime. Each instance has 14 measurements, among which ‘T (degC)’ is the target variable that I need to build a prediction model for. Additionally, each instance represents the 14 Iather measurements of every consecutive hour, which is indicative that this is a time-series data. The test dataset consists of 17447 instances. 

Unlike training set, test set has 336 columns, which is an aggregation of the 14 climate measurements across a period of 24 hours (a day). In other words, each test instance has a day worth of data. The test dataset was provided in such format so that it is ready for Keras Recurrent Network Model once it is ready to make predictions.

### 2. Basic exploratory data analysis
From the multivariate line chart (Multi-variables line chart), the first point that stands out is that the majority of climate measurements, except for ‘wv’, ‘maxwv’, and ‘wd’, have some sort of rhythm or pattern over time. Line chart of variable T (Temperature line chart) demonstrates the yearly pattern that I vaguely see in Graph 1. It’s worth noting that there are sets of variables that appear to have very similar pattern, such as: T -Tpot-Tdew; VPmax-VPact-VPdef; H2OC-rho. Is this a signal that these variable sets indicate correlations? The correlation matrix (Correlation matrix) shows that there is no strong positive correlation (the strongest is in pink, which is slightly higher than 0.25), but there are candidates of reasonably high negative correlations (the strongest is dark blue, which is about -0.9). It appears that variable ‘rho’ has strong negative correlations with many variables, among those are T-Tpot-Tdew, and VPmax-VPact-VPdef. 





## Multivariate Temperature Forecasting Using RNN/LSTM 

**Project description:** The problem is a multivariate forecasting problem. Given a historical data of climate conditions, we need to predict the temperature of the next hour based on the climate conditions and temperature over the last 24 hours.

### 1. The Data
There are two data files, one for training and one for testing.

The training dataset has 52566 instances, across 14 variables, excluding datetime. Each instance has 14 measurements, among which ‘T (degC)’ is the target variable that I need to build a prediction model for. Additionally, each instance represents the 14 Iather measurements of every consecutive hour, which is indicative that this is a time-series data. The test dataset consists of 17447 instances. 

Unlike training set, test set has 336 columns, which is an aggregation of the 14 climate measurements across a period of 24 hours (a day). In other words, each test instance has a day worth of data. The test dataset was provided in such format so that it is ready for Keras Recurrent Network Model once it is ready to make predictions.

### 2. Basic exploratory data analysis
From the multivariate line chart (Multi-variables line chart), the first point that stands out is that the majority of climate measurements, except for ‘wv’, ‘maxwv’, and ‘wd’, have some sort of rhythm or pattern over time. Line chart of variable T (Temperature line chart) demonstrates the yearly pattern that I vaguely see in Graph 1. It’s worth noting that there are sets of variables that appear to have very similar pattern, such as: T -Tpot-Tdew; VPmax-VPact-VPdef; H2OC-rho. Is this a signal that these variable sets indicate correlations? 

<p align="center">
  <img src="images/Capture1.PNG?raw=true">
</p>


<p align="center">
  <img src="images/Capture2.PNG?raw=true">
</p>

The correlation matrix (Correlation matrix) shows that there is no strong positive correlation (the strongest is in pink, which is slightly higher than 0.25), but there are candidates of reasonably high negative correlations (the strongest is dark blue, which is about -0.9). It appears that variable ‘rho’ has strong negative correlations with many variables, among those are T-Tpot-Tdew, and VPmax-VPact-VPdef. 


<p align="center">
  <img src="images/Capture3.PNG?raw=true">
</p>

### 3. Data pre-processing
In order to utilize Keras recurrent network models such as RNN, LSTM (Long-short term memory) or GRU (Gated recurrent unit), training set needs to be re-framed so that it is compatible with these recurrent net algorithms. I borrowed the function from here(https://machinelearningmastery.com/multivariate-time-series-forecasting-lstms-keras/), which can return reframed time series as a supervised learning dataset. The function takes as input the following parameters: the dataset, number of lag observations as input, number of observations as output, and whether to drop rows with NaN values. For the purpose of this project, the number of lag observations as input would be 24, as I want to predict the temperature by using data from the previous 24-hour window. Consequently, the number of observations as output for desired model is 1, or the temperature of the 25th hour.

Training dataset was first normalized. There are two normalizations that Ire experimented with using sklearn.preprocessing, which are MinMaxScaler and StandardScaler. The majority of the models trained for had data normalized using Standard normalization. Additionally, it is important to note that, in regards to training set, the order in which normalization and separation of training input and output was also experimented with. In other words, output used to train the models (ytrain) would either be normalized or not normalized. If normalization is not applied to ytrain, I wouldn’t need to rescale the predictions after calling model.predict() on test dataset. In the cases of the models trained, it appears that the models return better predictions if normalization. 

After using the function to reframe training set to have 1 output (prediction) for every 24 timesteps, I have a data frame of size 52542 x 350. This is because the function returns the prediction for all 14 variables, but I only need the final predictions of temperature. Thus, I would remove the 13 columns of the other climate measurements. Our updated data frame now has a shape of size 52542 x 337, and from here I can separate the input and output. Before separating the training input and output data, a split of proportions 80/20 was applied, so that I can have a validation set. In order to split, since the order of the instances is crucial due to the nature of time-series data, I use Pandas function loc[] to split training and validation sets. Finally, I use function reshape() for all input datasets (training, validation, and test), so that they would have Keras-ready format: (samples, timesteps, features/dimensions). These are the final shapes of the input sets for training, validation and test respectively: (42012, 24, 14), (10530, 24, 14), and, (17447, 24, 14). 





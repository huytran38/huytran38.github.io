## Using Weather Patterns to Predict a City's Energy Consumption and Renewable Energy Production

**Project description:** Using data from the fictitious Power City, the goal of this research is to construct predictive models for electrical energy production from wind and solar sources, and energy consumption across eight city sectors that can effectively forecast at an hourly level. My team also forecasted production and consumption values for a diverse set of days over the course of a single scenario year. Ultimately, these models can be used to assist in planning the demand-supply of renewable energy for a single city. Multiple machine learning methods (time series, neural networks, boosting, decision trees, random forest, and support vector machines) were explored and their performances were compared across ten datasets: wind and solar energy production, and consumption for eight sectors.

### 1. The Data

The data used for this project originated from fourteen files of raw data regarding Power City's energy production and consumption. All production and consumption files include hourly data – twenty-four records per day. Weather conditions and calendar specifics between all files include:

  a. Weather Condition Features: solar elevation, cloud cover, dew point, humidity, precipitable water, temperature, visibility, wind     speed, and pressure
  b. Calendar Day Features: day of the week, holiday, school day

### 2. Pre-processing & Exploratory Analysis

In order to get the files into a more comprehensible and cohesive format, some preliminary features were added and others were normalized in order to merge files. Initially separated time varibles (day, month, hour) were combined to generate a single DateTime column. Only two files had missing data: the scenario year weather and the solar array weather. Most of the missing values were filled in using the median value of the two weeks preceding and following the missing data point (median was preferred over mean due to the count of zeros in the data). The only exception was filling in values for Precipitation and Pressure variables, since many consecutive values were missing; for those values, the average of previous years was used to complete the data.

Once the files were merged, each was aggregated (using mean) by day to simplify the problem and smooth some of the noise coming from the weather data. The consumption data was subset into eight separate files, each representing a single sector of usage (residential, K-12 schools, etc.). Feature engineering was used to create additional calendar variables (such as ‘Weekend’ and ‘Season’), and dummy variables were extracted from categorical variables (‘Month’, ‘Day’, ‘Day of week’). All files except for the scenario file were split into 80/20 train/test sets.

<img src="images/datasetsvars.jpg?raw=true"/>

In observing the wind data, a nearly perfect linear relationship can be seen between wind speed and electricity production, which is no surprise; the greater the speed of the wind, the higher the production of electricity (Figure: Electricity Production by Wind Speed). However, from the plot, the level of energy starts to plateau after wind energy reaches a certain high level.

<img src="images/wind1.png?raw=true"/>

### 3. Time series model

Initial exploratory analysis was done in RStudio to identify starting autoregression, moving average, seasonality, and other parameters. Indepedent variable (electricity consumed) was tested for normality. Using the ACF, PACF, and EACF plots, potential seasonal parameters were identified, and also validated using the auto.arima() function. Models were then constructed using the SARIMAX() function from Python statsmodels library. The best performing parameters from the analysis done in RStudio were used to construct models, and the exogenous variables were reintroduced (weather conditions, calendar day features, etc.). The models were then tested against a test set using the RMSE and explained variance scores for evaluation. The parameters of each model were tweaked until the highest performing model was produced. 

Based on the low explained variance, models built for a couple of sectors (food service, residential) were considered unsuccessful. This might be due to limited data (one year worth) of city sectors' electricity consumption, while consumption appeared to be highly volatile during summer months.

<img src="images/FoodService_Consum.png?raw=true" width="425"/> <img src="images/Residential_Consum.png?raw=true" width="425"/> 

### 4. 

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 


```javascript
if (isAwesome){
  return true
}
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

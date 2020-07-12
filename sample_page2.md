## Timeseries Analysis of Madrid Air Quality 

**Project description:** 
- The high levels of pollution during certain dry periods in Madrid
- Provide recommendation on the usage of cars in the city
- Propose changes that can better the city of Madrid’s urbanism
- Use pollution prediction to adjust traffic and ensure that pollution does not exceed specified limits


### 1. The Data
- The data was found from Kaggle, but it is originally from Madrid’s City Council Open Data website
- The data set contains daily measurements of up to 17 air quality criteria pollutants (carbon monoxide, ozone, nitrogen dioxide, particulate matter, sulfur dioxide and others) registered from 2001 to 2018. 
- In addition, the list of 24 active  stations that are used for measurements are provided. Not every station has the same equipment, therefore each station was able to measure only a certain subset of particles.
- Split 24 stations into 2 groups: inner and outer stations

### 2. Methodology
1. AR: forecasts the variable of interest (target variable) using a linear combination of past values of the variable
2. MA: uses past forecast errors in a regression-like model to forecast variable of interest
3. ARIMA
4. SARIMA
5. Linear Regressions with Trend, Seasonality and Quadratic


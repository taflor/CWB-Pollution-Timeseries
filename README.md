# Causeway Bay Timeseries Pollution Model
*Hong Kong has been working to reduce emissions from motor vehicles, marine vessels, and power plants. In 2014, Hong Kong's Air Quality Objectives were put into effect.*

*After living in Hong Kong myself, it can be seen that pollution affects everyday life. Whether it is cancelling outside playtime for school children or sporting events for adults or finding yourself on a family hike surrounded by smog rather than the beautiful mountain views, everyone is somehow affected by air pollution.*

*This project's goal is to predict pollution over the next year to provide residents and tourists with estimated PM 2.5 levels. PM 2.5 are fine particulate matter that can cause a variety of respiratory issues, as well as reduce visibility. With these predictions, residents and tourists will better be able to plan their activities and travel.*

## 1. Data
This projects's dataset was obtained from the [World Quality Index Project](https://aqicn.org/city/hongkong/causeway-bay/) on February 15, 2021. The dataset contains PM2.5 and PM10 data spanning the dates of January 1, 2014 to February 15, 2021. This project utilized the dates up to December 31, 2019 due to recent events (Covid-19 pandemic) highly affecting the pollution in 2020 with the various shut-downs and social distancing measures put into place.

The dataset used for training, validation, and testing consisted of a total slightly above 2,200 rows of data.

## 2. Method
This is a timeseries forecasting problem with non-linear trends, therefore Facebook Prophet is used to forecast the PM2.5. This method allows for seasonality and holidays to be taken into account. Other advantages of using Facebook Prophet include its ease of use, speed, accuracy, and automation of dealing with outliers and dramatic changes.

## 3. Data Cleaning
[Data Cleaning Report](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/notebooks/1.0%20CWB%20Data%20Wrangling.ipynb)

Key features in a timeseries forecasting problem include the datetime stamp and the predicted variable. In order to ensure the highest accuracy, missing values were interpolated to allow for smoothing between dates. The original dataset consisted of 50 missing values, 25 in each row (10 can be seen as nan values, whereas the other 15 missing were due to missing date values as well), therefore not much information was lost.

## 4. Exploratory Data Analysis
[EDA Report](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/notebooks/2.0%20CWB%20EDA.ipynb)

Seasonality of the dataset is shown in the boxplot below when comparing month of the year to the average pm2.5 values and average pm10 values. The affect of seasons is most noticable in the pm25 boxplots.

![month-wise boxplot showing seasonality](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/visualizations/2.0_monthwise_boxplots_seasonality.jpg)

The timeseries below shows the pm2.5 for the years 2014-2020. The majority of values falls within the "Unhealthy" pollution rating, further supporting Hong Kong's cause to reduce emissions for the safety and wellbeing of it's citizens. The pollution scale can be found below.

![cwb timeseries with pollution rating colors](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/visualizations/2.0_timeseries_pm25_color.jpg)

![pollution rating scale](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/reference/Air%20Quality%20Measurements.png)


## 5. Machine Learning
[Model Report](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/notebooks/4.0%20CWB%20Modeling.ipynb)




# Causeway Bay Timeseries Pollution Model
*Hong Kong has been working to reduce emissions from motor vehicles, marine vessels, and power plants. In 2014, Hong Kong's Air Quality Objectives were put into effect.*

*After living in Hong Kong myself, it can be seen that pollution affects everyday life. Whether it is cancelling outside playtime for school children or sporting events for adults or finding yourself on a family hike surrounded by smog rather than the beautiful mountain views, everyone is somehow affected by air pollution. In order to spread awareness, Hong Kong provides residents with educational resources and daily pollution measurements.*

*Looking through past records, it is noticable that there are days of missing data, either due to maintenance of the measuring device or other reasons. In order to ensure high quality information continue to be available to the public, this project's goal is to predict PM 2.5 over the course of 2019 using PM 10.  PM 2.5 are fine particulate matter that can cause a variety of respiratory issues, as well as reduce visibility. With these predictions and records always being available, even when the measuring devices are out, residents and tourists will better be able to plan their activities and travel.*

*This project initially planned to utilize weather (and therefore weather predictions) to forecast PM 2.5, allowing for more accurate predictions with more regressors available. Since this data was unavailable to the public without intense web scraping of various formats, this particular forecast model requires PM 10 measurements. Thus, it is important that this device remain active. Should it become inactive while PM 2.5 devices are active, another forecast model could be created utilizing PM 2.5 to predict PM 10 measurements. In a real-life situation where a data scientist would be creating this model for the government, he/she would have access to past weather data and future predictions, allowing for greater forecast accuracy and future implementation.*

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

Our original problem: Forecast PM2.5 using PM10 in case of a device outage.

A Facebook Prophet timeseries forecast model was created and the mean absolute percentage error was the metric used to determine accuracy of the model. The below table contains the *mape* for the models created after adding each new regressor.

![fb prophet model performance](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/models/4.0_model_performance_metrics.png)

The final model was created using all above regressors, as can be seen in the graph of model components below.

![fb prophet model components](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/visualizations/4.0_forecasting_model_components.png)

## 6. 2019 Forecast
[2019 Forecast](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/notebooks/4.1%20CWB%20Final%20Forecast%20for%202019.ipynb)

![fb prophet 2019 forecast](https://github.com/taflor/CWB-Pollution-Timeseries/blob/main/visualizations/4.1_final_forecast_2019_timeseries.png)

The 2019 forecast is the shaded region to the right. The final 2019 forecast resulted in a mean absolute percentage error of 15.8% with an overall 15% *mape*.

## 7. Future Improvements
In a scenario when the Hong Kong government and/or HK Observatory are interested in creating and implementing a model to predict PM2.5 (or other pollution particulates measured), I advise adding weather regressors to the model to improve accuracy. Weather (e.g. rain, wind direction, wind speed) has been found to impact pollution measurements and having this historical information, as well as weather predictions, would be valuable to the future forecasts.

Additional holiday and date regressors would be beneficial to add should this information be known to the organization creating this model (e.g. government benchmarks and dates that could impact the pollution levels -- x percentage of marine vessels switched to low sulfur on z date).

## 8. Presentation
[Google Slidedeck](https://docs.google.com/presentation/d/1kovJiuVgEa7FPjVpbSu9SlS3Kkb1mqP2O3tMqbE5gDk/edit?usp=sharing)

## 9. Credits
Huge shout out to Ram Hariharan for being an amazing mentor and supporting me on my data science venture. I would also like to thank the creators and contributors of [FB Prophet](https://facebook.github.io/prophet/), as well as the data scientists whose articles and code for using Facebook Prophet have greatly helped me along the way -- [Leif Arne Bakker](https://futurice.com/blog/business-forecasting-with-facebook-prophet) and [Ruan van der Merwe](https://towardsdatascience.com/implementing-facebook-prophet-efficiently-c241305405a3).

---
#layout: post
title: Time Is Money
dark: False
image:
      url: /media/2018-09-20-time-is-money/cover.jpg
---
## Intro:
You don't realize how important time is until it hits you... And when it does, you quickly learn that planning and efficiency are your best friends.

## Motivation:
For my passion project at Metis I could choose to do any project that would require utilizing skills I have acquired in the last three months (Linear Regression, Classification, Clustering, NLP, Neural Networks, Time Series, etc.).
My professional expertise lies in transportation and so I decided on a topic as closely related to my domain as possible. Transportation industry as a whole, has always suffered from lack of transparency and therefore, inaccurate / inefficient pricing, as well as, disruptions due to traffic and weather.
The goal of my project is to predict Estimated Time of Arrival (ETA) and Fare of a personalized individual taxi ride.

## Dataset:
I used a dataset of Chicago city taxi rides containing around 22 million records (2016 and 2017 Jan-Feb), as well as, Chicago O'Hare airport daily weather dataset.

More information about the **taxi ride** dataset can be found [here](https://digital.cityofchicago.org/index.php/chicago-taxi-data-released/).

The **Weather dataset** contains daily precipitation, snowfall, snow depth, maximum / minimum temperatures and flag for weather tags (such as thunder, heavy fog, tornado, etc.).  
More information about **weather** dataset can be found [here](https://www.ncdc.noaa.gov/).

## Approach:
Thorough data analysis and exploration helped me to discover that taxi demand was mostly focused around Chicago downtown and the airports (as clearly visible in the plot below).  

![Demand plot is  Missing]({{"/assets/images/Chicago_Taxi_Demand_map.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Chicago_Taxi_Demand_map.png}})  

A further look into it, showed that my trip duration and fare (my target variables) were both skewed to the right, with most rides being distributed under 30 minutes and $20.

Another key take-away from data exploration was that my data clearly had time series related patterns, most notably, weekday and time of day. Please see the heat-map.

![Demand heatmap is  Missing]({{"/assets/images/Taxi_Demand_Heatmap.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Taxi_Demand_Heatmap.png}})

In order to understand how many lags to take as features for demand prediction, I used partial autocorrelation plot (please see below).  

![Partial Autocorrelation plot is  Missing]({{"/assets/images/Partial_Autocorrelation.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Partial_Autocorrelation.png}})

I concluded that 7 most recent lags, 96th and 672nd lags were enough to get a relatively good prediction.

## Project Flow
* User inputs origin / destination addresses and either chooses to travel now or enters a date and time
* Application retrieves historical demand of the last 7 days from postgreSQL database
* Differences the demand (calculates the increase / decrease from the previous timestamp) to remove the underlying trend
* Generates 9 lags and removes all the NaN values
* Finally, the algorithm uses standard scaler (used in the training of the model) to scale the variables
* Demand predictor model (OLS model) uses the latter demand feature array to predict the demand for the date and time provided by the user
* Weather information for that day is retrieved from a postgreSQL database
* 






## The Product:
If you would like to see a demo of my final product [click here](https://github.com/mastaus/metis_projects/blob/master/Time_Is_Money/Images/App%20Demo.mov).

If you would like to see my code or play around with the model itself, checkout my [GitHub page](https://github.com/mastaus/metis_projects/tree/master/Time_Is_Money).   
If you would like to see my final presentation [click here](https://docs.google.com/presentation/d/1xriOO8WHoY4NUBwriFRxvHKcMS5Cd_-agxeiourH7Ko/edit#slide=id.g35ed75ccf_0106).  

---
layout: post
title: Time Is Money
dark: False
image:
      url: /media/2018-09-20-time-is-money/cover.jpg
---
## Intro:
You don't realize how important time is until it hits you... And when it does, you quickly learn that planning and efficiency are your best friends.

## Motivation:
For my passion project at Metis I could choose to do any project that utilizes skills I have acquired in the last three months (Linear Regression, Classification, Clustering, NLP, Neural Networks, Time Series, etc.).
My professional expertise lies in transportation and so I decided on a topic as closely related to my domain as possible. Transportation industry as a whole, has always suffered from lack of transparency and therefore, inaccurate / inefficient pricing, as well as, disruptions due to traffic and weather.
The goal of my project is to predict Estimated Time of Arrival (ETA) and Fare of a taxi ride, based on origin and destination addresses and date & time.

## Dataset:
I used a dataset of Chicago city taxi rides containing around 22 million records (2016 and 2017 Jan-Feb), as well as, Chicago O'Hare airport daily weather dataset.

More information about the **taxi ride** dataset can be found [here](https://digital.cityofchicago.org/index.php/chicago-taxi-data-released/).

The **Weather dataset** contains daily precipitation, snowfall, snow depth, maximum / minimum temperatures and flag for weather tags (such as thunder, heavy fog, tornado, etc.).  
More information about **weather** dataset can be found [here](https://www.ncdc.noaa.gov/).

## Approach:
Thorough data analysis and exploration helped me to discover that taxi demand was mostly focused around Chicago downtown and the airports (as clearly visible in the plot below).  

![Demand plot is  Missing]({{"/assets/images/Chicago_Taxi_Demand_map.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Chicago_Taxi_Demand_map.png}})  

A further look into it, showed that my trip duration and fare (my target variables) were both skewed to the right, with most rides being distributed under 30 minutes and $20.

Another key take-away from data exploration was that my data clearly had time series patterns, most notably, weekday and time of day. Please see the heat-map.

![Demand heatmap is  Missing]({{"/assets/images/Taxi_Demand_Heatmap.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Taxi_Demand_Heatmap.png}})

In order to understand how many lags to take as features for demand prediction, I used partial autocorrelation plot (please see below).  

![Partial Autocorrelation plot is  Missing]({{"/assets/images/Partial_Autocorrelation.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/images/Partial_Autocorrelation.png}})

I concluded that 7 most recent lags, 96th and 672nd lags were enough to get a relatively good prediction.

## Project Flow
* User inputs origin / destination addresses and either chooses to travel now or enters a date and time
* Date and time is either assigned the timestamp of now or formatted to correct datetime format
* Addresses are converted to coordinates (lat/longs)
* Weather information for that day is retrieved from a postgreSQL database
* Historical demand of the last 7 days is also queried from postgreSQL database
* Demand variable is differenced (the increase / decrease from the previous timestamp is calculated) to remove the underlying trend
* 9 demand lags are generated and all the NaN values are removed
* Then my algorithm uses standard scaler (initiated in the training of the model) to scale the variables. *Scaling is needed in order not to inflate the significance of independent variables with inherently larger numerical values*
* Demand predictor (Ordinary Least Squared) model uses earlier described demand feature array to predict the demand for the date and time provided by the user
* Predicted demand is appended to weather and location data to create a feature space for my final models
* Target variables are logged
* The whole feature space is then scaled using the scaler initiated during Random Forest model training
* Finally, Random Forest for ETA and Random Forest for Fare models are run to predict a log of the duration and fare of a taxi ride
* As a last step the results are exponentiated to convert them from log values to seconds and dollars, respectively, and an ETA is generated by adding the duration (in seconds) to the user input date and time.

To visualize my work, I created a Flask app to allow users to interact with my product (a demo video is available on my Github).

## Results
* My final model for ETA prediction explains 86% of the variance (in the test set) and generates a prediction within ± 4min.
*  That for fare explains 97% of the variance and generates a prediction within ± $1.5.

## Fun facts
  * Interestingly, when looking at feature importance, for ETA prediction demand seems to be the seconds most important feature after distance, whereas it is pretty insignificant when estimating the fare. This is clearly the result of lack of transparency in the regular taxi business (unlike Lyft / Uber)
  * Out of all the features, weather related variables have close to no influence on the either duration or fare of a taxi trip

## The Product: 
If you would like to see my code or play around with the model itself, checkout my [GitHub page](https://github.com/mastaus/metis_projects/tree/master/Time_Is_Money).   
If you would like to see my final presentation [click here](https://docs.google.com/presentation/d/1xriOO8WHoY4NUBwriFRxvHKcMS5Cd_-agxeiourH7Ko/edit#slide=id.g35f391192_00).  

## Hope you enjoyed this post, sadly this is my last post as Metis student...

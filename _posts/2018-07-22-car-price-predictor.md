---
layout: post
title: Estimating Second-hand Car Price in Lithuania? 
dark: false
image:
      url: /media/2018-07-22-car-price-predictor/cover.jpg
---

## Intro:
If you have ever owned a car and you are not a car dealer or a child of one (like I am), you must have spent quite some time scratching your head, wondering how much your car is worth, especially once you were ready to sell it. Likely you are either emotionally attached to your car, absolutely hate it or somewhere in-between, but either way, you are biased when deciding how to price it.
If you've ever been in the described situation, read on! *But even if you haven't, keep reading, you might in the future.* :smirk:

## What and How?
As part of my quest to learn more about Data Science, I took on a challenge to see if Linear Regression can help me to estimate a second-hand car price (in Lithuania). Using two web-scraping techniques: Selenium and BeautifulSoup I retrieved about 1,500 second-hand car records from [Autoplius.lt](https://en.autoplius.lt/) website.   

### Challenges:
It was then turn for the "fun" part - cleaning it up. To begin with, the data came in text format (including price and other numerical features), I created a few helper functions in order to easily convert them to numbers. Secondly, a lot of my data was categorical (e.g. Make = BMW). Unfortunately, qualitative variables cannot be used in a Linear Regression model, I ended up creating *dummy variables* to replace them, because removing them completely would have significantly decreased my chances of developing a good model.   In order to somewhat account for the effect make has on price, I created variables to identify German, French and Japanese cars. For that of colour, I added flags to mark white and red cars.  
Now I was finally able to review my dataset. Thorough data analysis helped to identify outliers, such as cars that are older than 1995 or newer than 2016, cars with a price lower than €200 or more expensive than €40,000, as well as, cars with zero mileage (new) or ones with more than 450,000km driven. I went ahead and excluded the outliers, since my model was not being designed to account for such extreme cases.   
Finally, after assessing correlation plots, I narrowed down my dataset to the target variable (Price) and the following features:
1. Year of manufacture
2. Gearbox (manual / automatic)
3. Engine Size (in litres)
4. Mileage (km)
5. Japanese flag
6. French flag
7. German flag
8. Red colour
9. White colour

As the last step of cleaning process, I dropped all the cars that had any missing values for my chosen 9 features. The final dataset contains 1,015 cars in total.

### Modelling:
In search for the best model I explored a few options:
* Simple model with no transformation to any of the variables
* A model with logarithmic price transformation (normalized the distribution)

* Linear Regression model after normalization and regularization (Ridge and Lasso)  
 
**Number 2 won the race!**


### Results:
The model was trained on 70% of the dataset, while the remaining 30% was used to test it. The results were better than expected (given the challenges):  
* Price estimate at around 62% accuracy
* 67% of the variance in price explained by the 9 selected features *(when run on the test dataset)*

Even though results sound pretty good, when putting it in context, things don't seem so rosy. The average price of a car in my dataset is €5,700, the median price is just short of €4,000 and the average error is about €2,480. At the moment, my product cannot tell the difference between a BMW or Mercedes-Benz and an Open (they are all German cars in it's view). :flushed:   
Always good to put things into perspective :smirk:  

### The Future:
As I learn new Data Science techniques, I would like to refine this model to account for Make, Model, Colours and other categorical features that significantly influence second-hand car prices. :sunglasses:

## The Product:   
If you would like to see my code or play around with the model itself, checkout my [GitHub page](https://github.com/mastaus/metis_projects/tree/master/Car_Price_Estimation).   
If you would like to see my final presentation [click here](https://docs.google.com/presentation/d/1AWq3BJ6FTHG31dSinrZBUF_bDULnI8BUTrLn_kL36Q0/edit#slide=id.p).
### I hope you enjoyed my post. Your feedback would be much appreciated!

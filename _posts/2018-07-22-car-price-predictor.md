---
layout: post
title: Estimating Second-hand Car Price in Lithuania? 
---
## Intro
If you have ever owned a car and you are not a car dealer or a child of one (like I am), you must have spent quite some time scratching your head, wondering how much to sell your old car. For starters, likely you are either emotionally attached to your car or absolutely hate it, and therefore biased when deciding how to price it.
If you've ever been in the described situation, read on! *But even if you haven't, keep reading, you might in the future.* :smirk:

## What and How?
I have been working on testing if Linear Regression can help me to estimate a second-hand car price in the Lithuanian market. I used two web-scraping techniques: Selenium and BeautifulSoup to retrieve car data from [Autoplius.lt](https://en.autoplius.lt/) website (the most popular second hand dealership website in Lithuania).   
I collected a dataset of about 1500 different cars, which I chose to first save in a binary format, in other words, *pickled* it.

## Challenges
It was now turn for the "fun" part - cleaning it up. To begin with, the data came in a text format (including price and other numerical features), I created a few helper to help with this process. Secondly, a lot of my data was categorical (i.e. text), e.g. Make, which cannot be used in a Linear Regression model, so I had to *dummify* some of those variables, because removing them completely would have signidicantly decreased the chances of developing a good model. In order to account for the Make and Colour, I created a variables to identify German, French and Japanese cars, and white and red cards, respectively.
Now, I was finally able to review my dataset, during the analyis I identified some outliers, such as cars that are older than 1995 or newer than 2016, cars with a price lower than €200 or more expensive than €40,000, as well as, cars with zero mileage (new) or ones with more than 450,000km driven. I went ahead and excluded the outliers, since my model was not being designed to account for such extreme cases.
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

Once the dataset was narrowed down, as the last step of cleaning, I dropped all the cars that did not have at least one of the 9 features, which left me with 1015 cars in total.

## Modelling
In search for the best set of features, I exploresd a few options:
1. Simple model with no transformation to any of the variables
2. A model with logarithmic price transformation
3. Linear Regression model after normalization and regularization (Ridge and Lasso)   
Number 2 won the race!

## Results
The model was trained with 70% of the dataset, and the remaining 30% was used to test it. The results were better than expected, given the challenges:  
* Price estimate at around 62% accuracy
* 67% of the variance in price explained by the 9 selected features (when run on the test dataset)

Even though results sound pretty good, when putting it in context, things don't seem so rosy. The average price of a car in my dataset is €5,700, the median price is just short of €4,000 and the average error is about €2,480. At the moment, my product cannot tell the difference between a BMW or Mercedes-Benz and an Open or Audi (they are all German cars in it's view). :flushed:    It's always good to put things into perspective :smirk:  

## The Future
As I learn new Data Science techniques, I would like to refine this model to account for Make, Model, Colours and other categorical features that significantly influence second-hand car prices. :sunglasses:

## The Product

If you are interested in my final presentation it's available [HERE](https://docs.google.com/presentation/d/1AWq3BJ6FTHG31dSinrZBUF_bDULnI8BUTrLn_kL36Q0/edit#slide=id.p).   
If you would like to see my code or play around with the model itself, checkout my [GitHub page](https://github.com/mastaus/metis_projects/tree/master/Car_Price_Estimation).

### I hope you enjoyed my post. Your feedback would be much appreciated!

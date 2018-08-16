---
layout: post
title: Will You Pass?
---
## Intro  
We live in a society where kids and teenagers are put under increasingly more pressure. Pressure to do well at school, to get best grades, to find a great job and beyond...

## Why and How?  
With an idea to help our future generation, I decided to work on an application that would allow students to predict their final grade (Pass / Fail) for different disciplines.
By simply providing some personal, family and discipline related information and seemingly unrelated details about her / his leisure time spending choices, a student would get a prediction (Pass / Fail) and a corresponding probability to pass (in %).

## Dataset
This time I chose a relatively clean dataset, prepared by P. Cortez and A. Silva through Portuguese School Survey in 2014. I used two datasets, one containing information about Mathematics discipline, the second one - Portuguese language.
The datasets were easy to interact with, but needed variable "dummification" (converting "Yes" / "No" values to 1 / 0). Finally, some of the variables such as first and second trimester grades had to be removed due to their direct influence on the final grade. Overall, I had 1,045 records, which is on a lower side for a classification problem, but hey, beggars can't be choosers :smiley:  

## Modelling  
Choosing the right algorithm and hyper-parameters was quite a challenge. I ended up exploring 7 different classification models (mentioned below) and plenty of parameter combinations for each model, which led me to my best **Random Forest** model (at 87% precision and 67% under-the-curve score) *(with 150 estimators, balanced class weight, max tree depth of 20, min 10 samples per leaf and min 2 samples per split)*.
  1. K-Nearest Neighbors (KNN)
  2. Logistic Regression
  3. Random Forest
  4. Naive Bayes (Gaussian)
  5. Naive Bayes (Bernoulli)
  6. Support Vector Classifier (SVC)
  7. Stochastic Gradient Descent (SGD)

![ROC Curve Image Missing]({{"/assets/ROC_Curve.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/ROC_Curve.png}})

In addition, I experimented with three oversampling techniques (SMOTE, Random Over Sampler and ADASYN), but they did not help to make the model more accurate.

## Results

## The Product
![Image Missing]({{"/assets/app_interface.png"|https://github.com/mastaus/mastaus.github.io/blob/master/assets/app_interface.png}})  
If you would like to see my code or play around with the model itself, checkout my [GitHub page](https://github.com/mastaus/metis_projects/tree/master/Student_Grade_Estimator).   
If you would like to see my final presentation [click here]().  

### I hope you enjoyed my post and look out for the next one in 3 weeks!

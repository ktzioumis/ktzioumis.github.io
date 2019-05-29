---
layout: post
title:      "Building a Machine Learning Model is Exhausting"
date:       2019-05-28 22:42:26 -0400
permalink:  building_a_machine_learning_classifier_is_exhausting
---


## Introduction:

This was my first opportunity to take a deep dive into a data set of my own choosing so why did I choose this Los Angeles Metro Bike Share Trip Data[https://www.kaggle.com/cityofLA/los-angeles-metro-bike-share-trip-data](https://www.kaggle.com/cityofLA/los-angeles-metro-bike-share-trip-data) ? Los Angeles is a city I have never visited (I live in New York, East Coast baby) and bicycling is a mode of transport I don't particularly care for but I was drawn into a snapshot of a system at work anyway.  I wanted to know how this little web was going to play out.

## The Dataset:

The dataset furnishes us with plenty of details, we even get we get something akin to the 5 Ws [https://en.wikipedia.org/wiki/Five_Ws](https://en.wikipedia.org/wiki/Five_Ws)

* When - Timestamped Start and End times 
* Where - Start and End Stations with Latitude and Longitude
* What - Trip Route Category: One-Way or Return Trip and Duration
* Who - Passholder Types: Flex Pass, Monthly Pass, Walk-up 
* Why - So that they can ride a bike!

The briefest of glances shows 762 Bikes ridden over 130 thousand times between 66 Bike stations between early July  2016 and  the end of March 2017, the LA bike share network certainly looks like it was a hit!


**Behold the Network!**

![In all it glory!](https://i.imgur.com/JOItLVo.jpg)

Downtown LA is home to a dense network of bicycle stations, they are conveniently close-by for anyone in need of a ride or looking to drop-off at their destination. There are 2 additional stations outside the downtown area at Culver City and Venice by the beach. These stations only have rides attributed to them at the very end of our dataset's time period and appear to represent new additions to the network. 

## Learning Machines:

The goal of this project was to apply a machine learning classifier model to some aspect of the chosen dataset but I wanted to go one better and I built two. To make it more interesting they had to be different as well, one was to be a discrete classifier and the other a regression model on a continuous variable.

After exploring the time series data I elected to break apart the starting datetime condition into some key components: an On-Peak/Off-Peak class, the day, the month and the rounded off hour of the day. Based on these starting conditions, I wanted to know how much could we predict about what the rider was going to do? I was ready to grab the tiger by the tail and try to model one of the ride components; the Duration.

Of course to model the ride duration it was important to pretend I don't know about the end conditions of the ride, End Time is a proxy for duration and if we knew the end location of the ride then the ride is over and we know how long it went for. We're doing this the hard way, damnit!

Now what modelling method should I choose? Maybe Decision Tree Regressor or maybe a Random Forest Regressor (even more trees!), why not both?! So I'm not doing 1 machine learning model for regression now, I'm doing 2!

And my classifier model I chose to do on the membership types, they all ride the same bikes but do they ride them *differently?* What kind of classifier to use here? Random Foresat Classifier, ADABoost? XGBoost? ALL OF THEM?! I did indeed get a little carried away with building machine learning models and instead of making 1 I made 5....

Just 5?

I want the regressor to regress and I want the classifiers to classify but most importantly I want them  to do it well! Thats where hyper parameters come in, using sklearn's GridSearchCV I was able to automatically run and re-run these models with different hyper parameters to tune their performance aaaaand apply a 3 times crossfold validation. So no it wasn't 5 machine learning models after all it was...

**840 + 288 + 432 + 27 + 162  = 1749**

## 1749 Models

Well that was a bit of an effort wasn't it, hope it was quick...


<img src='https://i.imgur.com/TWJDjEP.png' >

Not exactly.....



---
layout: post
title:      "New York Restaurant Guide "
date:       2019-09-16 22:47:08 -0400
permalink:  new_york_restaurant_guide
---

*Because we all gotta eat amirite?*

I spent 3 years working in 2 Greenwich Village restaurants. As a line cook mostly, but also as a barista and a busser. I know from experience that the New York restaurant industry takes food safety inspections seriously. They have to, the thousands in fines are enough to drive a business struggling on razor thin margins over the edge but the real cost is having to put up that "Grade Pending" sign, or worse a big ol' "B" . A "C" is just gross. My Food Safety Certification is, sadly, expired now and I'm not as quick with a pair of tongs as I used to be but taking this deep dive into the New York City Department of Health and Mental Hygiene's open record of inspection results brought a lot of memories flooding back (Table 7, order up!).

Read my full analysis and machine learning on [Github](https://github.com/ktzioumis/New-York-Restaurant-Guide)
 
As a part of the New York Open Data project all Deptment of Health inspections for the 3 years prior to the most recent inspection are made publicly available. The complete dataset can be found here: [DOHMH New York City Restaurant Inspection Results](https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j). This dataset is updated daily! [NYC Open Data](https://opendata.cityofnewyork.us) is an amazing resource for all data scientists and all New Yorkers and for people (like me!) who happen to be both it is also a fantastic way to get to know their own city.

This project involved the most extensive data cleaning I have done so far. The database consists of almost 400 thousand rows, each representing an individual citation to a restaurant for... something. The scope of this dataset was staggering, The Dept of Health performs multiple kinds of inspections some of which are graded and some of which are not. It was necessary to focus this dataset on what I was interested - Food. An interesting problem was renegotiating this data from its current format of individual citations to a form that made more sense to me making each row an inspection. Inspections could result in 0 or many (sometimes far too many for comfort) violations that that make up a score and determine the grade awarded to the restaurant. I was able to achieve this by creating a new index of CAMIS and date unique pairs and then reading in the violation results for the inspection that occurred that day. The database was further culled to a 3 year period from mid 2016 to mid 2019 and in the end I had a 65,932 inspection results with violation details, scores, restaurant information all neatly packaged in individal rows and most importantly GRADES.

An A is precious, anywhere even remotely upmarket in New York pretty much HAS to get an A. The inital inspection is not the end of the sotry when it comes to getting an A, you can argue the point in a Tribunal Hearing and you are entitled to a reinspection one week later but even to not be able to display that A for a single day can get notice. Per Se is one othe most well known (and expensive) restaurants in New York and when it got a bad score on an inspection in 2014 it became the subject of an article on Business Insider ([](https://www.businessinsider.com/per-se-grade-pending-2014-3) .  So can we predict which restaurants will get an A and which will not?

Yes we can!

With 68% accuracy! And achieving this in two ways using XGBoost Classifiers raises an interesting comparison for machine learning construction. 

My predictive models use restaurant characteristics that fall lossely into 3 categories:
- Location - Community Board
- Type - Cuisine Description and Chain status
- History - Previous Score and Previous Critical Flags
 
The previous score, previous critical flags are numerical features are used the same for both classifiers. 
The chain status (whether or not the restaurant is part of chain with multiple locations) is a binary feature and is used the same for both classifiers
Cuisine Description and Community Board are categorical features and this is where the two models diverge.

![](https://i.imgur.com/MQOCMcR.png)<br>
*Starting Matrix*

The first model used one-hot encoding to create a large sparse matrix with 156 columns that consist mostly of zeroes. It does quite well, the classification report is below.

![](https://i.imgur.com/2cnBO8u.png)<br>
*Sparse Matrix Classification Report*

The second model took a different approach to the categorical features. The summary statistics for each cuisine style and community board consisting of mean, standard deviation and count were derived in exploratory data analysis. For this second model I used the categorical features as key to the summary statistics stored in a separate dataframe and merged them together

![](https://i.imgur.com/vd1LQXA.png)<br>
*Merging summary statistics into categorical features*

This created a matrix of 9 numerical columns that I believe maintained the important information from the categorical features in a much smaller matrix.

![](https://i.imgur.com/j8yOF2F.png)<br>
*Summary Statistics Matrix*

The second model was just as accurate as the sparse matrix classifier!

![](https://i.imgur.com/gxIVol2.png)<br>
*Summary Statistics Matrix Classification Report*

It also had one huge advantage; it trained in one tenth the time. Training the classifier on the sparse matrix took approximately 16 seconds per pass. Training the classifier on the summary statistics matrix took just 1.5 seconds per pass. The advantage in training is important becuase this is a continuously updated dataset. Inspections occur in New York City daily and will continue as long as there are restaurants (i.e. forever). An agile learning algorithm is important for keeping the model current. The model will need to be retrained to maintain accuracy as new data become available. If the dataset is expanded beyond the current 3 year period then this will also lead to longer training times that may make the sprase matrix unusable. 

Substituting my categorical data for summary statistics greatly reduced training time while maintaining accuracy. In this instance it worked, the features described we can reasonably expect to be normally distributed and a mean and standard deviation provide a good decription of distribution without having to one-hot encode it all. This may not work for everything but its certainly worth a shot.

---
layout: post
title:      "New York Restaurant Guide"
date:       2019-09-16 22:47:08 -0400
permalink:  new_york_restaurant_guide
---

*Because we all gotta eat amirite?*

I spent 3 years working in 2 Greenwich Village restaurants. As a line cook mostly, but also as a barista and a busser. I know from experience that the New York restaurant industry takes food safety inspections seriously. They have to, the thousands in fines are enough to drive a business struggling on razor thin margins over the edge but the real cost is having to put up that "Grade Pending" sign, or worse a big ol' "B" . A "C" is just gross. My Food Safety Certification is, sadly, expired now and I'm not as quick with a pair of tongs as I used to be but taking this deep dive into the New York City Department of Health and Mental Hygiene's open record of inspection results brought a lot of memories flooding back (Table 7, order up!).

Read my full analysis and machine learning on [Github](https://github.com/ktzioumis/New-York-Restaurant-Guide)
 
As a part of the New York Open Data project all Deptment of Health Inspections up to the 3 years prior to the most recent inspection are made publicly available. The complete dataset can be found here: [DOHMH New York City Restaurant Inspection Results](https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j). This dataset is updated daily! [NYC Open Data](https://opendata.cityofnewyork.us) is an amazing resource for all data scientists and all New Yorkers and for people (like me!) who happen to be both it is also a fantastic way to get to know their own city.

This project involved the most extensive data cleaning I have done so far. The database consists of almost 400 thousand rows, each representing an individual citation to a restaurant for... something. The scope of this dataset was staggering, The Dept of Health performs multiple kinds of inspections some of which are graded and some of which are not. It was necessary to focus this dataset on what I was interested - Food. An interesting problem was renegotiating this data from its current format of individual citations to a form that made more sense to me making each row an inspection. Inspections could result in 0 or many (sometimes far too many for comfort) violations that that make up a score and determine the grade awarded to the restaurant. This was achieved by determining all the unique combinations of Restaurant ID (CAMIS) and date that would indicate an individual inspection





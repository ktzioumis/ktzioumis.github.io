---
layout: post
title:      "Pandas , SQL and t-tests"
date:       2019-07-08 22:16:15 -0400
permalink:  pandas_sql_and_t-tests
---


Pandas is a powerful python library, SQL is an ubiquitous databasing language and t-tests are a eminently useful hypothesis testign tools. Each of these are incredible tools in their own right but this project has been about using all three in concert. And most importantly, using them to extract meaning and value from data.

Microsoft's well known [Northwind Traders Database](http://https://www.geeksengine.com/article/northwind.html) describes the company oprations through a number of interconnected database's like below: 

<img src='https://ras-blogdb.restdb.io/media/594a33ce72b4cf350000130d' width=600 height =300><br>
*Northwind Traders Schema*

Information about the company is distributed across 13 interconnected tables with connections in each table linked by unique keys. Tables describe different areas of the company's operation; for example, there's a table for customers and a table for products and the two are linked by a third table where customers have placed orders for products. Making sense of it all separately is extracting one story from three separate books. SQL is how we take that story and give it its own book 

Learning SQL was a challenge in its own way, but I was glad for an opportunity to use another language and see the way it differs from python. There's no *right* way to build a query language or a coding language and every one has its strengths and weaknesses but most importantly it has its own structure its own commands. Learning SQL was a necessary reminder that things are sometimes just different, not better, not worse, just different. I look forward in future to broadening my aptitude with SQL and other langiuages to take my coding skills to another level of versatility.

Mating SQL with  python can be performed through the **sqlite3** library which interacts very nicely with pandas to create DataFrames. Because, why should things be difficult when they could be easy? By using the pandas command **pd.read_sql()** and passing my (carefullly constructed) SQL query I was able to create one DataFrame that extracted only the relevant information from multiple tables and nothing else. I got my story out of all those books and into one easy to read slim volume. An example is below:

<img src='https://i.imgur.com/pqpvUkJ.png'><br>
*Elegant, am I right?*

Pandas, of course, shines when it come to data manipulation, visualisation and the Exploratory Data Analysis that is the first step to answering any question about data (check out this blog post about [visualising data](https://ktzioumis.github.io/visualizing)). The question is where the t-test comes in. t-tests are amazing, a t-test is *a type of inferential statistic used to determine if there is a significant difference between the means of two groups, which may be related in certain features.* (Thanks [Investopedia](https://www.investopedia.com/terms/t/t-test.asp)!). Really this means that a t-test, much like this Big Bird gif, will tell you if one of these things is not like the other.

![](https://media.tenor.com/images/dc1bce1662dba811859df99da31d8c51/tenor.gif)

Importantly, the t-test is a statistical measure. Not a yes-or-no, the outputs we take from the t-test is a probability - The likelihood that the sample means from the tested datasets are equal. It is up to us to determine whether or not the p-value is sufficient to reject or not-reject (important! we do not *accept* the null hypothesis, we fail to reject it) the null hypothesis. This determination is somewhat arbitrary, for this project I set that bar 0.05. This is a comon threshold and means that there is 5% likelihood that the samples have the equal means. Where the t-test p-value is below this, I determine that a 5% chance is too low to accept that the the means are equal. 

Being able to state with statistical confidence that groups of data **are** different is where we extract meaning and value. This ability has very broad potential for the (imaginary) business that I am anaysing. In this project I use it to determine the answers to 4 questions:

1.  Do discounts have a statistically significant effect on the number of products customers order? If so, at what level(s) of discount?
2.  Do certain product categories sell better in the Americas or Europe?
3.  Do late deliveries effect Customer's ordering?
4.  Does Number of Territories for each employee affect their sales figures?

Each of these questions touch on a different facet of the business:

1. Sales volume by price point
2. Sales volume by region
3. Supply chain logistics
4. Employee performance

And it is this versatility that is truly impressive. By chaining together an SQL query from the database of tables to create a pandas DataFrame and performing t-test analysis insights into widely varying aspects of the business, its operation and the performance of its customers, suppliers and employees is possible.

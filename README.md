# Customer Segmantation
This is the analysis about Maven Rewards Challenge (Sept 2024).
The description of the challenge was: you’ll play the role of a Sr. Marketing Analyst at Maven Cafe. You've just run a test by sending different combinations of promotional offers to existing rewards members. Now that the 30-day period for the test has concluded, your task is to identify key customer segments and develop a data-driven strategy for future promotional messaging & targeting.

# Dataset
The dataset used in this analysis can be found of this link: https://mavenanalytics.io/challenges/maven-rewards-challenge/404c6060-60eb-400f-9bce-c3b9f97e9d5a

In this analysis I used KMeans clustering to segment customers into 3 segments for the customers with all the details and for those with missing details the segments were 2.

This analysis is broken into 4 playbooks
 00 - Is a simple exploratory analysis. Analysing data with minimal manipulations
 01 - I used a principle of RFM (Recency, Frequency and Money) for segmenting customers using only the transactions they made
 02 - I expanded RFM to include the offers the customers received, viewed and completed
 03 - In 02 and 03 I only focussed on customers with full details. In this notebook 03, I focussed on the customers with missing details (this for me, represented the unknown class of customers)


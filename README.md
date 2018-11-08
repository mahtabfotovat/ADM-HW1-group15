# ADM-HW1-group15

# Homework 2 - How do Taxis move in NYC? 

The purpose of this homework is to perform analyses on data about Taxi trips in NYC.
The data source we used is : http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml .

----------


Approach
-------------

We analyzed data on three months [April, May and June] of 2018. 
We noticed anomalies in data, and for that reason we took into account only following cases : 

> - Trip distance is positive and greater than 0
> - Trip duration is positive and greater than 0
> - Number of passengers is positive and greater than 0
> - Drop off time is after the pick up time
> - Pick up time is in 2018
> - Total amount is positive and greater than 0


**RQ1**

1. Weighted hourly average of number of trips per day in order to understand which are the peak hours.
2. Plot of the weighted hourly average per day, for seeing the busiest hours. Thus, we observed that the average timeslot in which people in NY took taxi, was in the lunchtime (13h-14h).
3. Average number of trips per day for each borough.

**RQ2**

We looked into number of passengers per timeslots. 
The first graph shows that the least number of passeengers is in the morning around 6 am and the highest number of passengers is around midnight.
We looked into the same data per borough, and trends of the average number of passengers per hour in different borough were not similar.

We can say that Brooklyn and Manhattan follow the same pattern like overall NYC. 


**RQ3**

We analyzed trip duration.
Because we noticed that there are some records with very long trip durations which are probably uncorrect, we decided to focus on trip durations which are maximum 3 standard deviations far from the mean. 
From the corrected data we can see that the most frequent trip duration is between 8 and 14 minutes. The plot in the file has the shape of right skewed distribution.

Bronx, Brooklyn and Manhattan have approximately the same trip duration frequency like overall NYC. Histogram for EWR shows higher frequency of longer trip durations, between 18 and 43 minutes, which is expected, taking into account that it is airport area, further from the city center.

**RQ4**

We looked into the payment methods.
After the computation, we found out that credit card is the most used way of payment, followed by Cash payments, in overall NYC and in each borough.

We used ChiSquare to make a comparison between observed and expected values for payment methods in each borough. 

Based on the results of the test, we can state that there is no correlation between the borough and the payment method.

**RQ5**

We looked for the possible correlation between long distance trips and average duration of the trip.

After eliminating outliers and using Pearson's correlation coefficient, we came into conclusion that there is a strong linear correlation between trip distance and trip duration.

**CRQ1**
We analyzed how the fare for mile changes across NY's borough.
When we calculated fare for mile with simply dividing total amount paid with the trip distance, we could see bigger differences between boroughs. On the other hand, when fare for mile was weighted by the trip duration, differences in price between boroughs became less important. Reason could be that some boroughs have higher traffic density, which is causing that customers are spending more time in the vehicle and paying extra amounts for the same distance. 
This findings are supported by the results of ttest.


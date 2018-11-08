# ADM-HW1-group15
# Homework 2 - How do Taxis move in NYC? 
In this assignment we perform an analysis of Taxis in NYC. In particular, we are curious to answer to some specific *research questions* (__RQs__) that may help Taxi drivers in planning their movements throughout the city and the Taxi's users to have hints about the convenience of enjoying this service.

For this purpose we use the open data of Taxi's trips in NYC. In order to answer to the *RQs* we take into account the data related to Yellow cab for the year 2018.

![alt text](https://www.brickunderground.com/sites/default/files/styles/blog_primary_image/public/blog/images/4859177053_c3fb190917_o.jpg "Logo Title Text 1")

____

## Before starting
Here you find the list of task you need to perform before running the analysis.

1. Download [Yellow cabs data](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml) (2018).
2. Due to the size of the file, you will experience that fit all this data in memory is hard. Above all, if you are able to load data in memory, it's gonna be hard to run any analysis. For these reasons, before starting we really encourage you to take a look at the *RQs* and afterwords think of a strategy to deal with data. Learn how to free your memory [here](https://teamtreehouse.com/community/how-to-delete-a-variable-in-python).
* In order to do the analysis by borough you need to combine the *Yellow cabs data* with the dataset you find in `taxi_zone_lookup.csv`. Take a look [here](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.join.html) and [here](https://pandas.pydata.org/pandas-docs/stable/merging.html).
* Observe the dataset:
    * Read the [legend](http://www.nyc.gov/html/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf) of each columns to understand the data
    * Read [something about Yellow Taxis in NYC](http://www.nyc.gov/html/tlc/downloads/pdf/taxi_information.pdf) to make meaningful statements and comments.
* Get an [overview](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.describe.html) of the dataset, what are the variable types? May we need to change something?  E.g. some trips register distance 0, does it make sense?
* Check the presence of NaN values and decide how to deal with them (do I exclude them from the analysis?)

____ 

# VERY VERY IMPORTANT
1. __!!!Read the entire homework before coding anything!!!__
2. As any data analysis task, there __is not__ a unique and correct way to answer to our RQs. Since the results you get for each RQ may depend on choices you make during the analysis, it is very important (__necessary__) that you describe any single decision you take and all the steps you do.
____



# General notes:
* At the beginning of your analysis, decide and clearly state what borough you consider for running the analysis: the borough of departure or the arrival one.
* When you are asked to run a statistical test, pay attention to the assumptions that must hold to run it. E.g. do the sample distributions have a bell shape? (Visually is enough!)
* For any statistical test you run, you must provide the test hypothesis and clearly say if the null hypothesis is rejected or not.

____

# Research questions

### Exploratory Data Analysis
1. [__RQ1__]  *In what period of the year Taxis are used more?* Create a plot that, for each month, shows the average number of trips recorded each day. Due to the differences among New York zones, we want to visualize the same information for each boroughs. Do you notice any difference among them? Provide comments and plausible explanations about what you observe (*e.g.: what is the month with the highest daily average?*). 

2. [__RQ2__] *What are the time slots with more passengers?* Set your own time slots and discover which are those when Taxis drive the highest number of passengers overall New York and repeat the analysis for each borough. Provide the results through a visualization and comment them. 

3. [__RQ3__] *Do the all trips last the same?* Let's put our attention on the distribution of trip's duration. Provide a plot for it and comment what you see. Run this analysis for NYC and for each borough (and obviously comment the results!). 

4. [__RQ4__] *What is the most common way of payments?* Discover the way payments are executed in each borough and visualize the number of payments for any possible means. Then run the [*Chi-squared test*](http://learntech.uwe.ac.uk/da/Default.aspx?pageid=1440) to see whether the method of payment is correlated to the borough. Then, comment the results.

5. [__RQ5__] *Does a long distance correlate with the duration of the trip on average?* Make a plot that show the dependence between distance and duration of the trip. Then compute the [Pearson Coefficient](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient), is it significant? Comment the results you obtain.

### Core Research Questions
____
#### What you need to look at before 
To assess whether the difference among two distributions is [statistically significant](https://en.wikipedia.org/wiki/Statistical_significance), you should run a statistical test. Here useful link to get know of a statistical test: [link 1](https://towardsdatascience.com/inferential-statistics-series-t-test-using-numpy-2718f8f9bf2f), [link 2](https://machinelearningmastery.com/parametric-statistical-significance-tests-in-python/).
____
1. [__CRQ1__]: *Does the fare for mile change across NY's borough?* We want to discover whether the expenses of a user that enjoys Taxis in one zone is different from those that uses it in another one.
    * Considering the fare amount:
		- Compute the price per mile ![equation](https://latex.codecogs.com/gif.latex?P) for each trip.
        - Run the mean and the standard deviation of the new variable for each borough. Then plot the distribution. What do you see?
        - Run the t-test among all the possible pairs of distribution of different boroughs.
        - Can you say that statistically significant differences, on the averages, hold among zones? In other words, are Taxis trip in some boroughs, on average, more expensive than others? 
    * The price per mile might depend on traffic the Taxi finds on its way. So we try to mitigate this effect:
        - Likely, the duration of the trip says something about the city's congestion, especially if combined with the distances. It might be a good idea to weight the price for mile using the time ![equation](https://latex.codecogs.com/gif.latex?T) needed to complete the trip. Thus, instead of ![equation](https://latex.codecogs.com/gif.latex?P), you can use ![equation](https://latex.codecogs.com/gif.latex?P'&space;=&space;\frac{P}{T}), where ![equation](https://latex.codecogs.com/gif.latex?T) is the time needed to complete the trip.
        - Run the mean and the standard deviation of the new variable for each borough. Then plot the distribution. What do you see?
        - Run the t-test among all the possible pairs of new distribution of different boroughs.
        - Can you say that statistically significant differences, on the averages, hold among zones? In other words, are Taxis trip in some boroughs, on average, more expensive than others?            
    * Compare the results obtained for the price per mile and the weighted price for mile. What do you think about that?
    
2. [__CRQ2__]: *Visualize Taxis movements!* NYC is divided in many Taxis zones. For each yellow cab trip we know the zone the Taxi pick up and drop off the users. Let's visualize, on a [chropleth map](https://en.wikipedia.org/wiki/Choropleth_map), the number of trips that starts in each zone. Than, do another map to count the races that end up in the single zone. Comment your discoveries. To perform this task we use the library [`folium`](https://github.com/python-visualization/folium). You find some examples of chorophlet maps [here](https://nbviewer.jupyter.org/github/python-visualization/folium/blob/master/examples/Colormaps.ipynb) and [__here__](https://medium.com/@austinlasseter/using-folium-to-generate-a-simple-map-of-your-pandas-data-87ddc5d55f8d). The `Geojson` we use to trace the zones is `taxi_zones.json` in the Homework's repository.

![alt text](http://dylanbabbs.com/map-data-viz-design/header.png "Logo Title Text 1")

### Tips
For any request:
1. Focus on a single month, performing all your analysis over a single dataset.
2. Repeat the same analysis on the other months.
3. Combine the results!

### Bonus
1. Repeat the entire analysis for other years (aggregating the results) then highlighting the differences you find among years.
2. Go further with the EDA (*Exploratory Data Analysis*) showing new interesting stuff about the dataset.
3. Make nice visualization using libraries like [Bokeh](https://bokeh.pydata.org/en/latest/) and [Seaborn](https://seaborn.pydata.org/).



# Winning-Space-Race-with-Data-Science

 <img src="https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/506294cf93cc570783dff8fb37c2b0e607285cc6/Images/space.gif" width="800" height="500">

## Author : [William Sousa](https://github.com/williamsousab) 

### This Project is the Applied Data Science Capstone Project of the IBM Data Science Professional Certificate

<p align='center'> 
<img src="https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Images/certifi.png" width= "200" height= "200"> 
</p>

# Project Description

In this project, we will predict if the Falcon 9 first stage will land successfully. SpaceX advertises Falcon 9 rocket launches on its website, with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is because SpaceX can reuse the first stage. Therefore if we can determine if the first stage will land, we can determine the cost of a launch. This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.



# Outline 

|       SL. NO        |                                    Outline                                      |
| :-----------------: | :-----------------------------------------------------------------------------: |
|          1          |                              [Executive Summary](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#executive-summary)                                 |
|          2          |                                 [Introduction](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#introduction)                                    |
|          3          |                                   [Objective](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#objective)                                     |
|          4          |                       [Hardware and Software Requirments](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#hardware-and-software-requirments)                         |
|          5          |                                  [Methodology](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#methodology)                                    |
|          6          |                  [Insights Drawn from Exploratory Data Analysis](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#insights-drawn-from-exploratory-data-analysis)                  |
|          7          |                        [Launch Sites Proximities Analysis](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#launch-sites-proximities-analysis)                        |
|          8          |                       [Build A Dashboard with Plotly Dash](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#build-a-dashboard-with-plotly-dash)                        |
|          9          |                       [Predictive Analysis (Classification)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#predictive-analysis-classification-1)                        |
|          10         |                                  [Conclusion](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/main/README.md#conclusion)                                     |


# Executive Summary

This project utilized various data collection methods, including web scraping and API calls, to analyze SpaceX launch data. Through Exploratory Data Analysis (EDA) and machine learning, the goal was to develop a classification model that predicts whether the Falcon 9 first stage will successfully land.


# Introduction

In the era of commercial space travel, reducing costs is crucial. SpaceX advertises its Falcon 9 rocket launches at a fraction of the cost of other providers, largely due to the reuse of the first stage. By predicting the success of these landings, companies can optimize their bids and potentially compete with SpaceX.


# Objective

## Background
 The project analyzes SpaceX’s launch data to explore how reusable rockets minimize launch costs and how these insights can be applied by other companies.

## Problem
 The key problem is predicting the landing success of the Falcon 9 first stage based on specific flight features.
 
## Question for Analysis
 - Can we predict the success of the Falcon 9 first-stage landing?
 - What features influence the success of these landings?


# Hardware and Software Requirments

## Hardware
The project uses Jupter Notebook on a local computer and IBM Cloud Pack for Data, requiring only a stable Internet connection.


## Software
- IBM Watson Studio
  For local execution:
- Programming Language: Python
- IDE: Jupyter Notebook
- Libraries/Packages: Pandas, Numpy, Scipy, Scikit-learn, Matplotlib, BeautifulSoup


# Methodology

## Data Collection
The data set used in the project is the [SpaceX Launch data](https://drive.google.com).

The data set contains information about different flights including date, launch site, booster version and more.

The data is collected by two main approaches:

1. The SpaceX API

2. Web Scrapping

### Data Collection – SpaceX API

We’ll be collecting launch data from SpaceX API, First we request launch data from SpaceX API using the GET command (requests.get), then we create a pandas dataframe from the response, After that we make several sub requests to get more detailed and consistent information about the IDs stored in the dataframe. 

With the help of some helper functions, we save the responses into a dictionary, and then we transform it into a dataframe, which is our data set.

 <img src= "https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/269bd7d192af30309dda882254a8e4050e8c9d19/Images/fluxo.png" width="1000" height="500">
 
### To see the code and step by step process of Data Collection using SpaceX API [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/jupyter-labs-spacex-data-collection-api-v2.ipynb)

### Data Collection - Web Scrapping

We will be performing web scraping to collect Falcon 9 historical launch records from a Wikipedia page. First we perform an HTTP GET( using requests.get command)method to request the Falcon9 Launch HTMLpage, as an HTTP response. Then we create a BeautifulSoup object from the HTML response, We extract the column names from the object and use it
as dictionary keys.

We parse the HTML tables and fill the dictionary keys with launch records from table rows, and finally we transform it into a dataframe.

<img src= "https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/12f1752d5225cce47a4299f8861918027637ec00/Images/fluxo02.png" width="1000" height="500">

### To see the code and step by step process of Data Collection with Web Scrapping [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/jupyter-labs-webscraping.ipynb)

## Data Wrangling

Exploratory data analysis is an important step while preprocessing data, it is useful to find some patterns in the data and determine what would be the label for training supervised models.

This process was done in the following order:

1. First thing to do is to identify the data types of the columns.

2. Determine the number of values for each attribute.

3. Calculate the percentage of the missing values.

4. To determine the label, weapply zero/one hot encoding to the “Outcome” column to classify landing to either 1(Success) of 0 (Failure)

### To see the code and step by step process of Data Wrangling [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/labs-jupyter-spacex-Data%20wrangling-v2.ipynb)

## EDA with SQL 

In order to better understand the datasets, we ran the following SQL queries:

1. Display the names of the unique launch sites in the space mission.

2. Display 5 records where launch sites begin with the string 'CCA'.

3. Display the total payload mass carried by boosters launched by NASA (CRS).

4. Display average payload mass carried by booster version F9 v1.1 .

5. List the date when the first successful landing outcome in ground pad was achieved.

6. List the names of the boosters which have success in drone ship and have payload mass greater than 4000 but less than 6000.

7. List the total number of successful and failure mission outcomes.

8. List the names of the booster versions which have carried the maximum payload mass. Use a subquery.

9. List the failed landing outcomes in drone ship, their booster versions, and launch site names for in year 2015.

10. Rank the count of landing outcomes (such as Failure (drone ship) or Success (ground pad)) between the date 2010-06-04 and 2017-03-20, in descending order.

### To see the code and step by step process of EDA With SQL [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/jupyter-labs-eda-sql-coursera_sqllite.ipynb)

## EDA with Data Visualization

In order to understand the relations between different features, we visualize the data by plotting scatter plots, bar charts and line charts, it helps finding hidden patterns in data and gain insights about the dataset.

1. Pay load mass against the Flight number.

2. Lunch site against the Flight number.

3. Lunch site against the Pay load mass.

4. Orbit type against Class success rate.

5. Flight number against Orbit type.

6. Orbit type against the Pay load mass.

7. Launch success yearly trend.

### To see the code and step by step process of EDA with Data Visualization [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/jupyter-labs-eda-dataviz-v2.ipynb)

## Build an Interactive Map with Folium

Here, we complete the interactive visual analytics using Folium.

First we create Folium map object, with an initial center location around Nasa Johnson space center, Houston-Texas.

 We add a circle on the map for each launch site from the dataset by creating a folium circle and folium marker, now the launch sites are marked on the map which means we can see which one is proximate to the equator line or close to a coastline.

 In order to mark the success/failure launches, we create a marker on the map for each launch record from the dataset, a green marker indicates a successful lunching and a red one indicates failure,

we need to explore and analyze the proximities of launch sites, we calculate the distance between the launch site and its proximities and then we draw a polyline between them.

### To see the code and step by step process of Build an Interactive Map with Folium [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/f7adb55f7c197ba708c8e015b5227b425176ba7e/Projects/lab-jupyter-launch-site-location-v2.ipynb)

# Build A Dashboard with Plotly Dash

* Plots/Graphs
1. Payload Mass Distribution: Histogram showing payload mass distribution across launches.
2. Launch Success Rates: Bar plot illustrating success rates by launch site.
3. Launch Trends Over Time: Line plot displaying the number of launches per year.

* Interactions
1. Year Filter: Allows users to filter data by specific years.
2. Hover Tooltips: Provides additional information on data points.
3. Zoom and Pan: Enables detailed views of specific plot areas.
4. To See the code for making the Dashboard using Plotly Dash [CLICK HERE] (https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/6c5b835744b0de9c3b9bf886846f16242fca1148/Projects/Create%20an%20interactive%20dashboard%20with%20Ploty%20Dash.ipynb)


### To See the code for making the Dashboard using Plotly Dash [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/6c5b835744b0de9c3b9bf886846f16242fca1148/Projects/lab-jupyter-launch-site-location-v2.ipynb) 


## Predictive Analysis (Classification)

Now that we finished the exploratory analysis, the next step is to determine the training labels and build a predictor using machine learning algorithms. After using the ‘Class’ column as the label, first thing to do is normalizing the data. We split the normalized data into test/train sets, The training data is divided into validation data, a second set used for training data.

For the model development phase, we use the following algorithms:

1. Logistic regression

2. Support vector machine

3. Decision trees

4. K nearest neighbor

We build a grid search object for each of the algorithms and f i t it to find the best parameters of the model(hyper parameters tuning), then we choose the most accurate model.

### To see the code and step by step process of Predictive Analysis (Classification) [CLICK HERE](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/6c5b835744b0de9c3b9bf886846f16242fca1148/Projects/SpaceX-Machine-Learning-Prediction-Part-5-v1.ipynb)

## Results

* Payload Mass Distribution: Normal distribution with some outliers.
* Launch Success Rate: Over 80% success rate, varying by site.
* Temporal Trends: Increasing number of launches over the years.
* Weather Conditions Impact: Adverse weather conditions correlate with launch failures.
* Rocket Specifications: Varying success rates among different rocket models.


# Insights Drawn from Exploratory Data Analysis

## Flight Number vs. Launch Site

Scatter plot of Flight Number vs. Launch Site

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/launch%20Site_vs_Flight%20Number.png)

It is possible to identify that the greater the number of flights, the more successful flights occur, unlike the first flights that have more failures.

The launch site with the most launches is CCAFS SLC 40.

## Payload vs. Launch Site

Scatter plot of Payload vs. Launch Site

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/payload%20Mass_vs_LaunchSite.png)

We observe that from a payload of 8,000 we see that there is a greater chance of a successful launch. 

Between 1,000 and 7,000 is the greatest amount of information.

## Success Rate vs. Orbit Type

Show a bar chart for the success rate of each orbit type

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/success_Rate_vs_Orbit_Type.png)

The ES-L1, GEO, HEO and SSO orbits have the highest success rates while GTO has the lowest success rate.

## Flight Number vs. Orbit Type

Show a scatter point of Flight number vs. Orbit type

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/flight%20Number_vs_Orbit.png)

The number of flights on the ISS, GTO are constant while the flights on the VLEO have been happening in the last records.

## Payload vs. Orbit Type

Show a scatter point of payload vs. orbit type

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/payload%20Mass_vs_Orbit.png)

VLEO has the flights with the largest payloads, There is a possibility that the heavier the payload, the higher the probability of success.

## Launch Success Yearly Trend

Show a line chart of yearly average success rate

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/success%20Rate%20Over%20the%20Years.png)

You can observe that the success rate since 2013 kept increasing till 2017 (stable in 2014) and after 2015 it started increasing.

## All Launch Site Names

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/exclusive.png)

These are the names of unique release locations, obtained from the sql databases.

## Launch Site Names Begin with 'CCA'

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/cca.png)

5 records where launch sites begin with the string 'CCA’.

## Total Payload Mass

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/total_payload.png)

The total payload mass carried by boosters launched by NASA (CRS)

## Average Payload Mass by F9 v1.1

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/f9.png)

Average payload mass carried by booster version F9 v1.1

## First Successful Ground Landing Date

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/16a30f3286df77df1e0b14a5c01c7daec9d3da18/Images/solo.png)

Date when the first successful landing outcome in ground pad was achieved.

## Successful Drone Ship Landing with Payload between 4000 and 6000

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/938e4eeacba2283e57b70496bc0052e81306f105/Images/booster_Version.png)

The names of the boosters which have success in drone ship and have payload mass greater than 4000 but less than 6000.

## Total Number of Successful and Failure Mission Outcomes

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/938e4eeacba2283e57b70496bc0052e81306f105/Images/booster.png)

The total number of successful and failure mission outcomes.

## Boosters Carried Maximum Payload

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/938e4eeacba2283e57b70496bc0052e81306f105/Images/lading.png)

The names of the booster versions which have carried the maximum payload mass.

## 2015 Launch Records

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/2015.png)

The records which will display the month names, failure landing outcomes in drone ship ,booster versions, launch site for the months in year 2015.

## Rank Landing Outcomes Between 2010-06-04 and 2017-03-20

![Screenshot (189)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/lading.png)

Count of landing outcomes (such as Failure (drone ship) or Success (ground pad)) between the date 2010-06-04 and 2017-03-20, in descending order.

# Launch Sites Proximities Analysis

## Launch sites Marking

The markers on this maps show the launch site locations on the map.

![Screenshot (192)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/01map.png)

## Mark the success/failed launches for each site on the map

The green marker means a successful landing and the red one is an unsuccessful landing.

![Screenshot (193)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/02map.png)

## Distances between a launch site to its proximities

Distance from the launch site to the nearest highways, railways, coastline and city.

![Screenshot (194)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/03map.png)

## Launch Success Dashboard for All Sites

Count of successful launches for all sites in a pie chart.

![Screenshot (199)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/all.png)

## Launch site with the highest success rate

KSC LC-39A has the highest launch success rate.

![Screenshot (201)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/all02.png)

## Scatter plot with different loads

![Screenshot (201)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/a1525b07e04ffc332ef19b0d9b6c5eca80339a2c/Images/carga.png)

# Predictive Analysis (Classification)

## Classification Accuracy

![Screenshot (201)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/34d69e19f42a3ce01c299b65071abdeae81627e9/Images/modelbarras.png)

Accuracy of the models created.

All demonstrated the same accuracy.

## Confusion Matrix

![Screenshot (202)](https://github.com/williamsousab/Winning-Space-Race-with-Data-Science/blob/34d69e19f42a3ce01c299b65071abdeae81627e9/Images/confuso.png)

All models performed equally well and formed the same confusion matrix.

# Conclusion

* Our analysis of SpaceX rocket launches brought several interesting insights. Here are some of the main conclusions:

* Payload Mass Distribution:

The distribution of payload mass followed a normal distribution with some outliers, suggesting that most launches fall within a specific range of masses.

* Launch Success Rate:

The success rate of the launches was over 80%, but it varied depending on the launch site. This indicates that some locations may have better conditions or infrastructure for successful launches.

* Temporal Trends:

We observed an increase in the number of launches over the years, reflecting the growing activity and demand for space launches.

* Machine Learning Models:

We used Logistic Regression and Support Vector Machines (SVM) to predict the success of the launches. Both models showed similar accuracy, around 83%, on the test set, indicating that they are effective for this type of prediction.

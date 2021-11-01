## Predict Local Epidemics Of Dengue Fever: Midterm Report
#### Lu Cao, Elva Gao, Kinya Wang

### Data Set Summary: 
We used the Dengue Fever data from [Drivendata.com]( https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/). The data were provided in four different files, including one file consisting of features' data and one file consisting the number of dengue cases for each row in the feature file. We will be using those two files extensively as the other two files are related to competition submission format. 
Before we start data cleaning process, we looked at the two files more in details. 

The features dataset includes data that can be categorized into four groups: 
* ***City and data indicators*** which includes **City** (categorical data) and **Week Start Date** (in abbrev. number format)
* ***NOAA's GHCN daily climate data weather station measurements*** which includes five different features that corresponds to the maximum and minimum value, average and also the range of temperature as well as total precipitation
* ***Persiann satellite precipitation measurements*** includes one feature which is **Precipitation_amt_mm**, representing the total precipitation. 
* ***NOAA's NCEP Climate Forecast System Reanalysis measurements*** includes 10 different features that corrsponds to total precipitation (unit: amt_mm_, mean dew point temperature, mean air temperature, mean relative and specific humidity, total precipitation (unit: kg/m^2), max and minimum air temperature and diurnal temperature range. 
* ***Satellite vegetation - Normalized difference vegetation index (NDVI) - NOAA's CDR Normalized Difference Vegetation Index (0.5x0.5 degree scale) measurements*** includes four features that individually corresponds to the southeast, southwest, northeast and northwest of city centroid. 
All of the features that are mentioned above, unless stated, are in numerical form.

The label dataset includes four columns which include 
* **City** - categorical data representing different cities
* **Year** - an integer between 1990 and 2010; it denotes the year that the data is recorded
* **Week Of Year** - an integer ranging from 1 to 53; it denotes the number of week in the year that the data is been recorded
* **Total Cases** - an integer denoting the number of cases 

We noticed that the data are for two different cities, noted as sj and iq, representing San Juan and Iquitos. Thus, we will be looking into the data corresponding to the individual city. 

### Data Cleaning
* All variables were casted to appropriate types: categorical feature like the name of the city was one-hot encoded.
* Imputed missing values based on the average of the previous and next values
* Dropped the column of "week_start_date" as this is a redundant information since we have both year and weekofyear as features.

### Exploratory Analysis & Visualisations
We started the analysis with look over the trends of different features. First we started with checking if the disease has seasonality. 
These two line graphs show the trends of disease outbreak in sj and iq.    
<img src="https://user-images.githubusercontent.com/57336981/139634017-eb44bc07-2604-4233-8780-f13869136219.png" width="500" height="300" /> 
<img src="https://user-images.githubusercontent.com/57336981/139634081-f416d5b7-7228-4b5d-856a-fd764d3f7231.png" width="500" height="300" />  
 &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;(fig1: trend of outbreak time of the year in San Juan) &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;(fig2: trend of outbreak time of the year in Iquitos)      
From the two graphs that are shown above, both shown a similar trend, with San Juan's more obvious, that the Dengue Fever outbreaks during the first 10 weeks and also the last 15-20 weeks of the year. 
In order to see trends from other presepctives, we then created box plot for each city, denoting the trend of Dengue fever outbreak over the years.   
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<img src="https://user-images.githubusercontent.com/57336981/139634713-fdb708f5-042a-4fb3-b9f3-73a75f696957.png" width="400" height="300" />  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
<img src="https://user-images.githubusercontent.com/57336981/139634759-e737db0f-c343-4a22-876b-578abf1d77eb.png" width="400" height="300" />   
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;(fig3: trend of outbreak over the year in San Juan)  &nbsp; &nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (fig4: trend of outbreak over the year in Iquitos)   
With the goal of understanding what might be a determining factor of causing the local Dengue Fever, we created a heatmap to further examine the correlation between different features. 
 <img src="https://user-images.githubusercontent.com/57336981/139689303-9d56b2f2-f67b-4403-9ded-538502d03dbe.png" width="600" height="600" /> 







### Validation and Next Steps

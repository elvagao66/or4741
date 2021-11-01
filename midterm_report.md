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

### Cleaning & Null Data















### Validation and Next Steps

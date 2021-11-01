# Predict Local Epidemics Of Dengue Fever: Midterm Report
#### Lu Cao, Elva Gao, Kinya Wang

## 1. Data Set Summary: 
We used the Dengue Fever data from [Drivendata.com]( https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/). The data were provided in four different files, including one file consisting of features' data and one file consisting the number of dengue cases for each row in the feature file. We will be using those two files extensively as the other two files are related to competition submission format. 
Before we start data cleaning process, we looked at the two files more in details. 

The features dataset includes data that can be categorized into four groups: 
* ***City and data indicators*** : which includes `city` (categorical data) and  `week_start_date` (in abbrev. number format).
* ***NOAA's GHCN daily climate data weather station measurements***: which includes five different features that corresponds to the maximum and minimum value, average and also the range of temperature as well as total precipitation.
* ***Persiann satellite precipitation measurements***: which includes one feature which is `precipitation_amt_mm`, representing the total precipitation. 
* ***NOAA's NCEP Climate Forecast System Reanalysis measurements***: which includes 10 different features that corrsponds to total precipitation (unit: amt_mm_, mean dew point temperature, mean air temperature, mean relative and specific humidity, total precipitation (unit: kg/m^2), max and minimum air temperature and diurnal temperature range. 
* ***Satellite vegetation - Normalized difference vegetation index (NDVI) - NOAA's CDR Normalized Difference Vegetation Index (0.5x0.5 degree scale) measurements***: which includes four features (`ndvi_ne`, `ndvi_nw`, `ndvi_se`, `ndvi_sw`) that individually corresponds to the southeast, southwest, northeast and northwest of city centroid. 
All of the features that are mentioned above, unless stated, are in numerical form.

The label dataset includes four columns which include:
* `city` - categorical data representing different cities
* `year` - an integer between 1990 and 2010; it denotes the year that the data is recorded
* `weekofyear` - an integer ranging from 1 to 53; it denotes the number of week in the year that the data is been recorded
* `total_cases` - an integer denoting the number of cases 

We noticed that our dataset include information about two different cities, San Juan and Iquitos. We will compare the similarity and difference of data distribution of the two city to decided whether we could use one general model to make prediction

## 2. Data Cleaning
* All variables were casted to appropriate types: categorical feature like the name of the city was one-hot encoded. 
* Imputed missing values based on the average of the previous and next values
* Dropped the column of `week_start_date` as this is a redundant information since we have both year and `weekofyear` as features.

## 3. Exploratory Analysis & Visualisations
We started the analysis with look over the trends of different features. First we started with checking if the disease has seasonality. 
These two line graphs show the trends of disease outbreak in sj and iq.    
<img src="https://user-images.githubusercontent.com/57336981/139756207-254f9a05-4627-462e-a971-cac90ad69d45.png" width="500" height="400" /> 
<img src="https://user-images.githubusercontent.com/57336981/139756259-de4637cb-7f7a-4957-9f12-1ac34e518842.png" width="500" height="400" />  

Both of the graphs shown above indicate that there exist some seasonality in number of cases increased per week as cases tend to be higher in the first and last few weeks of the year in comparison the middle of the year. 
However, the trend variates between the two city. 
 1. San Juan 
   * has a larger number of cases on average
   * relatively small Dengue Fever outbreak happens around the first 10 weeks of the year
   * more severe outbreak happens around the 35-50 weeks of the year
 2. Iquitos
   * has a smaller number of cases on average
   * same lever of Dengue Fever outbreak happens during the first 10 weeks and last 15 weeks of the year.      

<img src="https://user-images.githubusercontent.com/57336981/139756311-61cd0f10-c367-407a-9736-98c4ab5cd41c.png" width="480" height="350" /> <img src="https://user-images.githubusercontent.com/57336981/139756350-7cd7d082-4ae7-45df-ad51-50f651193cd5.png" width="480" height="350" />   
The two graphs above reveal how the distribution of number of cases each year changed over time. We can observe that the number of cases tend to decrease over time in San Juan while showing a increase trend in Iquitos. At the same time, the number of cases increased each month tend to spread out more and has more skewnedd in San Juan in comparison to Iquitos. The above observation indicates that there are different pattern of Denque Fever in San Juan and Iquitos. Thus, we decided to train a model for each of the two cities. 
With the goal of understanding what might be a determining factor of causing the local Dengue Fever, we created a heatmap to further examine the correlation between different features.   
 <img src="https://user-images.githubusercontent.com/57336981/139756391-1d8975d7-20aa-4ef7-9e4c-981e35e974d6.png" width="500" height="500" /> 
 <img src="https://user-images.githubusercontent.com/57336981/139756435-680f24e0-6162-4fea-864b-63e5776be3b2.png" width="500" height="500" />        
Observation: Satellite vegetation indices (ndvi_ne, ndvi_nw, ndvi_se, ndvi_sw) are highly correlated to temperature features (reanalysis_air_temp_k, reanalysis_avg_temp_k).Total cases from both cities are related to the weather (described by features including average temperature and humidity), however, different from our expectation, aren't highly correlated to any of the features that are being examined. 

## 4. First Models
We first trained a linear regression using OLS on the total cases and city features with one hot encoding for nominal features. We applied the model onto both cities. The iq data set had the smallest eigenvalue as 1.34e-26 and the sj data set had the smallest eigenvalue as 2.93e-25.   

Our interpretation and hypothesis of the results:  
1. For iq, its smallest eigenvalue might indicate that there are strong multicollinearity problems or that the design matrix is singular.
2. Both standard Errors in the two outcomes assume that the covariance matrix of the errors is correctly specified.
3. For sj, its smallest eigenvalue is 2.93e-25 which might indicate that there are strong multicollinearity problems or that the design matrix is singular. 
4. R^2 is the coefficient of determination that tells us that how much percentage variation independent variable can be explained by independent variable. Here, ～20% variation in the total cases data can be explained by the features that are listed. The maximum possible value of R2 can be 1, means the larger the R2 value the better the regression.

As we noticed that there can be further improvements.

## 5. Validation and Next Steps
* Next, we plan on to evaluate models using k-fold cross validation to ensure the result that is produced by a model isn't biased due to how the data has been categorized.
* Engage feature selection in order to reduce variability of data as well as making data conform to normality. As the values of r-squred aren't as significant as we have expected, we want to further examine whether we should take all 21 dependent variables into account. For example, we might can check the p-value or compare anova test for feature selection
* Apply feature transformation in order to reduce variability of the data and make data conform to normality. 
* Implement random forest decision tree for limitting overfitting without substantially increasing error due to bias.

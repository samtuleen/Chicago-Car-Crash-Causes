# Chicago Car Crashes: Analyzing the Causes of The City's Traffic Accidents

## By: Sameeha Ramadhan

The goal of this analysis is to examine and determine what causes injury resulting car accidents in the city of Chicago. The data used are the Chicago Car Crash datasets and is processed and filtered to reflect crashes that occured in 2021 alone.

I will be using data from the City of Chicago website to build a classification model that can help predict why car accidents occur, as well as identify a number of trends from the accidents. Doing so can aid the city in taking the correct measures to help prevent accidents, and their resulting injuries, from occurring.

If the City of Chicago successfully implements my recommendations, the city should see a decrease in injuries and fatalities, improved flow of traffic, and an overall increase in safety on its roads.


## Data

The data used was sourced from the City of Chicago official website. The following three datasets were used, namely "Traffic Crashes - Crashes", "Traffic Crashes - Vehicle", and "Traffic Crashes - People". 

The datasets can be found here along with their column names and descriptions.

Traffic Crashes - Crashes: https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if

Traffic Crashes - Vehicles: https://data.cityofchicago.org/Transportation/Traffic-Crashes-Vehicles/68nd-jvt3

Traffic Crashes - People: https://data.cityofchicago.org/Transportation/Traffic-Crashes-People/u6pd-qa9d


## Process: OSEMiN (OSEMN)

### Obtain:

* Extracting the data from the following files:
Traffic Crashes - Crashes = https://data.cityofchicago.org/resource/85ca-t3if.csv
Traffic Crashes - Vehicle = https://data.cityofchicago.org/resource/68nd-jvt3.csv
Traffic Crashes - Person = https://data.cityofchicago.org/resource/u6pd-qa9d.csv


### Scrub:

* Explored the raw data and understood the values
* Identified the null values and implemented the best steps to take to eliminate them
* Replaced values with meaningful data and converted data types
* Deleted irrelevant and redundant columns


### Explore:

* Created visualizations to better read and understand the data
* Engineered new columns from binning and mapping
* Obtained important statistics from the data


### Model:

* Built multiple models including Logistic Regression, Decision Trees, K-Nearest Neighbors (KNN), Random Forest
* Performed a gridsearch on each model to extract the best parameters


### iNtrepret:

* Evaluated the accuracy score which produced our Logistic Regression model as the best model



 ## Results
 
I began by merging the three datasets into one, which resulted in a dataframe with a shape of 149 columns and 1,147,852 rows. I then calculated the null values in each column and removed any that had over 95% of missing data, resulting in a dataframe with only 83 columns. I then reviewed the description of each column on the cityofchicago.org website and proceeded to remove the remaining irrelevant columns.


Next, I either remapped or created bins of a number of columns, including, but not limited to,: crash_hour, age, and airbag_deployed.


### Target

I've chosen  the 'injuries_total' column (renamed to 'injuries') as the target and converted the data to the following: '1' if the crash resulted in an injury and '0' if no injuries occured.


### Preprocessing

I began by running a train-test-split to check for data leakage. After exploring the data, there were no more numerical columns so I proceeded with preprocessing the categorical columns. I've created a pipeline and passed the columns through SimpleImputer to fill empty values with 'MISSING', and then OneHotEncoded them to scale the data to a binary column.

### Models

I've tested the following models: Logistic Regression, Decision Trees, KNN (K-Nearest Neighbors), and Random Forest.

My Logistic Regression model produced accuracy rate of 92%. The confusion matrix displays that when the model predicted 0 (no injuries) and the result was no injuries, the model was correct 81% of the time, and when predicting 1 (injury) and the result was injury, it was correct 96% of the time.
<img width="455" alt="log_reg_test" src="https://user-images.githubusercontent.com/71333855/117534459-2cc64780-afb7-11eb-9b95-f5aa97604b11.png">



## iNterpretation

I plotted the chart below by extracting the 'feature_importance' from the bagging classifier.
![feature_importance](https://user-images.githubusercontent.com/71333855/117534431-0e604c00-afb7-11eb-8e28-d44a463e9493.png)


The most important observation from this chart is that most car accidents involve drivers colliding with non-motor vehicular travelers (pedestrians and cyclists). 

Also, the vehicle_type column could help inform which type of vehicles are most likely to get into a traffic accident, however a significant amount of information is missing.


Another interesting observation is that the majority of accidents occur in speed zones over 25mph and under 45mph, as displayed in the figure below:
![speed_limit_bins](https://user-images.githubusercontent.com/71333855/117534408-eec92380-afb6-11eb-8039-c3deef43b25a.png)


Additionally, the majority of severe car crashes occur during rush hour:
![time_bins_injuries](https://user-images.githubusercontent.com/71333855/117534417-f983b880-afb6-11eb-9ec0-45f35ddf87dd.png)


And most occur on Saturdays:

![crash_day_injuries](https://user-images.githubusercontent.com/71333855/117534425-01435d00-afb7-11eb-9f27-5d227e8b6a15.png)


## Conclusion:

Since our Logistic Regression model turned an accuracy rate of 92%, I am confident in the following conclusions:

* The injuries that that seem to result from accidents the most are **collisions between drivers and pedestrians or cyclists.**
* Accidents and injuries occur most often ***in the presence of traffic signals.***
* The majority takes place in the **afternoon or during rush hour as well as on Saturdays.**
* Most occur in speed limit zones between 30-40 mph.

## Recommendations:

**The city install more cyclist friendly lanes and designated pedestrian walking areas.**

**Pedestrians and cyclists should be required to wear bright or reflective clothing when traveling at night and in poorly lit areas.**

**Rush hour speed limits could be lowered.**

**The city could plan to expand two way roads to include a median/divider to reduce the possibility of wrong way driver collisions**

**More patrol offered in areas with speed zones that are prone to more accidents.**

**More classes can be offered in regards to driving safety to further teach drivers how to be aware of their surroundings, obey traffic laws, and control road rage.**

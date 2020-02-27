# IITMadras_Sangam_ML_2019_Challenge_4th_Place
This repository contains solution for Sangam IITMadras Machine Learning Challenge 2019. Placed 4th in this event on hackerearth platform.

Challenge link: https://www.hackerearth.com/challenges/competitive/IIT-Madras-Sangam-ML-Hackathon-2019/?utm_source=challenges-modern&utm_campaign=participated-challenges&utm_medium=right-panel

### Preprocessing Steps:

1)	In order to extract meaningful inferences from date_time column, it was converted to datetime format.

2)	Columns like rain_ph and snow_ph had numerical value 0 whereas their corresponding weather_type or weather_description had rain/snow details hence for such values mean imputation of the particular categorical variable i.e. (weather_type or weather_description) was used to replace such zeros.

3)	In the given dataset for both train and test, in the is_holiday column, every holiday was populated for only 0th hour hence as a preprocessing step we populated the same holiday to rest of the 23 hours for the day.

### Feature Engineering: 
	
  Here is the list of features used and their brief description:

#### 1)	Date Time features:

These features are extracted from date_time column.

a.	hour: contains hour of every data record. 

b.	month: contains month to which corresponding data record belongs to. 

c.	day of week: tells what day of week i.e. (Monday, Tuesday, etc.) it was for every data record date.

#### 2)	Boolean Features:

a.	is_weekend_boolean: this feature tells if the data record corresponds to a weekend (Saturday and Sunday) day or not. 

b.	is_holiday_boolean: this feature tells if the corresponding data record is from a day which was a Holiday or not.

#### 3)	Target encoding/ Mean encoding features:

From a mathematical point of view, mean encoding uses the concept of conditional averaging where average of your target variable, is calculated conditional on each unique value of the feature.
Such features give an intuition an average as to what was the trend of output variable with respect to each unique value of a categorical variable.

•	One level Target Encoding: Only one categorical variable is taken at a time.

i.	is_holiday_mean_encoding: this feature calculates conditional average of traffic_volume for each record on being a holiday or not.

ii.	day_of_week_mean_encoding: this feature calculates conditional average of traffic_volume for each day of the week i.e. (Monday, Tuesday, etc.) in the past.

iii.	weather_type_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different values of weather type i.e. (Clouds, Clear, etc.) in the past.

iv.	weather_description_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different values of weather description i.e. (scattered clouds, sky is clear, etc.) in the past.

•	Two level Target Encoding: Two categorical variables are taken at a time.

i.	hour_weather_type_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different possible combination of values of hour and weather type i.e. (0th hour-Clouds, 1st  hour-Clear, etc.)
This feature gives an intuition that at a particular hour and with a particular weather type what was the average traffic volume in the past.

ii.	hour_day_of_week_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different possible combination of values of hour and day of week i.e. (0th hour-Monday, 1st  hour-Monday, etc.)
This feature gives an intuition that at a particular hour and for a particular day of week what was the average traffic volume in the past.

iii.	 month_weather_description_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different possible combination of values of month and weather_description i.e. (January-scattered clouds, February-sky is clear, etc.)
This feature gives an intuition that for a particular month and for a particular weather description as in seasonality what was the average traffic volume in the past.

•	Three level Target Encoding: Three categorical variables are taken at a time.

i.	day_of_week_hour_weather_type_mean_encoding: this feature calculates conditional average of traffic_volume with respect to different possible combination of values of day of week, hour and weather_type i.e. (Monday-0th hour-Clouds, Tuesday-0th hour-Clear, etc.)
This feature gives an intuition that for a particular day of week at every hour for a particular weather type what was the average traffic volume in the past.


#### 4)	Shift Features: 

Shift or lag features are the classical way that time series forecasting problems are transformed into supervised learning problems where the approach is to predict the value at the next time (t+1) given the value at the previous time (t-1)

a.	weather_type_mean_encoding_1lag: One level conditional average value of weather type is shifted by 1 hour which creates a new time series with 24 hours of lag values to predict the current observation of mean traffic volume.

b.	weather_type_mean_encoding_2lag: One level conditional average value of weather type is shifted by 2 hour which creates a new time series with 24 hours of lag values to predict the current observation of mean traffic volume.

#### 5)	Raw features:

Few raw columns that were considered as features and were used as is were:

a.	temperature
b.	wind_direction 
c.	humidity
d.	visibility_in_miles
e.	dew_point    

#### 6)	Other Features:

a.	no_of_days_till_next_holiday: this numerical feature tries to capture number of days remaining for the upcoming holiday which includes both weekends and festival. Trends in the dataset suggest that traffic volume is likely to go up just a few days before a holiday.

b.	no_of_days_till_next_festival: this numerical feature tries to capture number of days remaining for the upcoming festival. Trends in the dataset suggest that traffic volume is likely to go up just a few days before a festival.
This was the exhaustive list of features that were considered for modelling but best set of features were selected using feature selection techniques.





#### Feature Selection

In order to decide best set of the features for the model various techniques were implemented, few of them are mentioned below:

a.	Correlation metric
b.	Forward feature selection
c.	Group Variation Inflation Factor (Group VIF)
d.	Feature selection using genetic algorithm

#### Modelling

We have used ensemble technique to improve predictive performance of our model as compared to a single model by bagging the predictions from two tree-based model algorithms i.e. Random Forest Regressor and LightGBM Regressor.

#### Hyperparameter Tuning

We have used several techniques to determine optimal set of parameters for learning algorithm:

a.	GridSearchCV from scikit-learn.
b.	Scikit-Optimize 


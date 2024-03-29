# New_York_Taxi_Deamand_Prediction
<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/pic1.jpg width = 1000>

# Business Objective:
Objective of this case study is to predict the number of pickups in 10 minute interval in a region 

## Data Information:
<p>
Ge the data from : http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml (2016 data)
The data used in the attached datasets were collected and provided to the NYC Taxi and Limousine Commission (TLC) 
</p>


# ML Problem Formulation
We need to understand the business objective and constraints very clearly to carve out the formulation of problem.
The end user would be a cab driver,probably using an app on smartphone.

__OBJECTIVE__:

-  to predict the number of pickups in a particular region for a 10 minutes interval 

__CONSTRAINTS__:

- Time latency: cab driver expect the application to tell the number of pickups in few seconds only,they will not wait for hour or so to know the number of pickups in the region.

- Interpretability : is not very important because our end user will not be interested in working of the model but in its results.

- We need to keep in mind that in such scenarios relative errors are more important than absolute errors
## Performance metrics
1. Mean Absolute percentage error.
2. Mean Squared error.


## Approach
we clustered the data using segmentation i.e by using the latitude and longitude of pickups and then broke the regions using daily pickups in 10 min interval ,the strategy we used here for clustering the data was that we wanted minimum inter cluster distance to be 0.5 and maximum cluster distance to be 2 miles as that's how much a taxi travels with average speed in a 10 min interval,also we smoothed the data as for intervals where number of pickups tend to be zero we imputated the average over interval values

If we notice carefully some 10 minute intervals has 0 pick ups. 0 is not very relevant when we train the model. So instead of keeping those values as it is, we will smooth them. The process is as follows. We have time binned regions of 10 minute intervals. Let's take three continuos intervals and let's say each of the intervals have 50,100 and 0 pickups respectively. Instead of taking 0 as the third value we will take the take the average of all the values and distribute it in the three regions as 50,50,50. In this way, each 30 minute interval will have the same number of pickups even though the pickups values changes in each of the three 10 minute interval.
<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/cluster_regions.JPG height = 400>

__Time Series Feature engineering__ : In the below graph, we can see repeated patterns like each day the number of cabs are highest during the office hours. It's least during midnight and increases as the day progresses. It decreases during noon time. Then again starts increasing during evening time. We will explore all such data dependendies using Fourier transformed features.
Fourier transform generally means decomposition of a wave into sum of multiple sine waves. Whenever there is are repeated patterns in data, we can leverage the most out of them by using Fourier transform. Using fourier transform we can decompose any given waveform(or a function) into it's constituent frequencies. The graph obtained after fourier transform will have unique frequencies and amplitudes corresonding to their most frequent occurences in the original wave.
<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/fourier.PNG>


Then we used __High band pass filter + Wavenet denosing along with Holt's exponential smoothening__ as part of feature extracting process.<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/graph.png>

## Modelling :I used 6 models for forecaasting -
  - __Baseline Models__:
      - Simple Moving Averages
      - Weighted Moving Averages
      - Exponential Moving Averages 
   - __Other Models__:
      - Linear Regression hypertuned using GridSearchCV
      - Random Forests hypertuned using RandomSearchCV
      - XGBRegressor hypertuned using RandomSearchCV
## Results:
<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/res1.PNG>
<img src = https://github.com/yatscool007/New_York_Taxi_Deamand_Prediction/blob/master/Images/res2.PNG>

### I achieved the best MAPE with XGBRegressor - 0.0875

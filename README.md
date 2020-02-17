# New_York_Taxi_Deamand_Prediction

## Business Objective:
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

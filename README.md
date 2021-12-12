# PyBer_Analysis
This is a training program.
The purpose of this project is to create a summary DataFrame of the ride-sharing data by city type.
Pandas and Matplotlib is used to create a multiple-line graph that shows the total weekly fares for each city type.
Two data resources(city data & ride data) are used in this project.
Deliverable Requirements:

The total number of rides for each city type is retrieved by the below code:
```
count_rides_by_type = pyber_data_df.groupby(["type"]).count()["ride_id"]
```

The total number of drivers for each city type is retrieved.
```
sum_drivers_by_type = city_data_df.groupby(["type"]).sum()["driver_count"]
```
The sum of the fares for each city type is retrieved.
```
sum_fares_by_type = pyber_data_df.groupby(["type"]).sum()["fare"]
```
The average fare per ride for each city type is calculated.
```
avg_fare_by_type=pyber_data_df.groupby(["type"]).mean()["fare"]
```
The average fare per driver for each city type is calculated.
```
avg_driver_fare_by_type=sum_fares_by_type/sum_drivers_by_type
```
A PyBer summary DataFrame is created.
```
pyber_summary_df=pd.DataFrame(
    {'total rides': count_rides_by_type,
     'total drivers':sum_drivers_by_type,
     'total fares':sum_fares_by_type,
     'average fare per ride':avg_fare_by_type,
     'average fare per driver':avg_driver_fare_by_type})
```



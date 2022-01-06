# PyBer  Analysis
The purpose of this training project is to analyze PyBer ride-sharing data for each city type. Pandas & Matplotlib are used in this project.

There are two data resources csv formats; city data  & ride data. First of all, we made pandas DataFrame of each resources by the below code;

	 city_data_df = pd.read_csv(city_data_to_load)
	 ride_data_df = pd.read_csv(ride_data_to_load)

Then they are merged together to make one complete data resource.

	 pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])

##  Summary DataFrame
There are three kinds of city; 
			-	Urban
			-	Suburban
			-	Rural
	
###  Technical summery
In this part, PyBer data is analyzed based on number of rides, number of drivers & total fares for each city as follow codes;

	 - total_ride_type = pyber_data_df.groupby(pyber_data_df["type"])["ride_id"].count()
	 - total_driver_count_type = city_data_df.groupby(city_data_df["type"])["driver_count"].sum()
	 - total_fare_type = pyber_data_df.groupby(pyber_data_df["type"])["fare"].sum()
###   summery
Urban areas has greatest number of rides and drivers while Rural areas have the least number of rides and drivers. The number of rides in Urban area is 1,625, in Suburban cities is 625 and in Rural cities is 125 and also the number of drivers in Urban cities is 2,405, in Suburban cities is 490 and in Rural cities is 78.
PyBer earned about $39,854  from fares of urban areas, about $19,356 from fares of suburban area and $4,327 from fares of rural areas.
###  Technical summery
The below codes is used to calculate average fare per ride and average fare per driver for each city type:

	 - avg_fare_type=total_fare_type/total_ride_type
	 - avg_fare_driver=total_fare_type / total_driver_count_type

###   summery
The above calculation shows that when the number of rides and number of drivers are increased, the average  fare will be decreased. Therefore,  the average of fares per ride and  per driver in rural areas are more than suburban and urban areas.

## The total weekly of the fares for each type of city.
In this part, we try to prepare new data frame to show the sum of the fares based on date and city types. "groupby" function is used to show the data of our date & type. the below code is used;

	 - fare_type_date=pyber_data_df.groupby(["date","type"])["fare"].sum()

Then,  the pivot table is used to create a data frame with  "date" as the index, "city types" as the columns, and "fares" as the values. we make it by the below code;

	 - type_date_fare= pyber_data_df.pivot_table( index="date",columns="type", values="fare")

Next, we use .loc() function to filter the date from ("2019-01-01" : "2019-04-28");

	 - date_specific = type_date_fare.loc["2019-01-01":"2019-04-28"]

Moreover, we  create a new DataFrame using the resample() function by week and get the sum of the fares for each week.

	 - date_specific_resample = date_specific.resample('W').sum()

As a result, we have the new DataFrame with date as index, city types as columns.
The DataFrame shows that the maximum  fare of urban area is about $2,471 in 2019-03-10, in suburban area; it is about $1,413 in 2019-02-24 and  in rural area; it  is about $501 in 2019-04-07.

## Line chart

In this part, we use object-oriented method to create line chart for each city type.


![PyBer_fare_summary](https://user-images.githubusercontent.com/91231253/144645132-3a1eb977-df66-4b9a-bed4-264159ffadaa.png)


the below code is used to create the chart;

	 - plt.style.use('fivethirtyeight')
	 - fig, ax = plt.subplots(figsize=(50, 20))
	 - ax.plot(date_specific_resample ['Rural'], label="Rural" , color='blue')
	 - ax.plot(date_specific_resample['Suburban'],label="Suburbam" , color='red')
	 - ax.plot(date_specific_resample['Urban'], label="Urban" , color='gold')
	 - ax.set_title('Total fare by City Type',fontsize="40")
	 - ax.set_xlabel('Month',fontsize="40")
	 - ax.set_ylabel('Fares ($USD)',fontsize="40")
	 - ax.set_xticks(date_specific_resample.index)
	 - ax.set_xticklabels(["Jan", "","","","Feb", "","","","March","","","","","April","","",""],fontsize="40")
	 - lgnd = plt.legend(loc="center",
	 - title="Types",fontsize="40")
	 - lgnd.get_title().set_fontsize(50)
	 - plt.yticks(fontsize="40" )
	 - plt.savefig("analysis/PyBer_fare_summary.png")


 


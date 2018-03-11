

```python
#Dependencies
import pandas as pd
import matplotlib.pyplot as plt
#import seaborn as sns
```


```python
#Save path to data set in a variable
data_file = "city_data.csv"
data_file2 = "ride_data.csv"
```


```python
#Use pandas to read the data
#print(data_file)
#data_file_pd = pd.read_json(data_file)
# pd_file = pd.read_csv(data_file)
# pd_file.head()

pd_file = pd.read_csv(data_file)
pd_file.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd_file2 = pd.read_csv(data_file2)
pd_file2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge the files together on city, which is the common field between the two.
# Merge our two data frames together
combined_pyber_data = pd.merge(pd_file, pd_file2 , how="left", on=["city","city"])
combined_pyber_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
#pwd
```


```python
#Create a dataframe that groups by city.
citygroup = pd.DataFrame(combined_pyber_data.groupby(["city"]).count())
citygroup.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
avgfare = round(combined_pyber_data.groupby(["city"]).mean()["fare"],2)
avgfare.head()
```




    city
    Alvarezhaven    23.93
    Alyssaberg      20.61
    Anitamouth      37.32
    Antoniomouth    23.62
    Aprilchester    21.98
    Name: fare, dtype: float64




```python
totalrides = combined_pyber_data.groupby(["city"]).count()["ride_id"]
totalrides.head()
```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Name: ride_id, dtype: int64




```python
# totaldrivers = combined_pyber_data.groupby("city").mean()["driver_count"]
# totalrides.head()

bycity = combined_pyber_data.groupby('city')
driver_count = bycity.mean()['driver_count']
driver_count.head()
```




    city
    Alvarezhaven    21.0
    Alyssaberg      67.0
    Anitamouth      16.0
    Antoniomouth    21.0
    Aprilchester    49.0
    Name: driver_count, dtype: float64




```python
cityanalysis = pd.DataFrame({"Average Fare":avgfare,
                        "Rides Per City":totalrides,
                         "Drivers per City":driver_count})
#"City Type": "type"} )
cityanalysis.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Fare</th>
      <th>Drivers per City</th>
      <th>Rides Per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.93</td>
      <td>21.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.61</td>
      <td>67.0</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.32</td>
      <td>16.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.62</td>
      <td>21.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.98</td>
      <td>49.0</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Create a new dataframe as a copy of pd_file (citydata csv) and set the index to city for merging purposes.
pd_file.reset_index()
pd_file.head()
citycsv = pd.DataFrame(pd_file)
citycsv = citycsv.reset_index()
citycsv = citycsv.set_index('city')
citycsv.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kelseyland</th>
      <td>0</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Nguyenbury</th>
      <td>1</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>East Douglas</th>
      <td>2</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>West Dawnfurt</th>
      <td>3</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Rodriguezburgh</th>
      <td>4</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
cityanalysis2 = pd.DataFrame(cityanalysis)
cityanalysis2 = cityanalysis2.reset_index()
cityanalysis2 = cityanalysis2.set_index('city')
cityanalysis2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Fare</th>
      <th>Drivers per City</th>
      <th>Rides Per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.93</td>
      <td>21.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.61</td>
      <td>67.0</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.32</td>
      <td>16.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.62</td>
      <td>21.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.98</td>
      <td>49.0</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge the dataframe above with the citydata csv to get the type.
getcity = pd.merge(citycsv, cityanalysis2, left_index=True,right_index=True) 
#on="city",left_index=True,right_index=True)
#drop driver count and index as they are irrelvant.
del getcity["index"]
del getcity["driver_count"]
getcity.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>Average Fare</th>
      <th>Drivers per City</th>
      <th>Rides Per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>Urban</td>
      <td>23.93</td>
      <td>21.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>Urban</td>
      <td>20.61</td>
      <td>67.0</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>Suburban</td>
      <td>37.32</td>
      <td>16.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>Urban</td>
      <td>23.62</td>
      <td>21.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>Urban</td>
      <td>21.98</td>
      <td>49.0</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
urban_cities = combined_pyber_data[combined_pyber_data["type"] == "Urban"]
rural_cities = combined_pyber_data[combined_pyber_data["type"]=="Rural"]
suburban_cities = combined_pyber_data[combined_pyber_data["type"]=="Suburban"]

urban_ride_count = urban_cities.groupby(["city"]).count()["ride_id"]
urban_avg_fare = urban_cities.groupby(["city"]).mean()["fare"]
urban_driver_count =  urban_cities.groupby(["city"]).mean()["driver_count"] 

rural_ride_count = rural_cities.groupby(["city"]).count()["ride_id"]
rural_avg_fare = rural_cities.groupby(["city"]).mean()["fare"]
rural_driver_count =  rural_cities.groupby(["city"]).mean()["driver_count"] 

suburban_ride_count = suburban_cities.groupby(["city"]).count()["ride_id"]
suburban_avg_fare = suburban_cities.groupby(["city"]).mean()["fare"]
suburban_driver_count =  suburban_cities.groupby(["city"]).mean()["driver_count"] 


#mean driver count                                #c = coral
    #coral, skyblue 
    #counr rideid, meanfare, meandriverfare
```


```python
#urban_cities.head()
#rural_cities.head()

ridesharingdata = pd.DataFrame({"Number of Urban Rides":urban_ride_count,
                         "Number of Urban Rides":rural_ride_count,
                         "Number of Suburban Rides":suburban_ride_count,
                          "Urban Average Fare": urban_avg_fare,
                          "Rural Average Fare":rural_avg_fare,
                           "Suburban Average Fare":suburban_avg_fare,
                            "Number of Urban Drivers": urban_driver_count,
                            "Number of Rural Drivers": urban_driver_count,
                            "Number of Suburban Drivers": suburban_driver_count} )
ridesharingdata.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Rural Drivers</th>
      <th>Number of Suburban Drivers</th>
      <th>Number of Suburban Rides</th>
      <th>Number of Urban Drivers</th>
      <th>Number of Urban Rides</th>
      <th>Rural Average Fare</th>
      <th>Suburban Average Fare</th>
      <th>Urban Average Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>21.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>67.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>67.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>NaN</td>
      <td>16.0</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37.315556</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>21.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>49.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.981579</td>
    </tr>
  </tbody>
</table>
</div>




```python
#This first bubble chart is without the types and it is not the final answer. 

# ridelist = getcity['Rides Per City'].tolist()
# avgfairlist = getcity['Average Fare'].tolist()
# drivercountlist = getcity['Drivers per City']
# typelist = getcity['type'].tolist()
# #s = getcity["type"]


# #plt.scatter(x=ridelist, y=avgfairlist)  #correct to use scatter plot without bubble chart.

# plt.scatter(x = ridelist, 
#             y = avgfairlist,
#            s = drivercountlist,
#            marker="o", facecolors="red",
#            alpha = 0.6)

# plt.title('Pyber Ride Sharing Data(2016)')
# plt.ylabel('Total Number of Rides (Per City)')
# plt.xlabel('Average Fares ($)')
# plt.text(-20,0, " Note: The circle size represents how many drivers are in that city.")
# #\n
# plt.show()
```


![png](output_16_0.png)



```python
#Create bubble chart. Final bubble chart.

plt.scatter(x=urban_ride_count,
            y=urban_avg_fare,
           s = 15 * urban_driver_count,
           marker="o", facecolors="coral",
            #linewidths = 0,
            edgecolor = "black",
           alpha = 0.6)
plt.scatter(x=rural_ride_count,
            y=rural_avg_fare,
           s = 15 * rural_driver_count,
           marker="o", facecolors="gold",
            #linewidths = 0,
            edgecolor = "black",
           alpha = 0.6)
plt.scatter(x=suburban_ride_count,
            y=suburban_avg_fare,
           s = 15 * suburban_driver_count,
           marker="o", facecolors="skyblue",
            #linewidths = 0,
            edgecolor = "black",
           alpha = 0.6)
plt.title('Pyber Ride Sharing Data(2016)')
plt.xlabel('Total Number of Rides (Per City)')
plt.ylabel('Average Fares ($)')
plt.text(-20,0, " Note: The circle size represents how many drivers are in that city.")

# legend = ["Rural", "Suburban", "Urban"]
plt.legend(["Urban","Rural", "Suburban"])
# lgnd = plt.legend(fontsize = "small", 
#             mode = "Expanded", 
#             numpoints = 1, 
#             scatterplots = 1, 
#             loc = "best", 
#             title = "City Type", 
#             labelspacing = 0.5)
# lgnd.legendHandles[0]._sizes = [30]
# lgnd.legendHandles[1]._sizes = [30]
# lgnd.legendHandles[2]._sizes = [30]

plt.grid()
plt.show()
```


![png](output_17_0.png)


#You must include a written description of three observable trends based on the data.
In the bubble chart above, I can see that in urban cities, the average fares are lower despite having the highest number of rides. By contrast, rural has less number of rides but higher average fares. Suburban is in the middle. It may be beneficial for the ride sharing company to target urban and suburban areas since urban areas have the highest number of rides and suburban has higher average fares. 
In the pie charts below, urban dominates the two other city types in the total fares, total rides and total rides. This makes sense because not everyone who lives in urban areas has a car and people who live in urban areas typically depend on public transportation. Suburban is second in all three pie charts. 

# Total Fares by City Type


```python
#% of Total Fares 
# demogroup = combined_pyber_data.groupby(["city","type"])
# demogroup.size()
typegroup = combined_pyber_data.groupby(["type","city"])
#typegroup.head()

```


```python

# perfare= combined_pyber_data.groupby(["city", "type"]).size()
# perfare #ridespertype
# #create into a dataframe
# farespertype = pd.DataFrame(perfare)
# farespertype

# #perfaretype = combined_pyber_data.groupby(["type"]).size()


# perfaretype = perfare.groupby(["type"]).size()
# perfaretype


#typefares = pd.DataFrame(farespertype.groupby(["type"]).count())
#typefares.columns = ["NumberFares"]
#typefares

```


```python
#ridestype = pd.DataFrame(combined_pyber_data.groupby(["city","type"]).sum())

ridestype = pd.DataFrame(combined_pyber_data.groupby(["type"]).sum()["fare"])
ridestype.columns = ["NumberFares"]
ridestype
#ridestype.loc['Port James']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NumberFares</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>4255.09</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>20335.69</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>40078.34</td>
    </tr>
  </tbody>
</table>
</div>




```python
# by_type = combined_pyber_data.groupby('type')['type', 'fare', 'ride_id', 'driver_count']
# by_type.head()
# #total fare by city
# fare_sum = by_type.sum()['fare']
# fare_sum
```


```python
#Total Number of Fares
fares_count = ridestype["NumberFares"].sum()
fares_count
```




    64669.119999999966




```python
ruralfares = round(ridestype["NumberFares"].loc["Rural"],2)
#ruralfares = typefares["NumberFares"].loc["Rural"]
print(ruralfares)
#print(ruralrides)
```

    4255.09
    


```python
subfares = round(ridestype["NumberFares"].loc["Suburban"],2)
#subfares = typefares["NumberFares"].loc["Suburban"]
print(subfares)
#print(subrides)
```

    20335.69
    


```python
urbanfares = round(ridestype["NumberFares"].loc["Urban"],2)
#urbanfares = typefares["NumberFares"].loc["Urban"]
print(urbanfares)
#print(urbanrides)
```

    40078.34
    


```python
ruralpercent = round(ruralfares / fares_count, 2) * 100
ruralpercent
```




    7.000000000000001




```python
# Labels for the sections of our pie chart
labels = ["Rural", "Suburban", "Urban"]

# The values of each section of the pie chart
sizes = [ruralfares, subfares, urbanfares]

# The colors of each section of the pie chart
colors = ["yellowgreen", "red", "lightcoral"]
#, "lightskyblue"]

# Tells matplotlib to seperate the "Python" section from the others
explode = (0, 0, 0.2)

#Define colors for each type to be used in pie plots. Use the hex code. 
color_scheme = {'Gold':'#FFD700', 'Light Sky Blue':'#87CEFA', 'Light Coral':'#F08080'}
city_color = {'Rural': color_scheme['Gold'], 'Suburban': color_scheme['Light Sky Blue'], 'Urban': color_scheme['Light Coral']}

```


```python
# Creates the pie chart based upon the values above
# Automatically finds the percentages of each part of the pie chart

#colors and exploe the same for all pie charts, reference here
colors = [city_color[n] for n in labels]
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.title('% of Total Fares by City Type')
```




    Text(0.5,1,'% of Total Fares by City Type')




![png](output_30_1.png)



```python
# Tells matplotlib that we want a pie chart with equal axes
#plt.axis("equal")
```


```python
# Prints our pie chart to the screen
plt.show()
```

# Total Rides by City Type


```python
#Total Rides by City Type
ridestype = pd.DataFrame(combined_pyber_data.groupby(["city","type"]).sum())

ridestype = pd.DataFrame(combined_pyber_data.groupby(["type"]).count()["ride_id"])
ridestype.columns = ["NumberRides"]
ridestype
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NumberRides</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>125</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>657</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python
riders_count = ridestype["NumberRides"].sum()
riders_count
```




    2407




```python
ruralrides = ridestype["NumberRides"].loc["Rural"]
print(ruralrides)
subrides = ridestype["NumberRides"].loc["Suburban"]
print(subrides)
urbanrides = ridestype["NumberRides"].loc["Urban"]
print(urbanrides)
```

    125
    657
    1625
    


```python
# Labels for the sections of our pie chart
labels = ["Rural", "Suburban", "Urban"]

# The values of each section of the pie chart
sizes = [ruralrides, subrides, urbanrides]

# The colors of each section of the pie chart
#colors = ["yellowgreen", "red", "lightcoral"]
#, "lightskyblue"]

colors = [city_color[n] for n in labels]

# Tells matplotlib to seperate the "Python" section from the others
explode = (0, 0, 0.2)
```


```python
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.title('% of Total Rides by City Type')
```




    Text(0.5,1,'% of Total Rides by City Type')




![png](output_38_1.png)


# Total Drivers by City Type


```python
#drivers = combined_pyber_data.groupby(["city","type"]).sum()["driver_count"] / combined_pyber_data.sum["driver_count"]
driversorig = pd.DataFrame(combined_pyber_data.groupby(["city","type", "driver_count"]).sum())

driversorig.reset_index(inplace=True)
driversorig
driversorig = pd.DataFrame(drivers.groupby("type").sum())
drivers = pd.DataFrame(driversorig)
# drivers = combined_pyber_data.groupby(["city","type"]).sum()
# drivers.reset_index(inplace = True)
# drivers.groupby("type").sum()
#drivers
#del drivers["fare"]
#del drivers["ride_id"]
drivers

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>104</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>638</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>2607</td>
    </tr>
  </tbody>
</table>
</div>




```python
urbandrivers = drivers.loc['Urban']
urbandrivers 
```




    driver_count    2607
    Name: Urban, dtype: int64




```python
subdrivers = drivers.loc['Suburban']
subdrivers
```




    driver_count    638
    Name: Suburban, dtype: int64




```python
ruraldrivers = drivers.loc['Rural']
ruraldrivers
```




    driver_count    104
    Name: Rural, dtype: int64




```python
# Labels for the sections of our pie chart
labels = ["Rural", "Suburban", "Urban"]

# The values of each section of the pie chart
sizes = [ruraldrivers, subdrivers, urbandrivers]

# The colors of each section of the pie chart
colors = ["yellowgreen", "red", "lightcoral"]
#, "lightskyblue"]

# Tells matplotlib to seperate the "Python" section from the others
explode = (0.1, 0, 0)

colors = [city_color[n] for n in labels]

# Tells matplotlib to seperate the "Python" section from the others
explode = (0, 0, 0.2)
```


```python
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

plt.title('% of Total Drivers by City Type')
```




    Text(0.5,1,'% of Total Drivers by City Type')




![png](output_45_1.png)



```python
# countfare = demogroup.count()["fare"]
# countfare
```


```python
#type(pd_file.groupby(["city","type"]))
```


```python
#list(pd_file.groupby(["type"]))
```


```python
# for group_key, group_value in pd_file.groupby('type'):
#     print(group_key)
#     print(group_value)
```


```python
# for group_key, group_value in typegroup:
#     print(group_key)
#     print(group_value)
```

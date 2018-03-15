

```python
#dependencies

import pandas as pd
import numpy
import matplotlib.pyplot as plt
import csv
import seaborn as sns

city_data_path = "Raw Data/city_data.csv"
ride_data_path = "Raw Data/ride_data.csv"

city_data = pd.read_csv(city_data_path)
ride_data = pd.read_csv(ride_data_path)
city_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Brianborough</td>
      <td>62</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>New Katherine</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lake Charlesside</td>
      <td>65</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merge data sets
city_ride_merge =  pd.merge(city_data, ride_data, on ="city", how ="outer")
city_ride_merge.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 10:56:28</td>
      <td>12.40</td>
      <td>7963408790849</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 04:28:03</td>
      <td>18.78</td>
      <td>2315208159060</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-03 03:00:08</td>
      <td>30.10</td>
      <td>558639764959</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-01 00:10:21</td>
      <td>7.76</td>
      <td>9113511454178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 05:22:44</td>
      <td>22.00</td>
      <td>4171010688543</td>
    </tr>
  </tbody>
</table>
</div>




```python
#variables for bubble chart

urban_cities=city_ride_merge[city_ride_merge["type"]=="Urban"]
suburban_cities=city_ride_merge[city_ride_merge["type"]=="Suburban"]
rural_cities=city_ride_merge[city_ride_merge["type"]=="Rural"]

urban_ride_count=urban_cities.groupby(["city"]).count()["ride_id"]
urban_fare_avg=urban_cities.groupby(["city"]).mean()["fare"]
urban_driver_count=urban_cities.groupby(["city"]).mean()["driver_count"]

suburban_ride_count=suburban_cities.groupby(["city"]).count()["ride_id"]
suburban_fare_avg=suburban_cities.groupby(["city"]).mean()["fare"]
suburban_driver_count=suburban_cities.groupby(["city"]).mean()["driver_count"]

rural_ride_count=rural_cities.groupby(["city"]).count()["ride_id"]
rural_fare_avg=rural_cities.groupby(["city"]).mean()["fare"]
rural_driver_count=rural_cities.groupby(["city"]).mean()["driver_count"]
```


```python
plt.scatter(urban_ride_count, 
            urban_fare_avg, 
            s=10*urban_driver_count,c="gold",
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Urban")

plt.scatter(suburban_ride_count, 
            suburban_fare_avg, 
            s=10*urban_driver_count,c="blue",
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Suburban")

plt.scatter(rural_ride_count, 
            rural_fare_avg, 
            s=10*urban_driver_count,c="coral",
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Rural")

plt.title("Pyber Ride Sharing Data")
plt.ylabel("Average Fare")
plt.xlabel("Total Number of Rides")
plt.xlim((0,40))
plt.grid(True)


lgnd = plt.legend(fontsize="small", mode="Expanded", 
                  numpoints=1, scatterpoints=1, 
                  loc="best", title="City Types", 
                  labelspacing=0.5)
lgnd.legendHandles[0]._sizes = [30]
lgnd.legendHandles[1]._sizes = [30]
lgnd.legendHandles[2]._sizes = [30]

plt.show()
```


![png](output_3_0.png)



```python
#group by fare by city type
fare_city = city_ride_merge.groupby("type")["fare"].sum().reset_index()
fare_city
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>4271.69</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>18779.26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>40093.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#pie chart
fig1, ax1 = plt.subplots()
ax1.pie(fare_city["fare"], labels = fare_city["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%",)
ax1.axis('equal')
plt.title('Fares by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()
```


![png](output_5_0.png)



```python
#group rides by city type
ride_city = city_ride_merge.groupby("type")["date"].count().reset_index()
ride_city
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>625</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python
#pie chart ride by city type
fig1, ax1 = plt.subplots()
ax1.pie(ride_city["date"], labels = ride_city["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%")
ax1.axis('equal')
plt.title('Ride by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()
```


![png](output_7_0.png)



```python
#group drivers by city
driver_city = city_ride_merge.groupby("type")["driver_count"].sum().reset_index()
driver_city
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>driver_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>662</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Suburban</td>
      <td>8774</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Urban</td>
      <td>60935</td>
    </tr>
  </tbody>
</table>
</div>




```python
#pie chart drivers by city
fig1, ax1 = plt.subplots()
ax1.pie(driver_city["driver_count"], labels = driver_city["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%")
ax1.axis('equal')
plt.title('Drivers by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()
```


![png](output_9_0.png)



```python
# 1 - Fares are the highest in urban areas
# 2 - There are the most rides in urban areas
# 3 - There are the most drivers in urban areas
```

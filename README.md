# Cyclistic Bike-Share

## Google Data Analytics: Capstone Project #1

### INTRODUCTION 

The director of marketing at Cyclistic, a bike-share company in Chicago, believes maximizing the number of its annual members will aid in the company’s future success. To explore this hypothesis and possibly design a new marketing strategy, the analyst team wants me to find out:

- How do annual members and casual riders use Cyclistic bikes differently?

### ASK

Understand how annual members and casual riders use Cyclistic bikes differently to maximize the number of annual members by converting casual riders to memberships. This will provide insight to marketing and the executive team on how to strategically build a new marketing campaign to achieve company growth.

These insights will drive business decisions by informing us:

1. The differences between annual members vs. causal riders
2. How bikes are used at Cyclistic
3. Why causal riders would buy a membership
4. How digital media can effect Cyclistic’s marketing tactics


### PREPARE

Data provided came from an Amazon Web Services database that was managed by Cyclistic. I’ve pulled 12 months’ worth of data from 2021/12 - 2022/11. The data collected does not contain personally identifiable information (due to data-privacy concerns). We have access to ride id, type of bike, start and end times, station names, station ids, and user type.


### PROCESS 

The data needed to be cleaned so I used MySQL. 

My data cleaning process consisted of:
-	Checking for misspelled words and duplicate rows
-	Removing null data cells
-	Assigning column datatypes
-	Applying correct formatting
-	Creating appropriate column names
-	Keeping only data that will identify how annual members and causal riders use Cyclistic bikes differently
-	Creating a duration column
-	Excluding trips less than 1 minute or over 24 hours
-	Creating a day of the week column

```mysql:
CREATE TABLE updated_cyclistic_table
  SELECT
    ride_id,
    rideable_type,
    start_station_name,
    end_station_name,
    started_at,
    ended_at,
    member_casual,
    TIME_TO_SEC((timediff(ended_at,started_at))) as ride_length,
    dayofweek(started_at)
  FROM
    combined_cyclistic_data
  WHERE
    (start_station_name IS NOT NULL 
    AND end_station_name IS NOT NULL)
    AND
    (ended_at - started_at > 0)
    AND
    (TIME_TO_SEC(timediff(ended_at,started_at))) < 86400
    AND 
    (TIME_TO_SEC(timediff(ended_at,started_at))) > 59
```
This resulted in removing 1,399,540 rows (5,733,451 -> 4,333,911). A loss of 32.29% of data

### ANALYZE

The data needed to be visualized so I used Tableau.

To start with the question of how annual riders and casual riders use Cyclistic bike differently I looked at a 12-month period and a weekday usage of membership riders vs. causal riders:

<img width="953" alt="Screenshot 2023-02-07 at 1 17 00 PM" src="https://user-images.githubusercontent.com/121827009/217336415-e10723b5-b712-4beb-921a-20dec49b3e7c.png">

During this 12-month period, casual riders peaked in July with 306,594 rides and membership riders peaked in August with 328,576. Following causal riders’ peak there was a 13% drop in riders. Following membership riders peak there was only a 6% drop in number of rides.


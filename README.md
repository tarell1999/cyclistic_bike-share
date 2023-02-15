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

During this 12-month period, casual riders peaked in July with 306,594 rides and membership riders peaked in August with 328,576. Following causal riders’ peak there was a 13% drop in riders. Following membership riders peak there was only a 6% drop in number of rides. The greater drop off in causal riders shows what’s expected, membership riders tend to be more consistent.

During the days of the week, member riders and causal riders peaked at different times. Member riders bike usage tend to peak on Wednesdays while causal riders peaked on Saturdays. This difference represents a behavior of member riders preferring to ride bikes toward the middle of the week and casual riders preferring to ride bikes towards the weekend. This difference in behavior is so significant that causal riders actually outnumbered member riders on Saturdays and Sundays.

<img width="567" alt="Screenshot 2023-02-09 at 4 11 17 PM" src="https://user-images.githubusercontent.com/121827009/218826883-d9e434be-6f22-4f65-8b0e-ac58fde94f76.png">

Focusing on the change from previous month’s bike usage there’s a pattern. Starting in February, bike usage consistently trends upward towards the warmer months then it starts to drop in September for member riders. For causal riders the trend stops in August. This could be an opportunity to target marking towards causal riders. The largest increase in casual riders happens in March. March can also be an opportunity to target causal riders. 

<img width="725" alt="Screenshot 2023-02-14 at 1 26 19 PM" src="https://user-images.githubusercontent.com/121827009/218827597-eff99cd9-533c-4d22-ab17-de748efe928c.png">

Looking at bike type usage members used electric bikes 34% of the time while casual riders use electric bikes 39% of the time. This is not a substantial difference, but it shows that causal rides tend to use eclectic bikes more than membership riders. This is likely due to electrics bikes price greater cost that is charged to all users.

<img width="615" alt="Screenshot 2023-02-14 at 6 03 27 PM" src="https://user-images.githubusercontent.com/121827009/218882971-0bc7d52f-709d-42f5-b678-236efdeabbbc.png">

Focusing on ride lengths between 1 minute and 24 hours, another difference between membership riders and causal riders is average ride length. Casual riders tend to ride bikes for a longer time. This was consistent for every month. On average causal riders used bikes 11 minutes longer than membership riders. 

This difference is likely due to the 30 minutes causal riders are covered when using a bike. After 30 minutes of using a bike, casual riders are charged for every minute over. Casual riders are encouraged to use bikes for longer due to make there initial fee worth it. Membership riders do not have an initial fee.


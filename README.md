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
-	Excluding tips less than 1 minute or over 24 hours
-	Creating a day of the week column

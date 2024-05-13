# **Google Data Analytics Professional Certificate**

# Introduction
## Scenario
In this case study, I have assumed the role of a junior data analyst working on the marketing analyst team for a fictional company, Cyclistic.

The director of marketing believes the company’s future success depends on maximising the number of annual memberships. Therefore, the team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, our team will design a new marketing strategy to convert casual riders into annual members.

## About Cyclistic
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. 

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno, the director of marketing, believes that maximising the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a solid opportunity to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs. 

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analysing the Cyclistic historical bike trip data to identify trends.

## Project Outline
During this project I will produce a report with the following deliverables:

1. A clear statement of the business task
2. A description of all data sources used
3. Documentation of any cleaning or manipulation of data
4. A summary of my analysis
5. Supporting visualisations and key findings
6. My top three recommendations based on my analysis


# Ask
## Analysis Questions
Three questions have been asked to help guide Cyclistic’s future marketing strategy:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

I have been assigned the first question to answer: **How do annual members and casual riders use Cyclistic bikes differently?**

## Business Task
Identify trends between casual riders and Cyclistic members to determine 3 recommended marketing strategies to help convert more Cyclistic’s casual riders into much more profitable annual members.

# Prepare
## Data Source
I have used Cyclistic’s historical trip data for my analysis. We will be looking at a total 12 months for this analysis, from April 2023 to March 2024.

**Note:** For the purposes of this case study, the datasets are appropriate and have enabled me to answer the business question. The data has been made available by Motivate International Inc. under this [license](https://www.divvybikes.com/data-license-agreement).

Data source: [Index of bucket "divvy-tripdata"](https://divvy-tripdata.s3.amazonaws.com/index.html)

Cyclistic uses the following file naming convention YYYYMM-divvy-tripdata with each file containing one month's worth of data. The range we will be using contains 12 files in the form of Comma Separated Values (CSV).

## Data Structure
Each file consists of historical trip data from one month, which includes the following information:

| Column name  | Description |
| ------------- | ------------- |
| ride_id | ID of the rid |
| rideable_type | Type of bike |
| started_at  | Trip start time |
| ended_at | Trip end time |
| station_start_name | Name of the starting station |
| start_station_id | ID of the starting station |
| end_station_name | Name of the starting station |
| end_station_id | ID of the starting station |
| start_lat | Starting latitude of bike |
| start_lng | Starting longitude of bike |
| end_lat | Ending latitude of bike |
| end_lng | Ending longitude of bike|
| member_casual | Whether the rider is a ‘Member’ or ‘Casual’ |

## Data bias & credibility
This data we are using is appropriate for the fictional company we are doing the analysis for. We will determine the bias and credibility of this data using ROCCC while taking into account the fictional scenario.

* **Reliable** - This data is reliable as it is accurate, complete, and contains a sample size that reflects the population.
* **Original** - This data is not original. The data is third party data and has been made available by Motivate International Inc. under this [license](https://www.divvybikes.com/data-license-agreement).
* **Comprehensive** - The data we are using does provide the information required to answer the question we’re looking to solve. Additionally, Cyclistic’s fleet of 5,824 bicycles are geotracked and locked into a network of 692 stations across Chicago ensuring that the data collected is automated and does not contain human error.
* **Current** - The most recent available dataset available for analysis is from March 2024, as a result this data is considered current given the task we will be conducting. 
* **Cited** - This source has been cited. The data is third party data and has been made available by Motivate International Inc. under this [license](https://www.divvybikes.com/data-license-agreement).

Although the data is not original, the source of the data has been cited and the data it contains has been deemed reliable, comprehensive, and current. Therefore the data is considered good quality and we will be able to produce business recommendations based on it.

## Data Privacy
This is public data that you can use to explore how different customer types are using Cyclistic bikes. Data-privacy prohibits the use of riders’ personally identifiable information. This means that we won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

## Data Integrity
Data-driven decisions are only as strong as the data they’re based on. If the integrity of your data has been compromised it will negatively impact the decisions made.

Data integrity is determined while looking at the bias & credibility of the data, and also during the data cleaning process. Any areas for concern are cleaned during the data cleaning process to ensure the data’s integrity. 


# Process
For the cleaning and analysis of this data I used BigQuery SQL.

Structured Query Language (SQL) was required to perform the cleaning of this data. Spreadsheet software such as Google Sheets or Excel would not have been able to handle such a large amount of data (5,750,177 rows). 

## Joining Tables
Within a new BigQuery project ‘cyclistic-trip-data-2023-24’, all 12 csv files from the selected range were uploaded onto the ‘trip_data_2023_2024’ dataset. Once all 12 files were uploaded they were joined to create a new ‘combined_trips_2023_2024’ table.

``` sql
-- Joining all 12 tables into 1 combined table

CREATE TABLE `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024` AS (
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_04` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_05` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_06` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_07` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_08` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_09` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_10` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_11` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2023_12` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2024_01` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2024_02` 
  UNION ALL
  SELECT *
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.trip_2024_03`
);
```

By creating a new table that joins all 12 individual files means I can manipulate and clean the data without affecting the original files. What’s more, it allows me to perform cleaning and analysis on all the data at once, rather than repeating the process 12 separate times,reducing the likelihood of human error, helping to maintain data integrity.

## Checking the Data
### Formatting
To check the formatting of the data I looked at the scheme and a preview of the data to ensure that the data type matched up correctly with the field.

| Field name  | Data type |
| ------------- | ------------- |
| ride_id | STRING |
| rideable_type | STRING |
| started_at  | TIMESTAMP |
| ended_at | TIMESTAMP |
| station_start_name | STRING |
| start_station_id | STRING |
| end_station_name | STRING |
| end_station_id | STRING |
| start_lat | FLOAT |
| start_lng | FLOAT |
| end_lat | FLOAT |
| end_lng | FLOAT |
| member_casual | STRING |

All of the fields were the correct data type so no action was required.

### Checking Duplicates
To check for duplicates, I specifically looked at the **ride_id** which was the primary key for this data.

I compared the number of rows from the original table with the number of rows that were returned when filtering for distinct **ride_id**’s. Both the original data and the queried data had 5,750,177 rows, meaning the data didn’t contain any duplicates.

``` sql
-- Ensure there are no duplicate ride_id's

SELECT
  COUNT(DISTINCT ride_id) AS ride_id_count,
  COUNT(*) AS original_data_count
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

### Checking Consistency
To check for consistency, I again looked at the primary key **ride_id**, while also looking at **rideable_type** and **member_casual** as they were the only fields with nominal data (e.g. **member_casual** can either be ‘member’ or ‘casual’).

For the **ride_id** column I looked at the maximum and minimum **ride_id** lengths to ensure all values had the same length of. The query returned 16 for both the maximum and minimum meaning the all values were of consistent length.

``` sql
-- Ensure all ride_id values had the same length.

SELECT
  MAX(LENGTH(ride_id)) AS max_ride_id_len,
  MIN(LENGTH(ride_id)) AS min_ride_id_len
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

For the rideable_type column I returned the distinct values to ensure the data contained the 3 expected fields, ‘electric_bike’, ‘classic_bike’ and ‘docked_bike’. The query revealed this was the case, meaning the **rideable_type** column was consistent.

``` sql
-- Ensure the rideable_type column contained the 3 expected fields, ‘electric_bike’, ‘classic_bike’ and ‘docked_bike’.

SELECT
  DISTINCT(rideable_type)
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

The same steps were completed for the **member_casual** column to ensure the data contained the 2 expected fields, ‘member’ and ‘casual’. The query revealed this was the case, meaning the **member_casual** column was consistent.

``` sql
-- Ensure the member_casual column contained the 2 expected fields, ‘member’ and ‘casual.

SELECT
  DISTINCT(member_casual)
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

### Checking Data Range
To check the data range we selected the minimum and maximum **started_at** values from the data. This confirmed that all trip data was from the range we selected.

``` sql
-- Checking Data Range

SELECT 
  MIN(started_at),
  MAX(started_at)
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

### Checking Missing Data
In order to learn more about the NULL values in the data I started by counting all of the NULL values for each column of the data.

``` sql
-- Checking number of NULL values in each column

SELECT
  SUM(CASE WHEN ride_id IS NULL THEN 1 ELSE 0 END) AS ride_id_null,
  SUM(CASE WHEN rideable_type IS NULL THEN 1 ELSE 0 END) AS rideable_type_null,
  SUM(CASE WHEN started_at IS NULL THEN 1 ELSE 0 END) AS started_at_null,
  SUM(CASE WHEN ended_at IS NULL THEN 1 ELSE 0 END) AS ended_at_null,
  SUM(CASE WHEN start_station_name IS NULL THEN 1 ELSE 0 END) AS start_station_name_null,
  SUM(CASE WHEN start_station_id IS NULL THEN 1 ELSE 0 END) AS start_station_id_null,
  SUM(CASE WHEN end_station_name IS NULL THEN 1 ELSE 0 END) AS end_station_name_null,
  SUM(CASE WHEN end_station_id IS NULL THEN 1 ELSE 0 END) AS end_station_id_null,
  SUM(CASE WHEN start_lat IS NULL THEN 1 ELSE 0 END) AS start_lat_null,
  SUM(CASE WHEN start_lng IS NULL THEN 1 ELSE 0 END) AS start_lng_null,
  SUM(CASE WHEN end_lat IS NULL THEN 1 ELSE 0 END) AS end_lat_null,
  SUM(CASE WHEN end_lng IS NULL THEN 1 ELSE 0 END) AS end_lng_null,
  SUM(CASE WHEN member_casual IS NULL THEN 1 ELSE 0 END) AS member_casual_null
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`;
```

The query results were as follows:

| Field name | Number of NULL values |
| ------------- | -------------: |
| ride_id | 0 |
| rideable_type | 0 |
| started_at  | 0 |
| ended_at | 0 |
| station_start_name | 874450 |
| start_station_id | 874450 |
| end_station_name | 929226 |
| end_station_id | 929226 |
| start_lat | 0 |
| start_lng | 0 |
| end_lat | 7566 |
| end_lng | 7566 |
| member_casual | 0 |

From this we can see that these fields contained NULL values: 

* **start_station_name**
* **start_station_id**
* **end_station_name**
* **end_station_id**
* **end_lat**
* **end_lng**

I hypothesised that a number of bikes were not returned to a station when their trip had ended. In turn this means that a number of bikes did not start their trip from a station. One area I needed to explore further are the NULL values in the **end_lat** and **end_lng** columns.

After filtering the results to see only the rows where **end_lat** or **end_lng** columns are NULL I saw a trend that each trip was greater than 24 hours. However, when looking to confirm this by running another query I found that this was the case for 7143 of the NULL values, meaning there were 423 still unaccounted for. 

``` sql
-- Exploring end_lat & end_lng NULL values further

SELECT *
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`
WHERE end_lat IS NULL
  OR end_lng IS NULL
LIMIT 10;


-- Exploring trend that NULL values are due to trip times being greater than 24 hours

SELECT
  *,
  TIMESTAMP_DIFF(ended_at, started_at, HOUR) AS journey_duration_hours
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`
WHERE (end_lat IS NULL OR end_lng IS NULL)
  AND TIMESTAMP_DIFF(ended_at, started_at, HOUR) > 24
LIMIT 10;


-- Exploring why some NULL values are not due to trip times being greater than 24 hours

SELECT
  *,
  TIMESTAMP_DIFF(ended_at, started_at, HOUR) AS journey_duration_hours
FROM
  `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`
WHERE (end_lat IS NULL OR end_lng IS NULL)
  AND TIMESTAMP_DIFF(ended_at, started_at, HOUR) < 24
LIMIT 10;
```

After exploring the data more I could not see a trend to explain the other 423 null values. One hypothesis is that the geo tracking system malfunctioned or was damaged during the journey.

## Data Cleaning
### Removing NULL Values
As mentioned earlier, there were 6 columns that showed NULL values. Of these I removed all the rows that showed NULL values for their **end_lat** or **end_lng** columns only.

I didn’t remove rows that show NULL values in the remaining 4 columns as I hypothesised that some bikes were not returned to a station when their trip had ended. In turn this means that a number of bikes did not start their trip from a station. This is the case as they still have values in their end_lat or end_lng columns.

### Adding New Columns
For the next ‘Analyse’ stage the following columns were added to enable my analysis:

* **ride_length**
* **hour**
* **day_of_week**
* **month**

After checking the results in the 4 new columns it revealed that some rows were showing a negative **ride_length**. To remove these errors I filtered the results to only show trips where the **ride_length** was greater than 60 seconds.

``` sql
-- Creating a new table with clean data and new columns

CREATE TABLE `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024` AS (
  SELECT *,
    TIMESTAMP_DIFF(ended_at, started_at, SECOND) AS ride_length,
    CASE EXTRACT(DAYOFWEEK FROM started_at)
      WHEN 1 THEN 'Sun'
      WHEN 2 THEN 'Mon'
      WHEN 3 THEN 'Tue'
      WHEN 4 THEN 'Wed'
      WHEN 5 THEN 'Thur'
      WHEN 6 THEN 'Fri'
      WHEN 7 THEN 'Sat'
      END AS day_of_week,
    CASE EXTRACT(MONTH FROM started_at)
      WHEN 1 THEN 'Jan'
      WHEN 2 THEN 'Feb'
      WHEN 3 THEN 'Mar'
      WHEN 4 THEN 'Apr'
      WHEN 5 THEN 'May'
      WHEN 6 THEN 'Jun'
      WHEN 7 THEN 'Jul'
      WHEN 8 THEN 'Aug'
      WHEN 9 THEN 'Sep'
      WHEN 10 THEN 'Oct'
      WHEN 11 THEN 'Nov'
      WHEN 12 THEN 'Dec'
      END AS month,
    EXTRACT(HOUR FROM started_at) AS hour
  FROM
    `cyclistic-trip-data-2023-24.trip_data_2023_2024.combined_trips_2023_2024`
  WHERE (end_lat IS NOT NULL AND end_lng IS NOT NULL)
    AND TIMESTAMP_DIFF(ended_at, started_at, SECOND) > 60);
```

After completing the cleaning phase 152,235 rows were removed from the data and 4 new columns added.

# Analyse
Now that the data we’ll be using is stored appropriately and has been prepared for analysis, it’s time to start putting it to work.

Looking back to the question we’re trying to answer - **How do annual members and casual riders use Cyclistic bikes differently?** - the following queries were required to help formulate my answer:

## User split

``` sql
WITH temp AS (
  SELECT 
    member_casual,
    COUNT(*) AS quantity
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
  GROUP BY member_casual
  ORDER BY COUNT(*) DESC
)
SELECT
  member_casual,
  quantity,
  ROUND((quantity / SUM(quantity) OVER () * 100), 2) AS percentage_of_member_casual
FROM temp;
```

## User split by bike type

``` sql
WITH trip_totals AS (
  SELECT 
    member_casual,
    rideable_type,
    COUNT(*) AS total_trips
  FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
  GROUP BY 
    member_casual, 
    rideable_type
  ORDER BY 
    rideable_type, 
    member_casual
)
SELECT 
  member_casual,
  rideable_type,
  total_trips,
  ROUND((total_trips / SUM(total_trips) OVER (PARTITION BY rideable_type) * 100), 2) AS percentage_of_rideable_type
FROM trip_totals
ORDER BY 
  rideable_type, 
  member_casual;
```

## Popular start location: Member Vs Casual

``` sql
SELECT
  member_casual,
  start_station_name,
  AVG(start_lat) AS start_lat, 
  AVG(start_lng) AS start_lng,
  COUNT(*) AS total_trips
FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
WHERE 
  start_station_name IS NOT NULL 
  AND end_station_name IS NOT NULL
GROUP BY 
  member_casual,
  start_station_name;
```

## Total trips: Member Vs Casual
### Hour

``` sql
SELECT
  member_casual,
  COUNT(ride_id) as total_trips,
  hour
FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
GROUP BY 
  hour,
  member_casual
ORDER BY
  hour;
```

### Day

``` sql
SELECT
  member_casual,
  COUNT(ride_id) as total_trips,
  day_of_week
FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
GROUP BY 
  day_of_week,
  member_casual;
```

### Month

``` sql
SELECT
  member_casual,
  COUNT(ride_id) as total_trips,
  month
FROM `cyclistic-trip-data-2023-24.trip_data_2023_2024.cleaned_trips_2023_2024`
GROUP BY 
  month,
  member_casual;
```

Similar to before, Structured Query Language (SQL) was required to perform the analysis of this data due to the amount of data being processed (5,597,942 rows). 

# Share
Tableau: [Cyclistic | April 2023 - March 2024](https://public.tableau.com/views/RMProject1/Dashboard1?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link)

With the data analysed and prepared, Tableau was used to visualise the data and formulate a story to help answer the question - How do annual members and casual riders use Cyclistic bikes differently?

Here is an overview of the dashboard created in Tableau:

![Cyclistic | Dashboard](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/1dbd8786-0318-4687-8d50-5b9002c53113)

## Diving into the Analysis
### User Split
I began by looking at the split of user type (Member Vs Casual). In order to achieve this it was important to show both the total trips and percentage share of the entire user base.

From Visual 1.1 below you can see that the User Split is 64.1% member and 35.9% casual.

![Cyclistic | trips by bike type](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/425b458e-a3ef-4848-af73-b9b8d858841f)
Visual 1.1: User Split & User Split | By Bike Type

The next step was to see if different user types preferred different bike types. From Visual 1.1 above, User Split | By Bike Type, the ‘Docked’ bike type seems to be exclusive to casual users. In terms of ‘Classic’ and ‘Electric’ bikes, there doesn’t seem to be a stand out preference with the percentage share of both bike types being ±3% compared to the overall User Split.

### Trips by Date & Time
The next stage of analysis was to determine if there was a difference time of trip by user type (Member Vs Casual). The data was separated into three tables, Trips By Hour, Trips By Day and Trips By Month with each providing total trips grouped by user type, and by their respective datetime value.

When visualising the data I removed the total trips from the Y axis for all 3 visuals. This was done because I wanted to focus on the trends rather than the quantity of trips. As seen from our previous analysis of Visual 1.1 the split of users favours ‘member’ user type so the quantity will likely be skewed towards them regardless of other factors.

#### Trips by Hour
From Visual 2.1 below you can see that member usage peaked at 8am and 5pm, which is likely to be associated with working hours (9am - 5pm) where users will be commuting to and from work.

![Cyclistic | trips by hour 1348 x 317](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/79c81f62-8e98-4621-a73a-00d979aa8a63)
Visual 2.1: Trips By Hour

In comparison, casual usage slowly increases from 5am before peaking at 5pm. It is harder to determine why this is the case, however a case could be made that some casual users also use Cyclistic to commute from work. 

#### Trips by Day
From Visual 2.2 below you can see that member usage is most common on weekdays before reducing just prior, and then during the weekend. Again this is likely to be associated with a regular work week (Mon-Fri) where users will use Cyclistic to commute to and from work.

![Cyclistic | trips by day 1348 x 317](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/350a6e8f-1b4f-42c9-89b6-6e1b574efa9e)
Visual 2.2: Trips By Day

In comparison, casual usage peaks on the weekend with Saturday being the most popular day, and Sunday being the second most popular day. This tells us that casual users are more likely to use Cyclistic on the weekend rather than the weekday. This could also indicate that they use Cyclistic for leisure rather than for commuting.

#### Trips by Month
From Visual 2.3 below you can see that both member and casual users are more likely to use Cyclistic in the more traditionally warmer months. This is indicated by the steady increase in usage from the winter months to the summer months, where it peaks in August before usage decreases as you get closer to winter again.

![Cyclistic | trips by month 1348 x 317](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/1be89071-211d-49b7-a4b3-a58ed03d3b7b)
Visual 2.3: Trips By Month

### Trips by Location
The final analysis was to determine if there was a difference of location by user type (Member Vs Casual). This data was separated into two maps.

![Cyclistic | pop  start location](https://github.com/ronanmcgann/Data_Analysis_Project/assets/168845115/a00cfc78-9e54-4d9a-b67d-38e2de03f8b6)
Visual 3.1: Popular Start Locations

As you can see from Visual 3.1, casual users seem to favour the city's shoreline and beaches, whereas members are less predictable with their start locations.

This backs up our previous theory that casual users use Cyclistic for leisure, whereas members use Cyclistic more for commuting.

## Key Findings
Here are the following key findings that will answer the question we were posed - How do annual members and casual riders use Cyclistic bikes differently?

| Member | Casual |
| ------------- | ------------- |
| Trips are during commuting hours (8am & 5pm). | Trips are throughout the day, favouring the afternoons. |
| Trips are more common on weekdays. | Trips are more common on weekends. |
| Start location is spread around the city with no clear favourable start location. | Start location is concentrated on the city's shoreline and beaches. |

# Act
With the three main differences highlighted in the Key Findings, the following three recommendations for a new marketing strategy to convert casual riders into annual
Members were made.

1. Introduce a new half-day membership option to target casual users who favour afternoon trips.

2. Introduce a weekend membership option to target casual members who favour weekend trips.

3. Focus membership marketing campaigns on the city's shoreline and beaches to target the majority of casual users.

Additional data I would look for to expand on these findings would be in relation to popular tourist locations. I would use this to see if there was a correlation between tourist hotspots and the popular locations we saw casual users start their trips from.

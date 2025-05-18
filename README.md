# Revenue analysis-Dashboard

### Dashboard Link : https:https://app.powerbi.com/groups/me/reports/f66f3705-20a0-4a89-9e7e-304ac219cd28/dea736ffbb5c7312b010?experience=power-bi

## Problem Statement

This project analyses hotel revenue data to uncover insights and trends that can inform business decisions .The dashboard provides visualizations and metrics to help hotel management understand revenue patterns,parking space utilization, and other key trends.


### Steps followed 

- Step 1 : Create Database in MS SQL.

for creating Database below SQL script was written;
CREATE DATABASE Hotel_Revenue

- Step 2 : Loaded hotel revenue dataset in the Database  by using Bulk insert code.

to load data into SQL Database below SQL script was written;

  BULK INSERT [dbo].[Sales]
  FROM "C:\Users\fsumbulero\OneDrive - Deloitte (O365D)\Hotel_Projects\2018.txt"
  WITH(
      DATAFILETYPE = 'char',
      FIRSTROW = 1,
      FIELDTERMINATOR = '\t',
      ROWTERMINATOR = '\n'
  )
- Step 3 : Cleaned the data,casted all the relevant columns into its respective data type,performed left join  
to merged Sales table(Primary) with Discount and meal tables(Secondary)

for left join below SQL script was written;

USE [Hotel_Revenue]

SET STATISTICS IO ON

SELECT [hotel]
      ,[is_canceled]
      ,[lead_time]
      ,[arrival_date_year]
      ,[arrival_date_month]
      ,[arrival_date_week_number]
      ,[arrival_date_day_of_month]
      ,[stays_in_weekend_nights]
      ,[stays_in_week_nights]
      ,[adults]
      ,[children]
      ,[babies]
      ,a.[meal]
      ,[country]
      ,a.[market_segment]
	  ,b.[Discount]
      ,c.[Cost]
	  ,ISNULL((CAST([stays_in_weekend_nights]AS FLOAT)+CAST([stays_in_week_nights] AS FLOAT))*CAST(b.[Discount] AS FLOAT)*CAST([adr] AS FLOAT),0) AS [Revenue]
      ,[distribution_channel]
      ,[is_repeated_guest]
      ,[previous_cancellations]
      ,[previous_bookings_not_canceled]
      ,[reserved_room_type]
      ,[assigned_room_type]
      ,[booking_changes]
      ,[deposit_type]
      ,[agent]
      ,[company]
      ,[days_in_waiting_list]
      ,[customer_type]
      ,[adr]
      ,[required_car_parking_spaces]
      ,[total_of_special_requests]
      ,[reservation_status]
      ,[reservation_status_date]
  FROM [Hotel_Revenue].[dbo].[Sales]a
  LEFT JOIN [dbo].[Markert_Segment]b ON a.[market_segment]  =b.[market_segment]
  LEFT JOIN [dbo].[Meal_Cost]c ON a.[meal]  =c.[meal]

# Snapshot of Imported table in SQL databasen

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

- Step 4 :loaded sales table into MS Power BI desktop by using SQL statement

# Snapshot of power BI Get Data from SQL server function

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

- Step 5 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 6 : It was observed that in none of the columns errors & empty values were present.
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Visual filters (Slicers) were added for four fields named "Hotel", "Country",& "reservation_status_date".
- Step 8 : Four card visuals were added to the canvas, one representing Total revenue,average discount,Average daily rate and total nights.

Total revenue = 
                sum(Hotel_Project[Revenue])
Snap Total revenue measure ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)


average discount=
                 AVERAGE(Hotel_Project[Discount])           
Snap average discount measure ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

Average daily rate=
                 AVERAGE(Hotel_Project[adr])           
Snap Average daily rate measure ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)


total nights=
             SUM(Hotel_Project[stays_in_week_nights]) + SUM(Hotel_Project[stays_in_weekend_nights])          
Snap of total nights measure ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

- Step 10 : A line chart was also added to the report design area representing the trend of of revenue from 2018 through to 2020.On filter pane the visual is restricted to show revenue trend from January 01,2018 and onwards. While creating this visual, field named "Hotelr" was also added to the Legends bucket, thus revenue is  seggregated according the hotel type.
  
Snap of Line visual ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)


  
- Step 11 : A donut chart was also added with Field "Hotels" on the legends and "Revenue" measure on the Values.This was done to depict percentage of revevune by hotel type

Snap of donut visual ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

  
- Step 12 : A Matrix chart was also added with fields "reservation_status_date" and "Hotel" were on rows where as fields "required_car_park_spaces","Revenue" measure were added to values.On the same we added a measure that calculates percentage of parking lot to total vistors per night.

for creating % measure following DAX expression was written;

%_of_car_park_space = 
                     SUM(Hotel_Project[required_car_parking_spaces])/[Total_Nights],

Snap of Matrix visual ,
![Snap_1](https://user-images.githubusercontent.com/102996550/174089602-ab834a6b-62ce-4b62-8922-a1d241ec240e.jpg)

- Step 13 : In the report view, under the insert tab, using image company's logo "Sunbird Hotels logo" was inserted & similarly using image option "revenue trend analysis" image o was added to the report design area.
  
- Step 18 : The report was then published to Power BI Service. 
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Revenue = 12330277.32

   Resort Hotel revenue by year
                             2018=852982.04
                             2019=2604962.03
                             2020=1702949.42

   City Hotel revenue by year
                             2018=705055.08
                             2019=3837424.03
                             2020=2626904.72         
### [2] Percentage of revenue by hotel

     Resort Hotel revenue by year=41.86
     City Hotel revenue by year= 58.14  

### [3] Average daily rate = 99.42

### [4] Average discount rate=23.96%

### [5] Total nights=485.89

### [6] Other insights
   Percentage ofcar park space over the years

   Resort Hotel revenue by year
                             2018=3%
                             2019=3%
                             2020=3% 

   City Hotel revenue by year
                             2018=1%
                             2019=1%
                             2020=1%
### [7] Conclusion
     (a)	Revenue is increasing by year
     (b)	There is no sufficient evidence that parking space should be increased
     (c)	City hotels generates substantial revenue as compared to Resort hotels

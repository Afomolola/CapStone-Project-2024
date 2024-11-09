# CapStone-Project-2024
This project helps show the analysis of a company's Sales performance and trends.

## Project Overview
This shows how 3 tools were used to prepare data for a company as regards their performance in regions and through returns gotten in the year and monthly.
The excel was used in preparing the data by eliminating duplicates then using Pivot table to summarize the thousand of data in a way that it is easy to understand by the people who needs to access it, it also helps show insights into trends that will help a company make decisions as to what to do and do best in the coming year, what and what not to offer also shows how this 3 tools used are intertwined and if accurately utilized can help get the same result but with difference in presentation.. 

## Data Source
The primary source of data we used majorly is Sales.csv gotten from Capstone LITA Project

## Data Tool
- Microsoft Excel [Download here](https://www.microsoft.com/en-us/microsoft-365/excel?ocid=ORSEARCH_Bing&msockid=04bff806b0a966640250ed20b10567a6)
- SQL[Download here](https://www.bing.com/search?q=microsoft+sql+server+download&filters=dtbk:%22MCFjZ192NV9kb3dubG9hZCFjZ192NV9kb3dubG9hZCFkODhhZWI3ZC00ZTViLTNjOWItMTkwMC0zOTNlNmQ1ZmNmNGU%3d%22+sid:%22d88aeb7d-4e5b-3c9b-1900-393e6d5fcf4e%22&FORM=DEPNAV)
- Power BI [Download here](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads?msockid=04bff806b0a966640250ed20b10567a6)

## Data Cleaning & Preparation
In the initial phase of the Data cleaning and preparation we performed the following actions;
- Data Loading from the sources and inspection into Server studio management after converting into CSV so it is workable also to work on Power BI after loading,the data was imported into the mechanics workshop which is *TransformData*
- Handling missing variables;
  1. This is done in Power BI by first transforming Data where the work is done checking for your Column quality,Distribution under View
  2. For Excel this is done by thorough checckings from source, data filling, Pivoting to summarize large data sets
- Data cleaning and formatting;
  1. Deleting duplicates and validating errors

## Exploratory Data Analysis
This is also knowna as a prescriptive analysis which involves the utilization of Data we worked on, to answer some questions about the Data such as;
- Average of data
- Total Revenue
- Maximum Subscriptions
- Top performing region
- % of total sale
- How many customer

## Data Analysis
This is used to include some basic lines of code or queries or even some of the DAX expression used during our analysis;
```SQL
Select * from [dbo].[Sales Performance Data]

Select Product, SUM(Total_revenuE) as Total_Sales FROM [dbo].[Sales Performance Data] GROUP BY Product


Select Region, COUNT(Total_revenuE) as Number_Sales FROM [dbo].[Sales Performance Data] GROUP BY Region

Select MAX(Product), Count(*) as Highest_Selling_Product FROM [dbo].[Sales Performance Data]

Select Datename(Month, OrderDate) AS Month,
Sum (Total_revenuE) AS MonthlySalesTotal
From [dbo].[Sales Performance Data]
GROUP BY datename (Month, OrderDate)


Select TOP 5 Customer_id, sum(Total_revenuE) as Total_Purchase from [dbo].[Sales Performance Data]
Group by Customer_id Order by Total_Purchase Desc

WITH Total_revenue AS (
    SELECT SUM(Total_revenuE) AS TotalSalesAmount
    FROM [dbo].[Sales Performance Data]
)
SELECT
    Region,
    SUM(Total_revenuE) AS RegionSales,
    (SUM(Total_revenuE) * 100.0 / (SELECT TotalSalesAmount FROM Total_revenuE)) AS PercentageContribution
FROM [dbo].[Sales Performance Data]
GROUP BY Region;

Select Product From [dbo].[Sales Performance Data]
GROUP BY Product
Having Max(OrderDate) < DATEADD(Quarter, -1, GetDate())



Subscription Table

Select * from [dbo].[Subscription Data]

Select Region, Count(CustomerName) as Total_Customer FROM [dbo].[Subscription Data] GROUP BY Region

Select TOP 1 SubscriptionType, Count (CustomerName) As total_Customer From [dbo].[Subscription Data]
Group By SubscriptionType
Order by Total_Customer DESC

----customers who canceled their subscription within 6months--
SELECT CustomerName
FROM [dbo].[CustomerData]
WHERE Canceled = 1
AND DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) <= 6;

----Average subscription duration for all customers----
SELECT AVG(DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd)) AS AverageSubscriptionDuration
FROM [dbo].[CustomerData]

----Customers with subscription longer than 12 months---
SELECT CustomerName
FROM [dbo].[CustomerData]
WHERE DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12;

---Total Revenue by subscription type---
SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
FROM [dbo].[CustomerData]
GROUP BY SubscriptionType;

----Top 3 regions by subscription cancellation---
SELECT TOP 3 Region, COUNT(CustomerID) AS Cancellations
FROM [dbo].[CustomerData]
WHERE Canceled = 1
GROUP BY Region
ORDER BY Cancellations DESC;

---total number of active and cancelled subscription---
SELECT
    SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
    SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CanceledSubscriptions
FROM [dbo].[CustomerData]
```

## Visualization
This deals mainly with the visuals of all that was done from the charts on excel to the charts generated from Power BI.
From the Visuals provided we were able to see how the shoe was the most sold product both in the year 2023 and 2024, also it also helps show the increment in the total customers we added from last year to date.

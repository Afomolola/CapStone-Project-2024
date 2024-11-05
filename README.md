# CapStone-Project-2024
This project helps show the analysis of a company's Sales performance and trends.

## Project Overview
This .

## Data Source
The primary source of data we used majorly is Sales.csv gotten from Capstone LITA Project

## Data Tool
Microsoft Excel Download here
For Data CleaningFor AnalysisFor Data VisualizationSQL - Structured Query Language for Querying of Data, data management and RetrievalGitHub for Portfolio BuildingPower BI for Data visualizationa and reporting

## Data Cleaning & Preparation
In the initial phase of the Data cleaning and preparation we performed the following actions;
- Data Loading from the sources and inspection into Server studio management and Power BI from Excel
- Handling missing variables;
  1. This is done in Power BI by first transforming Data where the work is done checking for your Column quality,Distribution under View
  2. For Excel this is done by filling datas
- Data cleaning and formatting;
  1. Deleting duplicates and validating errors

## Exploratory Data Analysis
This involved the utilization of Data we worked on, to answer some questions about the Data such as;
- 

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
This deals mainly with the visuals of all that was done from the charts on excel to the charts generated from Power BI

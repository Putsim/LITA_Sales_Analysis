# LITA_Sales_Analysis
This project demonstrates my ability to analyze and derive actionable insights from retail sales data using Excel, SQL, and Power BI. The objective was to explore sales performance metrics and visualize key trends, including top-selling products, regional performance, and monthly sales trends. 

# Sales Performance Analysis for a Retail Store
---
## Table of Contents
[Project Overview](#project-overview)

[Data Used](#data-used)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Results and Insights](#results-and-insights)

[Conclusion](#conclusion)

[Recommendations](#recommendations)
### Project Overview
I conducted an in-depth sales data analysis for a retail store in this project to provide actionable insights that drive business decisions. The objective was to explore key metrics such as top-selling products, regional sales performance, and monthly sales trends, culminating in an interactive Power BI dashboard. By leveraging Excel, SQL, and Power BI, I transformed raw sales data into a visual and comprehensive report that highlights the store’s sales performance.

### Data used:
The dataset used for this analysis is the **"Sales_data.csv"** file, containing detailed information about each sale made. It comprises of 8 columns;
1. Order ID
2. Customer Id
3. Product
4. Region
5. Order Date
6. Quantity
7. Unit Price
8. Total Sales

### Tools Used:
- **Excel**: For initial data exploration and pivot table analysis.
- **SQL**: This is used to query key insights such as top products, regional sales, and revenue trends.
- **Power BI**: This is used to visualize the findings through interactive dashboards.

### Data Cleaning and Preparation
In the initial data preparation phase, I performed the following tasks:
1. Data loading and inspection.
2. Handling missing variables.
3. Data cleaning and formatting.

### Exploratory Data Analysis
In this project, I analyzed the sales performance of a retail store by exploring key metrics such as **top-selling products**, **regional sales performance**, and **monthly trends**. The analysis follows three stages:

**1. Excel Analysis:**

The first step involved understanding the structure of the sales dataset and performing basic exploration using pivot tables and Excel formulas. This helped in revealing initial patterns and trends.

 - **Pivot Tables:**
   - **Summarize Total Sales by Product, Region, and Month:** Pivot tables provided an overview of how different products, regions, and periods (monthly) contributed to overall sales.
     
   - **Product Performance:** Total sales were broken down by product, highlighting which items are top-sellers.
     
   - **Regional Sales Trends:** Insights into which regions performed best and which are lagging.
     
   - **Monthly Sales Trends:** Identified seasonal fluctuations and monthly performance trends.
     
- **Formulas for Key Metrics:**
   - **Average Sales per Product:** This helped identify products that have consistent sales performance versus those with large fluctuations.
     
   - **Total Revenue by Region:** Calculates total income generated from each region, giving insight into geographic contributions.

**2. SQL Queries:**

The dataset was loaded into an SQL Server environment, structured queries were used to extract more detailed insights. 
- **Total Sales by Product Category:** This helped identify which categories are driving sales the most.
  
- **Sales Transactions by Region:** Provided a count of how many transactions are occurring in each region, reflecting customer activity levels.
  
- **Highest-Selling Product:** A query to determine which product has the highest sales value overall.
  
- **Total Revenue per Product:** Calculated how much revenue each product has generated, helping to compare the top-selling items.
  
- **Monthly Sales Totals for the Current Year:** Offered a view of how sales are trending month over month.
  
- **Top 5 Customers by Total Purchase Amount:** Identified the most valuable customers.
  
- **Regional Contribution to Total Sales:** Calculated the percentage of total sales contributed by each region.
  
- **Products with No Sales in the Last Quarter:** Flags products that have experienced a drop in sales, highlighting areas of concern.

**3. Power BI Dashboard:**

I translated these findings into a user-friendly and interactive dashboard.
- **Sales Overview:** Displays total sales, revenue trends, and comparisons of key metrics.
  
- **Top-Performing Products:** Visualizes which products generate the most revenue and sales volume.
  
- **Regional Breakdown:** A geographic visualization showing which regions are the most and least profitable.
  
- **Monthly Sales Trends:** Interactive charts displaying monthly sales fluctuations, helping spot trends and seasonal variations.

### Data Analysis
- _**Total sales for each product category**_
```SQL
SELECT Product, SUM(Total_Sales) AS TotalSales
FROM [dbo].[SalesData]
GROUP BY Product;
```

- _**Number of sales transactions in each region**_
```SQL
SELECT Region, COUNT(OrderID) AS NumberOfTransactions
FROM [dbo].[SalesData]
GROUP BY Region;
```

- _**Highest selling product by total sales value**_
```SQL
SELECT TOP 1 Product, SUM(Total_Sales) AS TotalSales
FROM [dbo].[SalesData]
GROUP BY Product
ORDER BY TotalSales DESC
```

- _**Total Revenue by product**_
``` SQL
SELECT Product, SUM(Total_Sales) AS TotalRevenue
FROM [dbo].[SalesData]
GROUP BY Product;
```

- _**Monthly Sales Total for the current year**_
```SQL
SELECT 
    MONTH(OrderDate) AS Month, 
    SUM(Total_Sales) AS MonthlySales
FROM [dbo].[SalesData]
WHERE YEAR(OrderDate) = YEAR(GETDATE()) 
GROUP BY MONTH(OrderDate);
```

- _**Top 5 customers by total purchase amount**_
```SQL
SELECT TOP 5 Customer_Id, SUM(Total_Sales) AS TotalPurchase
FROM [dbo].[SalesData]
GROUP BY Customer_Id
ORDER BY TotalPurchase DESC
```

- _**Percentage of Total Sales contributed by each region**_
```SQL
WITH TotalSalesCTE AS (
    SELECT SUM(Total_Sales) AS TotalSalesAmount 
    FROM [dbo].[SalesData]
)
SELECT 
    Region, 
    SUM(Total_Sales) AS RegionSales, 
    (SUM(Total_Sales) * 100.0 / (SELECT TotalSalesAmount FROM TotalSalesCTE)) AS PercentageContribution
FROM [dbo].[SalesData]
GROUP BY Region;
```

- _**Identify products with no sales in the last quarter**_
```SQL
SELECT Product
FROM [dbo].[SalesData]
GROUP BY Product
HAVING MAX(OrderDate) < DATEADD(QUARTER, -1, GETDATE());
```

- _**Average Sales per product**_
```Excel
=AVERAGEIF(Table1[Product],"Shirt",Table1[Total Sales])
```

- _**Total Revenue by region**_
```Excel
=SUMIF(Table1[Region],"North",Table1[Total Sales])
```

- _**Average Sales per Product**_
```DAX
 = Average(SalesData[Total Sales])
```

### Data Visualization
- **Using Excel**

![Total Sales by Product](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Total%20sales%20by%20product.png)

![Total Revenue by Region](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Total%20Revenue%20by%20Region.png)

![Monthly Sales Trend](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Monthly%20Sales%20trends.png)

![Total Sales by Product, Month & Region](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Total%20Sales%20by%20Product%20and%20Region.png)

![Slicer for Product & Region](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Slicer%20for%20Product%20and%20Region.png)


- **Using Power BI**

![Sales Performance Report Dashboard](https://github.com/Putsim/LITA_Sales_Analysis/blob/main/Power%20BI%20sd.png)

### Results and Insights
Here are the key findings and insights based on the data analysis:

- **Total and Average Sales**: 
  - Total sales generated amount to **$2.1 million**.
  - The **average sales per product** stand at **$212**.

- **Geographical Performance**:
  - **Regional Contribution to Total Sales**:
    - **South**: 44% (highest contributor).
    - **East**: 23%.
    - **North**: 19%.
    - **West**: 14% (lowest contributor).
  - The **South region** is both the best-performing and most profitable region.
  - The **West region** is the least-performing and least profitable region.

- **Product Performance**:
  - **Top-Selling Products**:
    - **Shoes**: $613k.
    - **Shirts**: $486k.
    - **Hats**: $316k.
  - Other product sales:
    - **Gloves**: $297k.
    - **Jackets**: $208k.
    - **Socks**: $181k.
  - **Top Sellers** are **Shoes, Shirts, and Hats**.

- **Monthly Sales Trends**:
  - **Peak Month**: February, with the highest sales at **$546,300**.
  - **Decline**: Sharp decline in sales following the peak in March.
  - **Lowest Month**: September recorded the lowest sales.
  - **Regional Peak Months**:
    - **South**: February.
    - **East**: July.
    - **North**: January.
    - **West**: August.

- **Customer Insights**:
  - **Top 5 Customers**: **CUS1431, CUS1495, CUS1005, CUS1115, and CUS1302**.

- **Quarterly Performance**:
  - All products had sales activity in the last quarter, indicating consistent demand across the product line.

These insights highlight regional and product-specific strengths, peak sales periods, and key customers, providing valuable direction for future strategic planning and targeted initiatives.

### Conclusion
The **South region** is the standout performer, driving the largest share of sales and profitability. **Shoes, Shirts, and Hats** emerge as top-selling products, contributing significantly to overall revenue. February marked the peak sales month, particularly for the South, though a notable drop followed in March. The **West region** lags in both sales and profitability, highlighting an area for potential improvement. Key customer contributions also underscore the importance of maintaining strong relationships with top buyers.

### Recommendations
1. **Focus on High-Performing Products and Regions**: Allocate more resources to **Shoes, Shirts, and Hats** in the **South region** to capitalize on high demand and profitability.
2. **Sales Growth Strategies for the West**: Implement targeted marketing and promotional efforts in the **West region** to boost its performance.
3. **Address Seasonal Trends**: Prepare for the peak **February sales** by ensuring stock availability and launching strategic promotions beforehand. Consider targeted campaigns during other regional peak months (e.g., July for East).
4. **Customer Retention and Relationship Management**: Strengthen engagement with the top 5 customers (e.g., personalized discounts or loyalty incentives) to encourage repeat business.

These steps will help maximize profitability, improve underperforming areas, and maintain momentum with key products and customers.


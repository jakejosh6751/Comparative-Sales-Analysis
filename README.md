# Comparative-Sales-Analysis

![comparative sales dashboard](https://github.com/jakejosh6751/Comparative-Sales-Analysis/blob/main/comparative%20sales%20dashboard.png)

### 1.	Project Overview

By analyzing Year-on-Year data, companies can identify trends, patterns, and areas for improvement, enabling informed strategic planning and goal setting.

Key reasons why companies should prioritize the development of these reports and unlock the power of financial dashboards and reporting templates includes, but not restricted to;
* Evaluating performance and progress;
* Identifying seasonal trends and patterns;
* Detecting anomalies and irregularities;
* Understanding customer behaviour; and
* Supporting financial forecasting.

This yearly comparison dashboard is designed for “Superstore” to compare key performance indicators (KPIs) over a 4-year period (2011 – 2014) for sales in the African region.

### 2.	Data Extraction

* Data is housed in SQL Server Management Studio database (Global Superstore Sales). There are 24 columns and 51,290 rows.
* A stored procedure (african_sales) is written to extract relevant data for this analysis from the “Global Superstore Sales” database. The query is filtered to return sales data for African countries only. The query result contains 8 columns and 4,587 rows.
* In Power BI, a connection to the data source is created to enable queries and dashboard updates when new data is added to the source table in the database. The SQL statement used is “execute african_sales;”

comparative sales stored procedure query:

```sql
create procedure african_sales
as
begin
	select	
			[Order ID],
			[Order Date],
			[Ship Mode],
			[Segment],
			[Country],
			[Category],
			[Sub-Category],
			[Sales]
	from
		[Global Superstore Sales]
	where
		Region = 'Africa'
end;
```

_african_sales query result (below)_:

![african_sales query result](https://github.com/jakejosh6751/Comparative-Sales-Analysis/blob/main/african_sales%20query%20result.png)

### 3.	Data Cleaning, Transformation & Modeling

* In Power Query, the data types of  “Order Date” and “Sales” are changed to date type and currency type ($) respectively.
* “Democratic Republic of the Congo” in the “Country” column is transformed to DR Congo.
* A “Calendar” table is created to hold dates from 2011 to 2014 with columns Date, Year, Month, and Quarter. The “Calendar” and “african_sales” tables are related on the “Date” and “Order Date” columns respectively.
* Measures are created for “Current Year Sales”, “Previous Year Sales”, “Year on Year Sales Growth %” and other relevant KPIs.

_comparative sales model diagram (below)_:

![comparative sales model diagram](https://github.com/jakejosh6751/Comparative-Sales-Analysis/blob/main/comparative%20sales%20model%20diagram.png)

### 4.	Data Visualization

* Card visuals are created for key performance indicators: “Current Year Sales”, “Previous Year Sales”, “Year on Year Sales Growth %” and “Year on Year Orders Growth %”.
* Line chart for “Current and Previous Year Sales by Country”.
* Line chart for “Current and Previous Year Sales by Month”.
* Clustered bar chart for “Current and Previous Year Sales by Segment”.
* Matrix chart showing “Current Year Sales”, “Previous Year Sales” and “Year on Year Sales Growth % by Category and Sub-category”.

_comparative sales dashboard (below)_:

![comparative sales dashboard](https://github.com/jakejosh6751/Comparative-Sales-Analysis/blob/main/comparative%20sales%20dashboard.png)
Interact with [Power BI report here](https://app.powerbi.com/groups/579e1741-4356-4184-93fb-13e61310efdc/reports/d4017250-464e-4403-8326-8921f853f2ee/ReportSection?experience=power-bi)

### 5.	Findings

```Fiscal year 2013-2014 insights from each chart:```

* Current and Previous Year Sales by Country;
	* For the 10 best countries in terms of 2014 sales, DR Congo, Nigeria, and Senegal recorded a decline in revenue.

* Current and Previous Year Sales by Month;
	* Generally, revenue growth is observed from 2013 to 2014 except for the conspicuous anomaly in February and a slight decline in July 2014.

* Current and Previous Year Sales by Segment;
	* A significant increase in sales for Consumer segment, slight increase for “Head Office” and a decline for “Corporate Segment”.

* Current Year Sales, Previous Year Sales, and Year on Year Sales Growth % by Category and Sub-category;
	* Increase of 14.3%, 26.2% & 27.7% on sales of furniture, office supplies, and technology categories respectively. However, 17.6% & 4.0% declines are observed for chairs and accessories respectively.

### 6.	Recommendations

* Further findings should be done to ascertain the cause of the anomaly in February sales in 2013 and 2014. It could be due to competition or alternative products in the market.
* The remarkable growth from $100k to $168k in sales from 2013 to 2014 signals possible untapped potential to drive sales for the Consumer Segment.

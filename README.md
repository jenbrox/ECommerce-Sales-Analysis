# eCommerce-Sales-Analysis
Power BI Dashboard
* Problem Statement
* Import Data in MS SQL Server
* Connect Power BI to MS SQL Database
* Clean Data
* Process Data
* Data Modelling
* Create Date Table
* Data Visualization
* Create Dashboard
* Generate Insights

### Problem Statement
A US based ecommerce business needs a real time sales performance dashboard to understand profitability, customer behavior, and product performance across the country. Leadership wants to monitor year-to-date sales, evaluate growth trends, and identify top- and bottom-performing categories, products, and regions to support strategic decision-making and revenue growth planning.

### ✅ Business Questions / Analytical Questions
📌 Sales & Growth Performance

What are our current YTD Sales, Profit, Quantity, and Profit Margin, and how do they compare to last year?

What is the YoY growth trend across key performance metrics?

Are we experiencing healthy and consistent monthly sales growth throughout the year?

What early indicators (sparklines) reveal positive or negative sales momentum?

📌 Category-Level Performance

Which product categories (Office Supplies, Technology, Furniture) are driving the most revenue?

How are YTD Sales performing vs. PYTD by category?

Which categories are growing or declining YoY and by what percentage?

Which categories require strategic focus to improve performance?

📌 Geographic Performance

Which states generate the highest and lowest sales revenue YTD?

Which US regions (East, West, South, Central) are performing best or underperforming?

Are there geographic opportunities to expand marketing or distribution?

📌 Product Insights

What are the Top 5 products contributing most to YTD sales?

Which Bottom 5 products are underperforming and may need attention (e.g., marketing, pricing, or removal)?

Are there patterns in product performance (SKU mix effectiveness)?

📌 Shipping & Operations

What percentage of YTD sales comes from each shipping method?

Which shipping method is most frequently used and does it correlate with profitability or order volume?

Should the company optimize shipping policies to drive profit margin or customer satisfaction?

✅ Strategic Insights Questions

These help you look like a BI consultant, not just a dashboard builder:

Where should the company focus to maximize revenue growth?

Which customer segments or regions show the greatest upsell or cross-sell potential?

What operational improvements (shipping, fulfillment, inventory levels) can drive cost efficiency?

Are there product categories losing traction that need pricing/marketing review?

Are there emerging high-value product opportunities based on YoY trends?


A US Based Ecommerce Sales Company wants a Sales Dashboard showing information of YTD Sales and generate insights for below scenarios -

* **Create a KPI Banner** showing YTD Sales, YTD Profit, YTD Quantity sold, YTD Profit Margin
* **Find Year on Year growth** for each KPI and show a YTD sparkline for each measure in the KPI to understand the monthly trend for each fact.
* **Find YTD Sales, PYTD Sales, YoY Sales growth** for different customer category. Add a trend icon for each category.
* **Find YTD Sales performance** by each State
* **Top 5 and Bottom 5 Products** by Sales
* **YTD Sales by Region** to know best and worst performing region all over country
* **YTD Sales by Shipping Type** to get the best shipping type percentage

### POWER BI FUNCTIONALITIES I WILL DISPLAY

* How to connect Power BI to MS SQL server and Flat Files
* Data Modelling with three tables
* Data cleaning in Power Query
* How to create a Date Table in Power BI
* Time Intelligence function (TOTALYTD, SAMEPERIODLASTYEAR, etc)
* Creating Dynamic and Complex KPI’s
* Basic to Advanced DAX Queries
* Conditional Formatting’s, Adding dynamic icons in Power BI
* Different DAX functions like Calculate, Sum, Sumx, Filter, values, selectedvalue, return, concatenate, divide, var, etc
* Creating different charts, maps and formatting them
* Generating insights from charts
* Export report

  ### step-by-step
* Study your data in Excel
* Import data in MS SQL Server DB
  * Open SSMS
  * Create Database under 'Databases'
  * right-click, Tasks -> Import Flat File, import each csv, and change all nvarchar(50) to varchar(50) under Modify Columns.
    *  nvarchar(50) to varchar(50) changes the character encoding from Unicode to a standard 8-bit non-Unicode character set, which can result in data loss if the column contains certain characters
  * right-click, new query, and `select * from <each table>` just to make sure imported correctly
* Connect Power BI to SSMS
  * Import Data from SQL Server and 'load' each table
  * If we go to the Model View tab, we see the tables are not connected. The thing connecting the tables are name and customer_state
  * drag and drop custome_state over on name and it creates a one to many relationship LOOK AT THIS AGAIN TO STUDY HOW THIS WORKS
* Create a Date Table
  * Whenever you have to determine YTD numbers, always remember to create a date table. This will help us to use time intelligence functions
  * Calendar = CALENDAR(MIN(ecommerce_data[order_date]), TODAY()) // <tableName = calendar dax function(minimum date, use today instead of max for dynamic purposes), since ours is a historical data though we have all of the dates, so can use max()
  * Year = YEAR('Calendar'[Date]) // creates new column named Year and extracts year from calendar date column
  * Month = FORMAT('Calendar'[Date], "mmmm") //gets month                       

* Creating the KPI
* ... 
* YoY Sales = ([YTD Sales] - [PYTD Sales]) / [PYTD Sales]
* to create up or down arrow: Sales Icon = var positive_icon = UNICHAR(9650)
            var negative_icon = UNICHAR(9660)
            VAR result = IF([YoY Sales]>0, positive_icon, negative_icon)
            return result

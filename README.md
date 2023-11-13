# Power BI Excercise

## Goal of this project

Create an exercise using Power BI.

## DAX
### Total Sales
*Total Gross Sales = SUM(Sheet1[Sales])*
### Total Profit
*Total Profit = sum(Sheet1[Profit])*
### Gross Profit Margin
*Gross Profit Margin = DIVIDE(Sheet1[Total Sales]-sum(Sheet1[COGS]),Sheet1[Total Sales])*
### Total sales by unit of time. Cumulative chart
1. Create new Calendar Table: *Calendar = CALENDAR(min(Sheet1[Date]), MAX(Sheet1[Date]))*.
2. Create new table: *_Measures*.
3. Create new measure inside table _Measures: *Sales Cumulative = CALCULATE(SUM(Sheet1[ Sales]), 'Calendar'[Date] <= MAX( 'Calendar'[Date]))*.
4. Visualization: line, x axis = *'Calendar'[Date]*, y axis = *Sales Cumulative*.
### Total sales with filters. Bar chart
Visualization created using Power BI tools. No DAX needed. Bar chart of sales by countries was created. Two filters (Product and Segment) were added.
### Total sales by territory, product, and customer. Table
Visualization created using Power BI tools. 
*Visulaizations>Build visual>Columns*:
1. Country.
2. Product.
3. Segment.
4. Sales (Sum of Sales).
### Gross Sales
Card with Sum of Gross Sales.
### Sales Growth Rate
#### General Formula
Growth by unit of time % = ((Gross Sales - Total Gross Sales) / Total Gross Sales) * 100
#### Code
1. Create a table *_All Measures*.
2. Inside *_All Measures* create a measure: *Total Gross Sales = SUM(Sheet1[Gross Sales])*.
3. Inside *_All Measures* create a measure: 
*Previous Month Gross Sales = CALCULATE('_All Measures'[Total Gross Sales], DATEADD('Calendar'[Date], -1, MONTH))*
4. Inside *_All Measures* create a measure: *MOM Previous Gross Sales % =*
    *VAR PMGrossSales =* 
        *CALCULATE('_All Measures'[Total Gross Sales], DATEADD('Calendar'[Date], -1, MONTH))*
    *RETURN* 
        *DIVIDE(([Total Gross Sales] - PMGrossSales), PMGrossSales)*.
5. To create the bar chart:
  - Drag *MOM Previous Gross Sales % =* from *Data>_All Measures* to the board. This movement creates the basic chart.
  - With the previously created chart highlighted, in *Visualizations>Build visual>Columns*, add *Calendar[Date]* at the top. Keep *Year* and *Month* only.
6. To create the table:
  - Insert a table.
  - In *Visualizations>Build visual>Columns* add the following: *'Calendar'[Date]* (Keep *Year* and *Month* only), *_All Measures[Total Gross Sales]*, *_All Measures[Previous Month Gross Sales]*, and *_All Measures[MoM Previous Month Sales %]*.
#### References
https://www.youtube.com/watch?v=6vJIAJNTdG0

## Bibliography
https://blog.enterprisedna.co/power-bi-financial-dashboard-examples/
https://www.investopedia.com/ask/answers/031815/what-formula-calculating-profit-margins.asp
https://www.youtube.com/watch?v=dMJLypl5HJg


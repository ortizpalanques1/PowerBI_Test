# Power BI Excercise

## Goal of this project

To share the instructions to build a simple dashboard comprehensive of valuable business metrics. Accordingly, our main contribution is this document with all the necessary DAX commands and formulas.
Because of the nature of the original data, some metrics are missing.
For this exercise, we took some of the measures recommended in https://blog.enterprisedna.co/power-bi-financial-dashboard-examples/.
## DAX
### Total Sales
*Total Gross Sales = SUM(Sheet1[Sales])*
### Total Profit
#### Measures and DAX
*Total Profit = sum(Sheet1[Profit])*
#### References
https://www.investopedia.com/terms/g/grossprofit.asp
### Gross Profit Margin
#### Measures and DAX
1. *Gross Profit Margin = DIVIDE(Sheet1[Total Sales]-sum(Sheet1[COGS]),Sheet1[Total Sales])*
2. Set the measure as Percentage.
#### References
https://www.investopedia.com/ask/answers/031815/what-formula-calculating-profit-margins.asp
### Total sales by unit of time. Cumulative chart
#### Measures, Tables, and DAX
1. Create new Calendar Table: *Calendar = CALENDAR(min(Sheet1[Date]), MAX(Sheet1[Date]))*.
2. Create a new table: *_Measures*.
3. Create new measure inside table _Measures: *Sales Cumulative = CALCULATE(SUM(Sheet1[ Sales]), 'Calendar'[Date] <= MAX( 'Calendar'[Date]))*.
4. Visualization: line, x axis = *'Calendar'[Date]*, y axis = *Sales Cumulative*.
#### References
https://www.youtube.com/watch?v=dMJLypl5HJg
### Total sales with filters. Bar chart
Visualization created using Power BI tools. No DAX is needed. We created a bar chart of sales by country. Finally, we added two filters (Product and Segment).
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
#### Measures and DAX
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
### Average Transaction Value
#### General Formula
Average Total Value = Total Sales / Total Transactions
#### Measures and DAX
1. In *Sheet1*, create a new measure: *Total Sales = sum(Sheet1[ Sales])*
2. In *Sheet1*, create a new measure: *Total Transactions = COUNTROWS(Sheet1)*
3. In *Sheet1*, create a new measure: *Average Transaction Value = DIVIDE(Sheet1[Total Sales], Sheet1[Total Transactions])*
#### References
https://yourcareersupport.com/how-to-calculate-atv/#:~:text=How%20To%20Calculate%20ATV%20%28With%20Formula%2C%20Examples%20and,It%20follows%20the%20same%20formula%20and%20calculation%20method.
### Operating Income
Insufficient data
### Gross Margin
#### General Formula
Gross Margin = (Net Sales - COGS) / Net Sales
#### Measures and DAX
1. Inside the table *Sheet1* create a measure *Gross Margin = DIVIDE(([Total Sales] - sum(Sheet1[COGS])), [Total Sales])*
2. Create a new *Card* and drag the measure *Gross Marging* in it. 
#### References
https://www.investopedia.com/terms/g/grossmargin.asp
### Revenue
#### General Formula (Net Revenue)
Net Revenue = Net Revenue = (Quantity Sold * Unit Price) - Discounts - Allowances - Returns
Quantity Sold * Unit Price = Sum of Gross Sales
#### Measures and DAX
1. Due to the absence of data on allowances and returns, this measure is equivalent to *Total Sales*.
2. In *Sheet1* create a new measure *Net Revenue = SUM(Sheet1[Gross Sales]) - SUM(Sheet1[Discounts])*.
3. Create a new *Card* and drag the measure *Net Revenue* in it.
#### References
https://www.investopedia.com/terms/r/revenue.asp


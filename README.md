# Power BI Excercise

## Goal of this project

Create an exercise using Power BI.

## DAX
### Total Sales
Total Gross Sales = SUM(Sheet1[Sales])
### Total Profit
Total Profit = sum(Sheet1[Profit])
### Gross Profit Margin
Gross Profit Margin = DIVIDE(Sheet1[Total Sales]-sum(Sheet1[COGS]),Sheet1[Total Sales])
#### Total sales by unit of time. Cumulative chart
1. Create new Calendar Table: Calendar = CALENDAR(min(Sheet1[Date]), MAX(Sheet1[Date])).
2. Create new table: _Measures.
3. Create new measure inside table _Measures: Sales Cumulative = CALCULATE(SUM(Sheet1[ Sales]), 'Calendar'[Date] <= MAX( 'Calendar'[Date])).
4. Visualization: line, x axis = 'Calendar'[Date], y axis = Sales Cumulative.

## Bibliography
https://blog.enterprisedna.co/power-bi-financial-dashboard-examples/
https://www.investopedia.com/ask/answers/031815/what-formula-calculating-profit-margins.asp
https://www.youtube.com/watch?v=dMJLypl5HJg


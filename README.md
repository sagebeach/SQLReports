# SQLReports

**I was tasked with learning to generate reports using SQL Server Reporting Services.**

Starting out from scratch I set up a new SQL server and configured a local SQL Reporting Server.

Using the AdventureWorks Sample Database I generated a report featuring three methods of Data presentation.

First a short query to create an actionable dataset

''' SQL
SELECT  soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal) AS LineTotal
FROM  Sales.SalesPerson AS sp INNER JOIN
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN
      Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID
INNER JOIN
      Production.Product AS pp ON sd.ProductID = pp.ProductID INNER JOIN
      Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID INNER JOIN
      Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID
GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID
HAVING  (ppc.Name = 'Clothing')
'''

Then I used the Dataset to display the dataset in tabular form sorted by the Order No
![alt text](https://github.com/sagebeach/SQLReports/blob/master/TabularData1.PNG "First rows of the data table")

Included in the report are relevant totals for the items
![alt text](https://github.com/sagebeach/SQLReports/blob/master/TabularData2.PNG "Last rows of the data table")

Next I created a bar graph displaying the quantity of each product sold over the span of time stored in the database. This would be useful for product sales analysis.

![alt text](https://github.com/sagebeach/SQLReports/blob/master/QuantityOverTime.png "Quantity of product sold over time")

Finally I included a line graph that displays the sales figures (line total) of each product over time. Useful for market analysis or predicting future sales trends.

![alt text](https://github.com/sagebeach/SQLReports/blob/master/SalesOverTime.PNG "line total sales figures over time")

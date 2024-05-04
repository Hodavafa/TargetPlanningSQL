**COUNT with WHERE Clause:**

1. - Count the number of orders with a total line amount greater than $1000.
   
   ```sql
   SELECT COUNT(*) AS HighValueOrders
   FROM Sales.SalesOrderDetail
   WHERE LineTotal > 1000;
   ```
   
   Sample output:
   
   ```
   HighValueOrders
   157
   ```

2. **SUM with GROUP BY Clause:**
   
   - Calculate the total sales amount for each product category.
   
   ```sql
   SELECT PC.Name AS ProductCategory, SUM(SOD.LineTotal) AS TotalSales
   FROM Sales.SalesOrderDetail AS SOD
   INNER JOIN Production.Product AS P ON SOD.ProductID = P.ProductID
   INNER JOIN Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID
   INNER JOIN Production.ProductCategory AS PC ON PS.ProductCategoryID = PC.ProductCategoryID
   GROUP BY PC.Name;
   ```
   
   Sample output:
   
   ```
   ProductCategory | TotalSales
   --------------------------------
   Bikes           | 2655478.56
   Components      | 1818968.56
   ...
   ```

3. **AVG with HAVING Clause:**
   
   - Calculate the average order quantity for products with at least 10 orders.
   
   ```sql
   SELECT P.Name AS ProductName, AVG(SOD.OrderQty) AS AvgOrderQty
   FROM Sales.SalesOrderDetail AS SOD
   INNER JOIN Production.Product AS P ON SOD.ProductID = P.ProductID
   GROUP BY P.Name
   HAVING COUNT(*) >= 10;
   ```
   
   Sample output:
   
   ```
   ProductName    | AvgOrderQty
   ------------------------------
   Adjustable Race| 21.8571
   ...
   ```

4. **MAX with Subquery:**
   
   - Find the maximum order quantity for products in the 'Mountain Bikes' subcategory.
   
   ```sql
   SELECT MAX(SOD.OrderQty) AS MaxOrderQty
   FROM Sales.SalesOrderDetail AS SOD
   INNER JOIN Production.Product AS P ON SOD.ProductID = P.ProductID
   INNER JOIN Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID
   WHERE PS.Name = 'Mountain Bikes';
   ```
   
   Sample output:
   
   ```
   MaxOrderQty
   44
   ```

5. **MIN with JOIN and WHERE Clause:**
   
   - Find the minimum unit price for products sold after a certain date.
   
   ```sql
   SELECT MIN(SOD.UnitPrice) AS MinUnitPrice
   FROM Sales.SalesOrderDetail AS SOD
   INNER JOIN Sales.SalesOrderHeader AS SOH ON SOD.SalesOrderID = SOH.SalesOrderID
   WHERE SOH.OrderDate >= '2023-01-01';
   ```
   
   Sample output:
   
   ```
   MinUnitPrice
   1.99
   ```

6. **GROUPING SETS:**
   
   1. - `GROUPING SETS` allows you to specify multiple groupings in a single query. You can define different combinations of groupings to get various levels of summarization.
      
      ```sql
      SELECT 
          PS.Name AS SubcategoryName,
          PC.Name AS CategoryName,
          SUM(SOD.LineTotal) AS TotalSales
      FROM 
          Sales.SalesOrderDetail AS SOD
      INNER JOIN 
          Production.Product AS P ON SOD.ProductID = P.ProductID
      INNER JOIN 
          Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID
      INNER JOIN 
          Production.ProductCategory AS PC ON PS.ProductCategoryID = PC.ProductCategoryID
      GROUP BY 
          GROUPING SETS ((PS.Name), (PC.Name), ());
      ```
      
      This query calculates the total sales amount for each product subcategory and product category, as well as the grand total. The `GROUPING SETS` clause allows us to specify individual groupings for subcategory, category, and a grand total.
   
   2. **ROLLUP:**
      
      - `ROLLUP` is a shorthand for `GROUPING SETS` and is used to create subtotals and grand totals for a specified list of columns.
      
      ```sql
      SELECT 
          PS.Name AS SubcategoryName,
          PC.Name AS CategoryName,
          SUM(SOD.LineTotal) AS TotalSales
      FROM 
          Sales.SalesOrderDetail AS SOD
      INNER JOIN 
          Production.Product AS P ON SOD.ProductID = P.ProductID
      INNER JOIN 
          Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID
      INNER JOIN 
          Production.ProductCategory AS PC ON PS.ProductCategoryID = PC.ProductCategoryID
      GROUP BY 
          ROLLUP (PC.Name, PS.Name);
      ```
      
      This query produces a similar result to the previous query but uses the `ROLLUP` operator to generate subtotals and grand totals for the product category and subcategory.
   
   

**INNER JOIN:**

1. - Returns rows when there is at least one match in both tables.
   
   ```sql
   SELECT P.Name AS ProductName, S.Name AS SubcategoryName
   FROM Production.Product AS P
   INNER JOIN Production.ProductSubcategory AS S 
   ON P.ProductSubcategoryID = S.ProductSubcategoryID;
   ```
   
   Sample output:
   
   ```
   ProductName         | SubcategoryName
   -----------------------------------------
   ML Mountain Frame   | Mountain Bikes
   HL Mountain Frame   | Mountain Bikes
   Road-250 Black, 58 | Road Bikes
   ...
   ```

2. **LEFT JOIN:**
   
   - Returns all rows from the left table and the matched rows from the right table. If no match is found, NULL values are returned for the columns from the right table.
   
   ```sql
   SELECT P.Name AS ProductName, ISNULL(S.Name, 'No Subcategory') AS SubcategoryName
   FROM Production.Product AS P
   LEFT JOIN Production.ProductSubcategory AS S 
   ON P.ProductSubcategoryID = S.ProductSubcategoryID;
   ```
   
   Sample output:
   
   ```
   ProductName         | SubcategoryName
   -----------------------------------------
   ML Mountain Frame   | Mountain Bikes
   HL Mountain Frame   | Mountain Bikes
   Road-250 Black, 58 | Road Bikes
   ...
   Headset             | No Subcategory
   ```

3. **RIGHT JOIN:**
   
   - Returns all rows from the right table and the matched rows from the left table. If no match is found, NULL values are returned for the columns from the left table.
   
   ```sql
   SELECT ISNULL(P.Name, 'No Product') AS ProductName, S.Name AS SubcategoryName
   FROM Production.Product AS P
   RIGHT JOIN Production.ProductSubcategory AS S 
   ON P.ProductSubcategoryID = S.ProductSubcategoryID;
   ```
   
   Sample output:
   
   ```
   ProductName         | SubcategoryName
   -----------------------------------------
   ML Mountain Frame   | Mountain Bikes
   HL Mountain Frame   | Mountain Bikes
   Road-250 Black, 58 | Road Bikes
   ...
   No Product          | Tires and Tubes
   ```

4. **FULL OUTER JOIN:**
   
   - Returns all rows when there is a match in either the left or right table. If there is no match, NULL values are returned for the missing side.
   
   ```sql
   SELECT ISNULL(P.Name, 'No Product') AS ProductName, ISNULL(S.Name, 'No Subcategory') AS SubcategoryName
   FROM Production.Product AS P
   FULL OUTER JOIN Production.ProductSubcategory AS S 
   ON P.ProductSubcategoryID = S.ProductSubcategoryID;
   ```
   
   Sample output:
   
   ```
   ProductName         | SubcategoryName
   -----------------------------------------
   ML Mountain Frame   | Mountain Bikes
   HL Mountain Frame   | Mountain Bikes
   Road-250 Black, 58 | Road Bikes
   ...
   No Product          | Tires and Tubes
   Helmet              | No Subcategory
   ```

5. **CROSS JOIN:**
   
   - Returns the Cartesian product of the two tables, i.e., all possible combinations of rows from both tables.
   
   ```sql
   SELECT P.Name AS ProductName, S.Name AS SubcategoryName
   FROM Production.Product AS P
   CROSS JOIN Production.ProductSubcategory AS S;
   ```
   
   Sample output:
   
   ```
   ProductName         | SubcategoryName
   -----------------------------------------
   ML Mountain Frame   | Mountain Bikes
   ML Mountain Frame   | Road Bikes
   ML Mountain Frame   | Touring Bikes
   ...
   ```

6. **Multiple Joining Tables**

In this example, we'll join four tables: Product, ProductSubcategory, ProductCategory, and SalesOrderDetail.

```sql
SELECT 
    P.Name AS ProductName,
    PS.Name AS SubcategoryName,
    PC.Name AS CategoryName,
    SOD.OrderQty,
    SOD.UnitPrice,
    SOD.LineTotal
FROM 
    Sales.SalesOrderDetail AS SOD
INNER JOIN 
    Production.Product AS P ON SOD.ProductID = P.ProductID
INNER JOIN 
    Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID
INNER JOIN 
    Production.ProductCategory AS PC ON PS.ProductCategoryID = PC.ProductCategoryID;
```

This query retrieves data from the SalesOrderDetail table along with related information from the Product, ProductSubcategory, and ProductCategory tables. 

```
ProductName                | SubcategoryName  | CategoryName   | OrderQty | UnitPrice | LineTotal
------------------------------------------------------------------------------------------------
Adjustable Race           | Headsets         | Accessories     | 1        | 100.00    | 100.00
Bearing Ball              | Bearings         | Components      | 2        | 10.00     | 20.00
BB Ball Bearing           | Bearings         | Components      | 2        | 20.00     | 40.00
HL Mountain Frame - Black | Mountain Frames  | Bikes           | 1        | 829.00    | 829.00
HL Mountain Frame - Black | Mountain Frames  | Bikes           | 1        | 829.00    | 829.00
Road-150 Red, 48          | Road Frames      | Bikes           | 1        | 1431.50   | 1431.50
...
```

This output combines product details with sales order information, including the product name, subcategory name, category name, order quantity, unit price, and line total. The multiple joins allow us to retrieve relevant data from different tables and combine them into a single result set for analysis or reporting purposes.



1. **Filtering on Joined Tables:**
   
   * **`ON` clause:** Use this when you want to filter rows before the join operation. If you need to limit the rows being joined, it's generally better to include the condition in the `ON` clause. This can potentially improve performance by reducing the number of rows processed during the join.
   
   * **`WHERE` clause:** Use this when you want to filter the result set after the join operation. If you want to filter based on columns from tables that are not part of the join condition, you'll need to use the `WHERE` clause.

2. **Performance Considerations:**
   
   * Placing conditions in the `ON` clause can sometimes improve performance, especially when joining large tables. Filtering before the join reduces the number of rows that need to be processed and joined together.
   
   * However, in some cases, it might not make a significant difference in performance, especially with modern query optimizers that can optimize both `ON` and `WHERE` conditions effectively.

3. **Clarity and Readability:**
   
   * Using conditions in the `WHERE` clause might make the query more readable, especially if the filtering is based on criteria unrelated to the join itself.
   
   * Placing all join-related conditions in the `ON` clause can make the query more compact and easier to understand if the filtering is directly related to the join operation.

4. **Specific Use Cases:**
   
   * If you're inner joining and the filtering condition is directly related to the join (e.g., filtering on the joined columns), it's often best to use the `ON` clause.
   
   * If you're performing an outer join or need to filter based on columns from both joined tables, you may need to use both `ON` and `WHERE` clauses.



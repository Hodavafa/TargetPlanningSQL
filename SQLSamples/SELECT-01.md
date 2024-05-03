# Retrieving Data with SELECT

The `SELECT` command is fundamental in SQL and is used to retrieve data from a database. Let's break down how to use the `SELECT` command with the AdventureWorks sample database.

**Selecting All Columns from a Table:**
To select all columns from a table, you use the asterisk (*) symbol after the `SELECT` keyword:

```sql
SELECT * FROM TableName;
```

For example, to select all columns from the `Product` table:

```sql
SELECT * FROM Production.Product;
```

```sql
ProductID | Name             | ListPrice | Color  | Size
---------------------------------------------------------
1         | Adjustable Race  | 50.99     | NULL   | NULL
2         | Bearing Ball     | 10.00     | NULL   | NULL
3         | BB Ball Bearing  | 20.00     | NULL   | NULL
...       | ...              | ...       | ...    | ...

```

**Selecting Specific Columns:**
If you only want to retrieve specific columns from a table, you can specify them after the `SELECT` keyword:

```sql
SELECT Column1, Column2, ... FROM TableName;
```

For example, to select only the `ProductID` and `Name` columns from the `Product` table:

```sql
SELECT ProductID, Name FROM Production.Product;
```

```sql
ProductID | Name             
-----------------------------
1         | Adjustable Race  
2         | Bearing Ball     
3         | BB Ball Bearing  
...       | ...              

```

**Filtering Rows with WHERE Clause:**
You can filter rows using the `WHERE` clause. This allows you to specify conditions that the rows must meet to be included in the result set:

```sql
SELECT * FROM TableName
WHERE Condition;
```

For example, to select products with a list price greater than $100:

```sql
SELECT * FROM Production.Product
WHERE ListPrice > 100;
```

```sql
ProductID | Name             | ListPrice | Color  | Size
---------------------------------------------------------
456       | ML Mountain Frame| 215.00    | Black  | 44
789       | HL Mountain Frame| 829.00    | Black  | 42
...       | ...              | ...       | ...    | ...

```

**Combining Conditions with Logical Operators:**
You can use logical operators such as `AND`, `OR`, and `NOT` to combine multiple conditions in the `WHERE` clause:

```sql
SELECT * FROM TableName
WHERE Condition1 AND/OR Condition2;
```

For example, to select products with a list price greater than $100 and have 'Black' Color:

```sql
SELECT * FROM Production.Product
WHERE ListPrice > 100 AND Color = 'Black'
```

```sql
ProductID | Name             | ListPrice | Color  | Size
---------------------------------------------------------
456       | ML Mountain Frame| 215.00    | Black  | 44
789       | HL Mountain Frame| 829.00    | Black  | 42
...       | ...              | ...       | ...    | ...

```

**Ordering Results with ORDER BY Clause:**
You can sort the result set using the `ORDER BY` clause:

```sql
SELECT * FROM TableName
ORDER BY ColumnName [ASC|DESC];
```

For example, to select products from the `Product` table ordered by list price in descending order:

```sql
SELECT * FROM Production.Product
ORDER BY ListPrice DESC;
```

```sql
ProductID | Name             | ListPrice | Color  | Size
---------------------------------------------------------
789       | HL Mountain Frame| 829.00    | Black  | 42
123       | Road Frame       | 599.99    | Black  | 58
...       | ...              | ...       | ...    | ...

```

These are some basic examples of how to use the `SELECT` command with the AdventureWorks sample database. 

You can further explore SQL by experimenting with different queries and clauses.

# Introduction

**What is SQL?** 

sql stands for structured query language, a query language used to query huge volume of data.


Today, i will be using **Microsoft SQL Server** to teach you sql.  And what we will learn will be compatible with **Oracle, Ibm db2** as well as **MySql**. So, basically, sql is a language that can be run on any database server.

We will download a database sample called **AdventureWorks**, initially. A typical question would be…**Why this database particularly**? The reason is that this database contains **extensive** details of **human resource employees, person details, sales** as well as alot of **detailed data**. So, it is indeed a perfect database to practice any freshly learnt techniques on.

Head to this link: https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver15&tabs=ssms and swipe up.

![AdventureWorks](https://user-images.githubusercontent.com/76493518/164912755-319e36c9-19d0-4775-9e0c-61e9b8e05e62.png)

In this tutorial, We will learn by using AdventureWorks version 2019 OLTP, depending on your sql server version, you can choose whichever version that best suits your needs.
After you download your .bak file, you need to copy it to a specific folder in order to complete the full configuration and be set to go.

After you download your .bak file, you need to copy it to a specific folder in order to complete the full configuration and be set to go.

"Local Disk (C:) >> Program Files >> Microsoft SQL Server >> MSSQL15.MSSQLSERVER (Your local server name) >> MSSQL >> Backup"

The path above is the path where you should copy your newly downloaded .bak file, otherwise, you won't be able to follow along.

![Backup](https://user-images.githubusercontent.com/76493518/164913098-8b6bdb00-1a86-4629-af94-a6f957205e88.png)

Once you have completed this step, you then need to open "Object explorer" >> right click on databases >> restore database >> In General section choose "Device" then click on the three dots at the very right side, choose the media type to be a file then click add and choose your "AdventureWorks.bak" file.

![Restore database](https://user-images.githubusercontent.com/76493518/164913119-ca18018c-06eb-4842-9f6b-045c0c7ff742.png)


Once restored successfully, it should appear under databases folder.

![database](https://user-images.githubusercontent.com/76493518/164913149-0aa0d424-cb58-4f47-8243-0bdc352b03a6.png)

When you expand the database by clicking the "+" sign, a list of folders will appear, our focus now will go towards the tables folder.
Once you expand it, you will see lots of tables appear in front of you. An important concept to learn is that there're two names separated with a dot (.) sign, the one on the left side is the schema name while the other is the table name.

![schema](https://user-images.githubusercontent.com/76493518/164913675-af1870e6-4df2-4327-a86b-8c606eb754ac.png)

Henceforward, We're going to be executing sql queries in order to further interact with our Tables, schema, columns, etc…

![New query](https://user-images.githubusercontent.com/76493518/164913690-983ce5ec-aafd-4f07-bee3-ee433fa38bbe.png)

---

Press on that button then you'll be prompted to enter your first ever sql query in this course. :)

# SELECT statement

```USE databaseName;```
Command is used to switch to a **different** database. For instance, if you're on a database called "_My_Database_" and you execute the following command "USE  AdventureWorks2019", you have now switched to execute queries on **AdventureWorks2019** database.

```SELECT * FROM tableName;```
The asterisk sign here refers to (ALL), so this query selects **all columns** from a specified **table**. Therefore, if you wish to extract a specific column from a table you'de mention it instead of the asterisk sign as show in the example below.

```SELECT BusinessEntityID,JobTitle FROM HumanResources.Employee;```

> HumanResources is the **_schema_** name while Employee is the **_table_** we show columns from.

This query displays only "BusinessEntityID" and "JobTitle" columns from the **Employee** table.
Notice that we separate column names we wish to see with a **comma** sign "**,**"

## DISTINCT

```SELECT DISTINCT JobCandidateID FROM HumanResources.JobCandidate;```
Try excuting that query and notice the difference; Simply, DISTINCT **filter out unique values**. Which means you won't find any duplicates in the results.

```SELECT BusinessEntityID,JobTitle FROM HumanResources.Employee WHERE JobTitle = 'Research and Development Manager';```
This displays **BusinessEntityID** and **JobTitle** columns but the **JobTitle** column where it's content matches only the string 'Research and Development Manager'.

```SELECT SubTotal, TaxAmt, SubTotal + TaxAmt FROM Purchasing.PurchaseOrderHeader;```
Displays SubTotal, TaxAmt and the **sum** of both by using the **+** operator.
But if you notice, the third column which displays the sum Doesn't have a name. The query below will ad a temporary name to that column using an **_ALIAS_**.

``` SELECT SubTotal, TaxAmt, SubTotal + TaxAmt AS SubTotalWithTaxAmt FROM Purchasing.PurchaseOrderHeader;```

The third column was added with **SubTotalWithTaxAmt** temporary name by using an ALIAS (AS).

```SELECT SubTotal, TaxAmt, SubTotal + TaxAmt FROM Purchasing.PurchaseOrderHeader WHERE SubTotal + TaxAmt > 500;```

This query does the same as the previous one but diplays only the results where the **sum** of **SubTotal** + **TaxAmt** is **greater than** 500.

```SELECT FirstName, MiddleName, LastName, FirstName + MiddleName + LastName AS FullName FROM Person.Person;```

Displays **FirstName, MiddleName** and **LastName** columns and adds a temporarily named column **FullName** with all the previous results concatenated together. Notice here it concatenated because what we added were **_strings_** and not integers.

One way to solve this and make our fourth column look better is by adding spaces before each column as shown here:

* ```SELECT FirstName, MiddleName, LastName, FirstName + ' ' + MiddleName + ' ' + LastName AS FullName FROM Person.Person;```


# NULL values
**What are NULL values?**
NULL values are **unknown** or **missing** values that you can't define a particular value to. Consequently, we use NULL values to refer to any **empty** or **unknown** result.

```SELECT FirstName, MiddleName, LastName FROM Person.Person WHERE MiddleName IS NULL;```
Displays **FirstName, MiddleName** and **LastName** columns where the **MiddleName** column equals to NULL.
Similarly, If we executed the following query it would display the same results but **MiddleName column** is **_NOT_** equal NULL.
* ```SELECT FirstName, MiddleName, LastName FROM Person.Person WHERE MiddleName IS **NOT** NULL;```

# Operators
## AND
Let's say we want to get the results where **MartialStatus** equals to **"S"** and **Gender** equals to female, in this case, **"F"** ;

```SELECT * FROM HumanResources.Employee WHERE MartialStatus = 'S' AND Gender = 'F'```

## OR
For some reason we want to display all **Employees** whose job titles **are either** 'Design Engineers' **OR** 'Research and Development Manager', execute the following query and observe the results.

```SELECT * FROM HumanResources.Employee WHERE JobTitle = 'Design Engineer' OR JobTitle = 'Research and Development Manager';```

## IN
In the previous example we have used JobTitle **_twice_** using **OR** to show specific results, while in fact, using the same column twice in a query isn't considered as best practice. Therefore, when required to test a particular column multiple times **IN** operator comes into play. 

```SELECT * FROM HumanResources.Employee WHERE JobTitle IN ('Design Engineer', 'Research and Development Manager');```

* **Same as** ```SELECT * FROM HumanResources.Employee WHERE JobTitle = 'Design Engineer' OR JobTitle = 'Research and Development Manager';```



```SELECT * FROM HumanResources.Employee WHERE BusinessEntityID IN (1,5,10,15);```

* **Same as** ```SELECT * FROM HumanResources.Employee WHERE BusinessEntityID = '1' OR BusinessEntityID = '5' OR BusinessEntityID = '10' OR BusinessEntityID = '15';```

## BETWEEN

```SELECT * FROM HumanResources.Employee WHERE BusinessEntityID BETWEEN 1 AND 50;```

Displays results from BusinessEntityID between 1 and 50 only.

## LIKE
LIKE operator is used to match a specific regular expression, for intsance, if we want to display results from **NAME** column where the name starts with letter **A** then we would execute this query;
* ```SELECT * FROM Person.StateProvince WHERE Name LIKE 'A%';```

Correspondingly, executing the following query would display results ending with letter **"O"**:
* ```SELECT * FROM Person.StateProvince WHERE Name LIKE '%O';```

# SORTING
We use sorting whenever we wish to see our results ordered either by **Ascending** order or **Descending** order.

```SELECT City, PostalCode FROM Person.Address ORDER BY City```

This displays **City** column and **PostalCode** column but arranges City column by **ascending** order by default (since we didn't specify an order).

The following query, alternatively, displays the same but in **Descending** order.

* ```SELECT City, PostalCode FROM Person.Address ORDER BY City DESC```
> Note the DESC operator at the end

```SELECT FirstName, LastName, MiddleName FROM Person.Address WHERE MiddleName IS NOT NULL ORDER BY FirstName DESC, LastName ASC;```

This will show results of mentioned tables but arrange them by **Descending** order for **FirstName** column and **Ascending** order for **LastName** column.

# GROUP BY
**Group by** clause is used to arrange results together **Per category**.
Let's say this command ```SELECT SalesOrderId, UnitPrice FROM sales.salerorderdetail;```
will display the following

![image](https://user-images.githubusercontent.com/76493518/165004592-c8b72179-9863-41b2-9d6a-1a68fb672dd8.png)

In the **SalesOrderId** column, there're several results of **sales ID** with the same number "**43659**" but showing different **Unit price** for each one.
We could use the following command if we want to group the same **Sales ID** into only one result and display the **_TOTAL_** of **Unit prices**.

```SELECT SalesOrderId, SUM(UnitPrice) FROM sales.salesorderdetail GROUP BY SalesOrderId```

![Grouped by](https://user-images.githubusercontent.com/76493518/165021365-f901b63b-d1e2-4ae3-b96d-9f5649a977b2.png)

> Now we can see only 1 sales order in each result with it's Unit price sum

# AVG(),COUNT(),MAX(),MIN()

```SELECT SalesOrderId, AVG(UnitPrice) FROM sales.salesorderdetail GROUP BY SalesOrderId```
> Shows the **_average_** of **Unit Price** per **Sales Order**

![image](https://user-images.githubusercontent.com/76493518/165022789-7ee7047c-e5bb-487a-a42f-0142266d0324.png)

```SELECT SalesOrderId, COUNT(UnitPrice) FROM sales.salesorderdetail GROUP BY SalesOrderId```
> Shows the **_total_** of **Unit Price** per **Sales Order**

![image](https://user-images.githubusercontent.com/76493518/165023089-8ea9c6b6-6c99-4dff-9dfe-670d967725a5.png)

```SELECT SalesOrderId, MAX(UnitPrice) FROM sales.salesorderdetail GROUP BY SalesOrderId```
> Shows the **_maximum_ Unit Price** per **Sales Order**
![image](https://user-images.githubusercontent.com/76493518/165023228-c5a3c210-b572-4515-83eb-1396d6f2d082.png)

# STRINGS

## CONCAT()
```SELECT FirstName, MiddleName, LastName, CONCAT(FirstName, ' ', MiddleName, ' ', LastName) AS FullName FROM Person.Person WHERE MiddleName IS NOT NULL;```

This query will add a third column named **FullName** and Concatenates all the three names together as a full name. It acts exactly here like the **+** operator.

![image](https://user-images.githubusercontent.com/76493518/165636744-1f8288c9-29c5-4994-be08-630a5e3372ef.png)

## LENGTH()
* As the name suggests, This clause let's you know the **how many characters** a specific string has.

![image](https://user-images.githubusercontent.com/76493518/165637304-cfc2fb57-5021-4fa9-a957-724d4ae4fc01.png)

## LEFT(),RIGHT()
* If i want to extract, for example, 3 characters from the left of a string i use the **LEFT()** function.

>> **LEFT()** and **RIGHT()** functions take two arguments, in the first argument you specify the column name containing the string and the second how many letters you with to show from a string.


```Select FirstName, LEFT(FirstName, 3) AS FirstThreeLetters FROM Person.Person;```

This query will display the **First three letters** of each result in **FirstName** column in a second column called **FirstThreeLetters**.

![image](https://user-images.githubusercontent.com/76493518/165637457-8a2c269c-e953-4446-82cf-364701b96660.png)

## SUBSTRING()
* SUBSTRING() Function takes 3 arguments, the first one is the column that has our string, second is the index we wish to start counting from while the third one is the number of string we wish to display.

```SELECT Firstname, SUBSTRING(FirstName, 3, 4) FROM Person.Person;```

>> This query will display all **Strings** starting from the **third letter** and will show only 4 letters

![image](https://user-images.githubusercontent.com/76493518/165640698-7d549999-325b-414b-8b6c-88620957f8ef.png)

>> As you might have noticed, the first result showed only 2 letters since the name **"Syed"** has only 4 letters then it started counting from the **third** letter "e" till the end. On the other hand, **"Catherine"** has more than 4 letters and it started counting from the **Third letter** "t" till "r".

# DATE()
## DAY()

* ```SELECT SalesOrderId,OrderDate, DAY(OrderDate) AS extractDay FROM Sales.SalesOrderHeader;```

Displays **SalesOrderId**, **OrderDate** columns and the **_DAY_** of the **Order** in a third column called **extractDay**.

![image](https://user-images.githubusercontent.com/76493518/165644092-9cffd006-5c24-40c1-bd3c-7abfac8a6103.png)

## MONTH()

* ```SELECT SalesOrderId,OrderDate, MONTH(OrderDate) AS extractMonth FROM Sales.SalesOrderHeader;```

Displays **SalesOrderId**, **OrderDate** columns and the **_MONTH_** of the **Order** in a third column called **extractMonth**

![image](https://user-images.githubusercontent.com/76493518/165644350-a1eaa2d0-31b9-428f-9337-4efd7d0d4a8f.png)

# HAVING

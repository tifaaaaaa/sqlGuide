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

## USE databaseName;
Command is used to switch to a **different** database. For instance, if you're on a database called "_My_Database_" and you execute the following command "USE  AdventureWorks2019", you have now switched to execute queries on **AdventureWorks2019** database.

## SELECT * FROM tableName;
The asterisk sign here refers to (ALL), so this query selects **all columns** from a specified **table**. Therefore, if you wish to extract a specific column from a table you'de mention it instead of the asterisk sign as show in the example below.

## SELECT BusinessEntityID,JobTitle FROM HumanResources.Employee;
### HumanResources is the **_schema_** name while Employee is the **_table_** we show columns from.
This query displays only "BusinessEntityID" and "JobTitle" columns from the **Employee** table.
Notice that we separate column names we wish to see with a **comma** sign "**,**"

## SELECT DISTINCT JobCandidateID FROM HumanResources.JobCandidate;
Try excuting that query and notice the difference; Simply, DISTINCT **filter out unique values**. Which means you won't find any duplicates in the results.

## SELECT BusinessEntityID,JobTitle FROM HumanResources.Employee WHERE JobTitle = 'Research and Development Manager';
This displays **BusinessEntityID** and **JobTitle** columns but the **JobTitle** column where it's content matches only the string 'Research and Development Manager'.

## SELECT SubTotal, TaxAmt, SubTotal + TaxAmt FROM Purchasing.PurchaseOrderHeader;
Displays SubTotal, TaxAmt and the **sum** of both by using the **+** operator.
But if you notice, the third column which displays the sum Doesn't have a name. The query below will ad a temporary name to that column using an **_ALIAS_**.

## SELECT SubTotal, TaxAmt, SubTotal + TaxAmt AS SubTotalWithTaxAmt FROM Purchasing.PurchaseOrderHeader;
The third column was added with **SubTotalWithTaxAmt** temporary name by using an ALIAS (AS).

# Fun with SQL Queries

For this exercise, you will learn to install a SQL Server database using the restore method. Then, you will practice creating SQL statements using the query editor of the SQL Client, and complete a set of exercises covering basic SQL query syntax.

## Setup

### Download and install the Northwind sample database

* Navigate to:  https://northwinddatabase.codeplex.com/
* Download the Northwind database zip file:  Northwind.bak.zip
* Unzip to:  C:\Program Files\Microsoft SQL Server\MSSQL12.SQLEXPRESS\MSSQL\Backup

* Open sql server client
* In the object explorer, right-click on Databases
* Select Restore Database...
* At the Restore Database UI, under Source, select Device and click the browse button
* At the Select backup device UI, select Add and navigate to Northwind.bak
* Click Ok, Ok, and Ok

* You should see a message indicating the restore completed successfully. You should also see the Northwind database listed under 
Databases.
* Select the Northwind database in the object explorer and open the Tables folder to view the 13 tables of the database
* In the toolbar above the object explorer, change the selected default Master database to NORTHWIND
* Click the New Query button in the upper tool bar and save this file locally as sql-exercises.sql.
* Click the New Query button again to open a fresh query session and work your way through the exercises. As you complete each exercise, add and save the required SQL statement to sql-exercises.sql with a comment indicating which exercise it belongs to.
* When you've finished, upload the completed sql script to your GitHub account as 14 - Fun with SQL Queries

### SQL Exercises

Create SQL statements to complete the following:

1.  Return all category names with their descriptions from the Categories table.
2.  Return the contact name, customer id, and company name of all Customers in London
3.  Return all available columns in the Suppliers tables for the marketing managers and sales representatives that have a FAX number 
4.  Return a list of customer id's from the Orders table with required dates between Jan 1, 1997 and Jan 1, 1998 and with freight under 100 units.
5.  Return a list of company names and contact names of all the Owners from the Customer table from Mexico, Sweden and Germany.
6.  Return a count of the number of discontinued products in the Products table.
7.  Return a list of category names and descriptions of all categories beginning with 'Co' from the Categories table.
8.  Return all the company names, city, country and postal code from the Suppliers table with the word 'rue' in their address. The list should ordered alphabetically by company name.
9.  Return the product id and the total quantities ordered for each product id in the Order Details table.
10. Return the customer name and customer address of all customers with orders that shipped using Speedy Express.
11. Return a list of Suppliers containing company name, contact name, contact title and region description.
12. Return all product names from the Products table that are condiments.
13. Return a list of customer names who have no orders in the Orders table.  
14. Add a shipper named 'Amazon' to the Shippers table using SQL.
15. Change the company name from 'Amazon' to 'Amazon Prime Shipping' in the Shippers table using SQL. 
16. Return a complete list of company names from the Shippers table. Include freight totals rounded to the nearest whole number for each shipper from the Orders table for those shippers with orders.
17. Return all employee first and last names from the Employees table by combining the 2 columns aliased as 'DisplayName'. The combined format should be 'LastName, FirstName'.
18. Add yourself to the Customers table with an order for 'Grandma's Boysenberry Spread'.
19. Remove yourself and your order from the database.
20. Return a list of products from the Products table along with the total units in stock for each product. Give the computed column a name using the alias, 'TotalUnits'. Include only products with TotalUnits greater than 100.
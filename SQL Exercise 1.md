# SQL Exercise 1
1. Show the first name and the email address of customer with CompanyName 'Bike World'
2. Show the CompanyName for all customers with an address in City 'Dallas'.
3. How many items with ListPrice more than $1000 have been sold?
4. Give the CompanyName of those customers with orders over $100000. Include the subtotal plus tax plus freight.
5. Find the number of left racing socks ('Racing Socks, L') ordered by CompanyName 'Riding Cycles'.
---
### Answers
1. **USE** AdventureWorksLT2012
   **SELECT** FirstName,EmailAddress,CompanyName
   **FROM** SalesLT.Customer
   **WHERE** SalesLT.Customer.CompanyName='Bike World'
2. **USE** AdventureWorksLT2012
   **SELECT** SalesLT.Customer.CompanyName
   **FROM** SalesLT.CustomerAddress
   **INNER JOIN** SalesLT.Customer **ON**
   SalesLT.CustomerAddress.CustomerID=SalesLT.Customer.CustomerID
   **INNER JOIN** SalesLT.Address **ON**
   SalesLT.CustomerAddress.AddressID=SalesLT.Address.AddressID
   **WHERE** SalesLT.Address.City='Dallas'
3. **SELECT** COUNT(SalesLT.Product.ProductID)
   **FROM** SalesLT.Product
   **WHERE** SalesLT.Product.ListPrice > 1000
4. **USE** AdventureWorksLT2012
   **SELECT** SalesLT.Customer.CompanyName,
   **SUM**(SalesLT.SalesOrderHeader.SubTotal*SalesLT.SalesOrderHeader.TaxAmt*SalesLT.SalesOrderHeader.Freight) **AS** Orders
   **FROM** SalesLT.SalesOrderHeader
   **INNER JOIN** SalesLT.Customer **ON**
   SalesLT.SalesOrderHeader.CustomerID=SalesLT.Customer.CustomerID
   **GROUP BY** SalesLT.Customer.CompanyName
   **HAVING** **SUM**(SalesLT.SalesOrderHeader.SubTotal*SalesLT.SalesOrderHeader.TaxAmt*SalesLT.SalesOrderHeader.Freight) >100000

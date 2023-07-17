# SQL Exercise 2
6. A "Single Item Order" is a customer order where only one item is ordered. Show the SalesOrderID and the UnitPrice for every Single Item Order.
7. Where did the racing socks go? List the product name and the CompanyName for all Customers who ordered ProductModel 'Racing Socks'.
8. Show the product description for culture 'fr' for product with ProductID 736. 
9. Use the SubTotal value in SaleOrderHeader to list orders from the largest to the smallest. For each order show the CompanyName and the SubTotal and the total weight of the order.
10. How many products in ProductCategory 'Cranksets' have been sold to an address in 'London'?
---
### Answers
6.
**USE** AdventureWorksLT2012
**SELECT** SalesLT.SalesOrderDetail.SalesOrderID, SalesLT.SalesOrderDetail.UnitPrice
**FROM** SalesLT.SalesOrderDetail
**WHERE** SalesLT.SalesOrderDetail.OrderQty =1

7.
**USE** AdventureWorksLT2012
**SELECT**
SalesLT.Product.Name,
SalesLT.Customer.CompanyName
**FROM** SalesLT.SalesOrderDetail
**INNER JOIN** SalesLT.Product **ON**
SalesLT.SalesOrderDetail.ProductID=SalesLT.Product.ProductID
**INNER JOIN** SalesLT.SalesOrderHeader **ON**
SalesLT.SalesOrderDetail.SalesOrderID=SalesLT.SalesOrderHeader.SalesOrderID
**INNER JOIN** SalesLT.Customer **ON**
SalesLT.SalesOrderHeader.CustomerID=SalesLT.Customer.CustomerID
**INNER JOIN** SalesLT.ProductModel **ON**
SalesLT.Product.ProductModelID=SalesLT.ProductModel.ProductModelID
**WHERE** SalesLT.ProductModel.Name = 'Racing Socks'

8.
**USE** AdventureWorksLT2012
**SELECT**
SalesLT.ProductDescription.Description
**FROM** SalesLT.ProductDescription 
**INNER JOIN** SalesLT.ProductModelProductDescription **ON**
SalesLT.ProductDescription.ProductDescriptionID=SalesLT.ProductModelProductDescription.ProductDescriptionID
**INNER JOIN** SalesLT.Product **ON**
SalesLT.ProductModelProductDescription.ProductModelID=SalesLT.Product.ProductModelID
**WHERE** SalesLT.Product.ProductID = 736 AND SalesLT.ProductModelProductDescription.Culture = 'fr'

9.
**USE** AdventureWorksLT2012
**SELECT**
SalesLT.Customer.CompanyName,
SalesLT.SalesOrderHeader.SubTotal,
SalesLT.Product.Weight
**FROM** SalesLT.SalesOrderDetail
**INNER JOIN** SalesLT.Product **ON**
SalesLT.SalesOrderDetail.ProductID=SalesLT.Product.ProductID
**INNER JOIN** SalesLT.SalesOrderHeader **ON**
SalesLT.SalesOrderDetail.SalesOrderID=SalesLT.SalesOrderHeader.SalesOrderID
**INNER JOIN** SalesLT.Customer **ON**
SalesLT.SalesOrderHeader.CustomerID=SalesLT.Customer.CustomerID
**ORDER BY** SalesLT.SalesOrderHeader.SubTotal DESC

10.
**USE** AdventureWorksLT2012
**SELECT**
**COUNT**(SalesLT.Product.ProductID) **AS** NUMBER
**FROM** SalesLT.ProductCategory

**INNER JOIN** SalesLT.Product **ON**
SalesLT.ProductCategory.ProductCategoryID=SalesLT.Product.ProductCategoryID

**INNER JOIN** SalesLT.SalesOrderDetail **ON**
SalesLT.Product.ProductID=SalesLT.SalesOrderDetail.ProductID

**INNER JOIN** SalesLT.SalesOrderHeader **ON**
SalesLT.SalesOrderHeader.SalesOrderID=SalesLT.SalesOrderDetail.SalesOrderID

**INNER JOIN** SalesLT.CustomerAddress **ON**
SalesLT.SalesOrderHeader.CustomerID=SalesLT.CustomerAddress.CustomerID

**INNER JOIN** SalesLT.Address **ON**
SalesLT.CustomerAddress.AddressID=SalesLT.Address.AddressID

**WHERE** SalesLT.ProductCategory.Name = 'Cranksets'
**GROUP BY** SalesLT.Address.City
**HAVING** SalesLT.Address.City = 'London'

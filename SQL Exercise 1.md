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

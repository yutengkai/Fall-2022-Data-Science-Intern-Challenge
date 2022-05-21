# Question 1:
The fixed average order value (AOV) should be **302.58**.
Please refer to the 'Fall 2022 Data Science Intern Challenge Q1.ipynb' for detailed answer.

# Question 2:
## a.
**Code**:
select count(OrderID) from Orders  
join Shippers on Orders.ShipperID = Shippers.ShipperID   
where Shippers.ShipperName = 'Speedy Express'
**Result**: 54
## b.
**Code**:
with ECount (EmployeeID, c) as (  
select EmployeeID, count() from Orders   
group by EmployeeID  
order by count() desc limit 1  
),  
TopE as (  
select * from ECount   
join Employees on ECount.EmployeeID=Employees.EmployeeID  
)  
select LastName from TopE  
**Result**: Peacock
## c.
**Code**:
with GermanySupplier (SupplierID, Country) as (  
select SupplierID, Country from Suppliers  
where Country = 'Germany'  
),  
GermanyProduct (ProductID, ProductName, Country) as (  
select ProductID, ProductName, Country from   
Products join GermanySupplier on   
Products.SupplierID = GermanySupplier.SupplierID  
),  
GProductQuantity (ProductID,ProductName, Quantity, Country) as(  
select GermanyProduct.ProductID, ProductName, sum(Quantity), Country from   
GermanyProduct join OrderDetails  
on GermanyProduct.ProductID = OrderDetails.ProductID  
group by GermanyProduct.ProductID  
order by sum(Quantity) desc  
limit 1  
)  
select ProductName from GProductQuantity
**Result**: Gumbär Gummibärchen

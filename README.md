# sql-assignment-2

-- Assignment 2

-- 1. Display the details from Customer table who is from country Germany

Select * from Customer where Country = 'Germany'

-----------------------------------------------
-- Employee Table

CREATE TABLE Employee(
EmployeeId int IDENTITY(1,1) PRIMARY KEY,
FirstName nvarchar(40),
LastName nvarchar(40),
City nvarchar(40),
Country nvarchar(40),
Phone nvarchar(40),);

----------------------------
INSERT INTO dbo.Employee(FirstName,LastName,City,Country,Phone)
VALUES ('Max','Smith','New York','USA','148523697'),
('Amit','Sexana','Bangalore','INDIA','741258963'),
('Shobhit','Dubey','Mumbai','India','741258931'),
('Sita','Gupta','Canada','UK','3698521470'),
('Chanchal','Singh','London','UK','789541230');

-------------------------------------
-- 2. Display the full name of the employee  

SELECT * FROM Employee
-------------------------------------------------

-- Display the customer details who has Fax number
ALTER TABLE Customer 
ADD FaxNumber nvarchar(12);

SELECT * from Customer Where FaxNumber is not Null;

---------------------------------

-- display the customer details whose name holds second letter as U

Select * from Customer Where FirstName Like '_u%';

---------------------------------------
-- select order Details where unit price is greater than 10 and less than 20

Select * From OrderItem Where UnitPrice >10 and UnitPrice <20;

--- Alternative

Select * From OrderItem Where UnitPrice between 10 and 20;

--------------------------------------------
--Display order details which contains shipping date and arrange the order by date

SELECT OrderDate AS SHIPPING_DATE 
FROM OrderTable
ORDER BY OrderDate ASC

---------------------------------------------------

--Print the orders shipped by ship name 'La corned'abondance' between 2 dates(Choose dates of your choice)

SELECT ShipName
FROM OrderTable
where ShipName =''La corned abondance' AND'OrderDate BETWEEN '2022-04-02' AND '2022-04-05' 
ORDER BY OrderDate ASC

---------------------------------------------------
--Print the products supplied by 'Exotic Liquids'

SELECT * FROM ProductTable
WHERE Package ='EXOTIC LIQUIDS'

-------------------------------------------
-- print the average quantity ordered for every product

select avg(quantity) From OrderItem INNER JOIN Product ON OrderItem.ProductId = Product.id;

-----------------------------------------

--Print all the Shipping company name and the ship names if they are operational

SELECT ShipCompany, ShipName
From ShippingTable
Where Operational = 'yes'

-------------------------------------------

--Print all Employees with Manager Name

SELECT E.NAME AS EMPLOYEE_NAME,M.NAME AS MANAGER_NAME
FROM Employee E JOIN Employee M
ON E.MANAGER=M.MANAGER

-----------------------------------------

--Print the bill for a given order id .bill should contain Productname, Categoryname,price after discount

SELECT OI.OrderId,P.ProductName,P.Category,P.Discount
FROM ProductTable P INNER JOIN OrderItemTable OI
ON P.ProductId=OI.ProductId

-----------------------------------

--Print the Total price of orders which have the products supplied by 'Exotic Liquids' if the price is > 50 and also print it by Shipping company's Name

SELECT SUM(UnitPrice) As Total,CompanyName 
FROM ProductTable 
GROUP BY ProductSupplied
having ProductSupplied ='exotic liquids' and UnitPrice >50;

-- Salesman Table :

create table Salesman_table
(
    Salesmanid int primary key,
    SalesmanName varchar(20),
    Commission int,
    City varchar(20) default 'Unknown',   -- default constraint added
    Age int
)

-- Insert Salesman Records :

insert into Salesman_table
(Salesmanid, SalesmanName, Commission, City, Age)
values
(101,'Joe',50,'california',17),
(102,'Simon',75,'Texas',25),
(103,'Jessie',105,'florida',35),
(104,'Danny',100,'Texas',22),
(105,'Lia',65,'New Jersy',30),
(106,'Jose',58,'Mexico',34),
(107,'Selcia',75,'Texas',23),
(108,'Jannu',101,'netherland',35)

select * from Salesman_table


-- Customer Table :

create table Customer_table
(
    Salesmanid int foreign key references Salesman_table(Salesmanid),
    Customerid int,
    CustomerName varchar(20) not null,   -- not null constraint added
    PurchaseAmount int
)

-- Insert Customer Records

insert into Customer_table
(Salesmanid, Customerid, CustomerName, PurchaseAmount)
values
(101,2345,'Andrew',550),
(102,1575,'Lucky',4500),
(103,2346,'Brian',4000),
(104,3747,'Remon',2700),
(105,1234,'Julia',4545)

select * from Customer_table


-- Orders Table
create table order_table
(
    orderid int,
    Customerid int,
    Salesmanid int,
    orderdate date,
    Amount int
);

-- Insert Orders
insert into order_table
(orderid, Customerid, Salesmanid, orderdate, Amount)
values
(5001,2345,101,'2021-04-07',550),
(5002,1575,102,'2020-04-12',4500),
(5003,1234,105,'2022-05-02',4545),
(5004,2346,103,'2023-05-10',1580),
(5005,3747,104,'2020-08-10',1400);

select * from order_table;

-- TASKS


1) Insert a new record in Orders
insert into order_table
(orderid, Customerid, Salesmanid, orderdate, Amount)
values(5006,4560,108,'2025-12-19',1590);

2) Fetch Customers ending with 'N' and PurchaseAmount > 500
select * from Customer_table
where CustomerName like '%N' and PurchaseAmount > 500;

 3) Using SET Operators
-- Unique SalesmanIds
select Salesmanid from Salesman_table
except
select Salesmanid from Customer_table;

-- Common SalesmanIds
select Salesmanid from Salesman_table
intersect
select Salesmanid from Customer_table;

4) Display Orderdate, Salesman Name, Customer Name, Commission, City (500–1500)
select 
    ort.orderdate,
    smt.SalesmanName,
    cst.CustomerName,
    smt.Commission,
    smt.City
from order_table ort
inner join Salesman_table smt on ort.Salesmanid = smt.Salesmanid
inner join Customer_table cst on ort.Customerid = cst.Customerid
where cst.PurchaseAmount between 500 and 1500;

 5) Right Join Salesman and Orders
select *
from Salesman_table smt
right join order_table ort
on smt.Salesmanid = ort.Salesmanid;

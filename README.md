# SQL-Queries

create table Department
(Id int primary key,
Name varchar(50),
)
insert into Department values
(1,'IT'),
(2,'HR'),
(3,'Admin')

create table Employee
(
Id int,
Name varchar(50),
Did int
)
insert into Employee values
(1,'Ashish',1),
(2,'Ritesh',2),
(3,'Jyoti',2),
(4,'Archana',null),
(5,'Dheeraj',null),
(6,'Satish',2)


select * from Department
select * from Employee

-- Select all employees whose name starts with ‘A’ [use all possible ways].
select * from Employee where name like('A%')

-- Select all employees whose name ends with ‘h’ [use all possible ways].
select * from Employee where name like('%h')

-- Find department name that does not have any employee.
select Employee.name as Empname,Department.name as Deptname
from Employee right join Department 
on Employee.Did=Department.id
where Did is null 

-- Find all employees who do not belong to any department.
select Employee.name as Empname,Department.name as Deptname
from Employee left join Department 
on Employee.Did=Department.id
where did is null

-- Compute employee count by its department name.
select Department.name as departname,count(Employee.id) as Empname
from Department join Employee
on Department.id=Employee.did
group by Department.name

-- Retrieve Department Id & Name who has more than 2 employees.
select d.id,d.name from Department d join Employee e on e.did=d.id
group by d.id ,d.name
having count(e.id)>=2

-- Find Department ID and Name who has at least one employee.
select d.id,d.name from Department d join Employee e on e.did=d.id
group by d.id ,d.name
having count(e.id)>=1

-- Write a query for below output use function wherever required.
/*Id	Name	Did	Dname
 1	   Ashish	1	IT
 2	   Ritesh	2   HR
 3	   Jyoti    2   HR
 4	   Archana  0   No Department
 5	   Dheeraj  0   No Department
 6	   Satish   2   HR   */

select employee.id,employee.name as employeename,coalesce(department.id,0) as did, 
coalesce(department.name,'no department')as departmentname
from
employee left join department
on
employee.did=department.id 

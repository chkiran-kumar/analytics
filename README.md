# Kiran Kumar Cherupalli - Data Analyst

SQL Queries For Data Analyst

#1) Manager name and list of Employees in a row
----------------------------------------
SELECT DISTINCT e2.name AS ManagerName, EmployeeName = STUFF(
(Select ','+ Name from Employee X WHERE X.ManagerID = e2.EmployeeID for XML PATH ('')),1,1, '')
FROM Employee e1
INNER JOIN Employee e2
ON e1.ManagerID = e2.EmployeeID

#2) Find Latest Salary of an Employee
----------------------------------------------
SELECT * FROM (
SELECT Ename, sal, Saldate, ROW_NUMBER() over (PARTITION BY Ename ORDER BY Saldate DESC) AS RowN FROM emp
)c 
WHERE c.RowN>1

#3) Remove Duplicate rows in a Table
----------------------------------------------
SELECT * FROM (
SELECT Ename, DOB, City, ROW_NUMBER() over (PARTITION BY Ename, DOB, CITY ORDER BY Ename DESC) AS RowN FROM emp
)c 
WHERE c.RowN>1

#4) Frequently used formulas in Queries to replae NULL values
-------------------------------------------------------------
ISNULL: If the value is NULL then prints alternate value

COALESCE: Retrieves first Non Null columns value

SELECT FirstName, LastName, MiddleName, COALESCE(FirstName, LastName, MiddleName,'NO record') as [Name] from PersonalDetails
SELECT FirstName, LastName, MiddleName, ISNULL(FirstName,'Update record') as [Name] from PersonalDetails 

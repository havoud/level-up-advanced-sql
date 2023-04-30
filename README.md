# Level Up: Advanced SQL
This is the repository for the LinkedIn Learning course Level Up: Advanced SQL. The full course is available from [LinkedIn Learning][lil-course-url] and the instructor is Jess Pomfret.

 I have tried this course to assess my SQL knowledge in sophisticated SQLite queries, including complex join types, grouping, advanced select options, windowing functions, and more.

This course is integrated with GitHub Codespaces and includes different challenages from easy to hard SQL coding.

### Challenges

#### 1) Gabriella needs to gather some employee information. She wants us to retrieve a list of employees, including their first and last names, and the first and last names of their immediate managers.

*SQL* *Answer*:
```
SELECT emp.firstName,
    emp.lastName,
    emp.title,
    mng.firstName AS ManagerFirstName,
    mng.lastName AS ManagerLastName
FROM employee emp
INNER JOIN employee mng
    ON emp.managerId = mng.employeeId
```

#### 2) Get a list of salespeople with zero sales.

*SQL* *Answer*:

```
SELECT emp.firstName, emp.lastName, emp.title, emp.startDate, sls.salesId
FROM employee emp
LEFT JOIN sales sls
    ON emp.employeeId = sls.employeeId
WHERE emp.title = 'Sales Person'
AND sls.salesId IS NULL;
```

#### 3) Analyze all our sales and the customer data relating to those sales. Get a list of all sales and all customers even if some of the data has been removed.

*SQL* *Answer*:

```
SELECT cus.firstName, cus.lastName, cus.email, sls.salesAmount, sls.soldDate
FROM customer cus
INNER JOIN sales sls
    ON cus.customerId = sls.customerId
UNION
-- UNION WITH CUSTOMERS WHO HAVE NO SALES
SELECT cus.firstName, cus.lastName, cus.email, sls.salesAmount, sls.soldDate
FROM customer cus
LEFT JOIN sales sls
    ON cus.customerId = sls.customerId
WHERE sls.salesId IS NULL
UNION
-- UNION WITH SALES MISSING CUSTOMER DATA
SELECT cus.firstName, cus.lastName, cus.email, sls.salesAmount, sls.soldDate
FROM sales sls
LEFT JOIN customer cus
    ON cus.customerId = sls.customerId
WHERE cus.customerId IS NULL;
```

#### 4) How many cars have been sold per employee?

*SQL* *Answer*:

```
SELECT emp.employeeId, emp.firstName, emp.lastName, count(*) as NumOfCarsSold
FROM sales sls
INNER JOIN employee emp
    ON sls.employeeId = emp.employeeId
GROUP BY emp.employeeId, emp.firstName, emp.lastName
ORDER BY NumOfCarsSold DESC;
```

#### 5) Find the least and most expensive car sold by each employee.

*SQL* *Answer*:

```
SELECT emp.employeeId, 
    emp.firstName, 
    emp.lastName, 
    MIN(salesAmount) AS MinSalesAmount, 
    MAX(salesAmount) as MaxSalesAmount
FROM sales sls
INNER JOIN employee emp
    ON sls.employeeId = emp.employeeId
WHERE sls.soldDate >= date('now','start of year')
GROUP BY emp.employeeId, emp.firstName, emp.lastName
```



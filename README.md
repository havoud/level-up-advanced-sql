# Level Up: Advanced SQL
This is the repository for the LinkedIn Learning course Level Up: Advanced SQL. The full course is available from [LinkedIn Learning][lil-course-url] and the instructor is Jess Pomfret.

 I have tried this course to assess my SQL knowledge in sophisticated SQLite queries, including complex join types, grouping, advanced select options, windowing functions, and more.

This course is integrated with GitHub Codespaces and includes different challenages from easy to hard SQL coding.

### Challenges

#### 1) Gabriella needs to gather some employee information. She wants us to retrieve a list of employees, including their first and last names, and the first and last names of their immediate managers.

*SQL* *Answer*
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


                          

# Database management SQL query Interview questions

### CREATE database

```bash
CREATE DATABASE subquerydb;
USE subquerydb;
```

### CREATE tabels

```bash

CREATE TABLE employee(
id INT PRIMARY KEY,
fname VARCHAR(25),
lname VARCHAR(25),
Age INT,
emailID VARCHAR(225),
phoneNo INT,
city VARCHAR(25)
);

CREATE TABLE client(
id INT PRIMARY KEY,
first_name VARCHAR(25),
last_name VARCHAR(25),
age INT,
emailID VARCHAR(25),
phoneNo INT,
city VARCHAR(25),
empID INT,
FOREIGN KEY(empID) REFERENCES employee(id)
);

CREATE TABLE project(
id INT PRIMARY KEY,
empID INT,
name VARCHAR(25),
startdate DATE,
clientID INT,
FOREIGN KEY(empID) REFERENCES employee(id),
FOREIGN KEY(clientID) REFERENCES client(id)
);

SHOW TABLES;

```

### Insert values

```bash

INSERT INTO employee VALUES
(1, 'AMan', 'Proto', 32, 'aman@gmail.com', 018, 'Delhi'),
(2, 'Yagya', 'Narayan', 44, 'yagya@gmail.com', 018, 'Palalm'),
(3, 'Rahul', 'BD', 22, 'rahul@gmail.com', 018, 'Kolkata'),
(4, 'Jatin', 'Hermit', 31, 'jatin@gmail.com', 018, 'Raipur'),
(5, 'PK', 'Pandey', 21, 'pk@gmail.com', 018, 'Jaipur');

SELECT * FROM employee;

INSERT INTO client VALUES
(1, 'Mac', 'Rogers', 47, 'mac@gmail.com', 333, 'Kolkata', 3),
(2, 'Max', 'Poirier', 27, 'max@gmail.com', 222, 'Kolkata', 3),
(3, 'Peter', 'Jain', 24, 'peter@gmail.com', 11, 'Delhi', 1),
(4, 'Sushant', 'Aggarwai', 23, 'sushant@gmail.com', 4545, 'Hyderabad', 5),
(5, 'Pratap', 'Singh', 36, 'pratap@gmail.com', 7765, 'Mumbai', 2);

SELECT * FROM client;

INSERT INTO project VALUES 
(1, 1, 'A', '2021-04-21', 3),
(2, 2, 'B', '2021-04-22', 1),
(3, 3, 'C', '2021-04-23', 5),
(4, 3, 'D', '2021-04-24', 2),
(5, 5, 'E', '2021-04-25', 4);

SELECT * FROM project;

```

1. employees with age > 30

```bash
SELECT * FROM employee WHERE age in (SELECT age FROM employee WHERE age>30);

```

2. Find the youngest employee.

```bash
SELECT * FROM employee WHERE age = 
(SELECT MIN(age) FROM employee);
```

3. emp details working in more than 1 project.

```bash
SELECT * FROM employee WHERE id in 
(SELECT empID FROM project group by empID having count(empID) > 1);

```

4. emp details having age > avg(age)

```bash
SELECT * FROM employee WHERE age > (SELECT avg(age) FROM employee);
```

5. select max age person whose first name contains 'a'


```bash
SELECT max(age) FROM (SELECT * FROM employee WHERE fname like '%a%') as temp;

```

6. find 3rd oldest employee


```bash
SELECT * FROM employee as e1
WHERE 2 = (
SELECT COUNT(e2.age)
FROM employee as e2
WHERE e2.age >= e1.age
);
```

7. Find employees who have more than one client.


```bash
SELECT 
    e.id,
    e.fname,
    COUNT(c.id) AS total_clients
FROM employee e
JOIN client c
    ON e.id = c.empID
GROUP BY e.id, e.fname
HAVING COUNT(c.id) > 1;
```

8. Display employee name, client name and client city

```bash
SELECT
    e.fname AS employee_name,
    c.first_name AS client_name,
    c.city AS client_city
FROM employee e
JOIN client c
    ON e.id = c.empID;
```

9. Find the number of projects handled by each employee.

```bash
SELECT e.fname, count(p.id) as number_of_proj
FROM employee as e
LEFT JOIN project as p
ON p.empID = e.id
GROUP BY e.id;
```

10. Find employees who have at least one client.

```bash
SELECT * FROM employee WHERE id IN
(SELECT empID FROM client);
```
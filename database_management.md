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


```bash

```
## Librariy-Management-System.-SQL-P-03
**Project Name - Library Management System**

**Dificulty Level - Intermediate**

**Database-** `library_db`

<img width="1600" height="1067" alt="image" src="https://github.com/user-attachments/assets/5cc086fc-4ea0-431f-a9a6-5fde2ef76e8d" />

## Objective
**1.To showcase the usecase of SQL database management system to manage a library with efficiency.**

**2. To build rational relationship between tables**

**3. Do the advanced SQL queeries to manage the library System**

## Database
Create a datababse for library management system. Tables are-

1.books

2.members

3.issue_status

4.employees

5.branch

6.return_status

**Database Structure**

<img width="1525" height="891" alt="Screenshot 2025-10-21 183641" src="https://github.com/user-attachments/assets/e81e8f05-ae61-4add-b4d4-93df829c8af6" />



**Create Tables-**
```sql
CREATE DATABASE Libery_DB;

\c library_db;
\dt

CREATE TABLE books (
                  isbn varchar(20),
				  book_title varchar(75),
				  category varchar(10),
				  rental_price FLOAT,
				  status  varchar(15),
				  author VARCHAR(35),
				  publisher VARCHAR(55)
				  );


Create table employees(
                       emp_id varchar(10) PRIMARY KEY, 
                       emp_name VARCHAR(25),
					   position VARCHAR(
					   salary INT,
					   brench_id VARCHAR(25)
					   );

CREATE TABLE branch  (
                        branch_id VARCHAR (10) PRIMARY KEY,
						 manager_id VARCHAR(10),
						 branch_adress VARCHAR(55),
						 contact_no VARCHAR(10)
						 );

CREATE TABLE members (
                     member_id VARCHAR(10) Primary key,
					 member_name VARCHAR(25),
					 member_address VARCHAR(75), 
					 reg_date DATE
					 );
CREATE TABLE issue_status (
issued_id VARCHAR (10) PRIMARY KEY,
issued_member_id VARCHAR (10),
issued_book_name varchar(75) , 
issued_date DATE,
issued_book_isbn varchar(25),
issued_emp_id varchar (10)

);


SELECT * FROM books;
SELECT * FROM employees;
SELECT * FROM branch;
SELECT * FROM issue_status;
SELECT * FROM members;
SELECT * FROM return_status;
```
**Task-01: Create a New Book Record -- '978-1-60129-456-2', 'To kill a mocking bird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.'**
```sql
Insert INTO books(isbn,book_title,category,rental_price,status,author,publisher)
VALUES
('978-1-60129-456-2', 'To kill a mocking bird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.'
);
```

**Task-02: Update an existing member's address**
```sql
UPDATE members
SET member_address = '125 Main St'
WHERE member_id = 'C101';
```

**Task-03: Delete a table from issued_status table -- Objective: Delete the record with the issued_id ='IS107' from the issue_status table**
```sql
SELECT * FROM issue_status
where issued_id = 'IS122';

DELETE FROM issue_status
where issued_id = 'IS122';
```

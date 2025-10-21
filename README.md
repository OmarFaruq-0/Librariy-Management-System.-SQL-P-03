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

**Task-04: Retrive all books issued by a specific employee -- Objective: Select all books issued by emp_id ='E101'**
```sql
SELECT * FROM issue_status
where issued_emp_id = 'E101'
```

**Task-05: Count the all books by the issued_emp_id**
```sql
SELECT COUNT(issued_id) as Total_books, issued_emp_id FROM issue_status
GROUP BY issued_emp_id;
```

**CATS**			
**Task-06: Create Summary Table: Use CATS to generate new tables based on querry result - each book and total_issued_cnt**
```sql
CREATE TABLE book_count AS
SELECT B.isbn,B.book_title, COUNT(i_s.issued_book_isbn) FROM books as  B 
join issue_status as  i_s
ON B.isbn = i_s.issued_book_isbn GROUP BY B.isbn, B.book_title;
SELECT * FROM book_count;
```

**Task-07: Retrive all books based on category**
```sql
SELECT Count(book_title) as Total book, Category  FROM books
GROUP BY category;
```

**Task-08: Find the total rental price based on category **		
```sql
SELECT category, sum(rental_price), COUNT(*) FROM books as  B 
join issue_status as  i_s
ON B.isbn = i_s.issued_book_isbn GROUP BY category;
```

**Task-09: List members who registered in last 180 days**
```sql
select * from members
where reg_date >= CURRENT_DATE - INTERVAL '180 days';

select * from members
insert into members (member_id, member_name,member_address, reg_date)
Values
('C120', 'Sam John', '454 ABC ST', '2025-07-15'),

('C121', 'Willamson Wiki', '564 Bradshaw ST', '2025-08-15');
```

**Task- 10: List Employees with thier branch Manager's name and thier branch details**
```sql
SELECT * FROM branch;
SELECT * FROM employees;
select E.*,
 E2.emp_name as Manager
from employees E
JOIN branch B
on E.brench_id = B.brench_id
JOIN employees E2
ON B.manager_id = E2.emp_id;
```

**Task-11: Create a table of books wiht rental price above a certain Thresold $7**
```sql
Create table books_price_greater_than_7
SELECT * FROM books
where rental_price > 7

SELECT * FROM books_price_greater_than_7;
```

**Task-12: Retrive all books which are not returned**
```sql
--Task-12: Retrive all books which are not returned.
SELECT DISTINCT I.issued_book_name
FROM issue_status I
LEFT JOIN return_status R
ON I.issued_id=R.issued_id
WHERE R.return_id is NULL;
```
## Advanced Query 
**Task 13: Identify Members with Overdue Books
/*Write a query to identify members who have overdue books (assume a 30-day return period). 
Display the member's_id, member's name, book title, issue date, and days overdue.
*/**




































































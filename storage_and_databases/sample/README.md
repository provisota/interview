# Sample for RDBS

```sql
CREATE TABLE Authors
(
    id      SERIAL PRIMARY KEY,
    name    VARCHAR(255) NOT NULL,
    country VARCHAR(100)
);
CREATE TABLE Books
(
    id               SERIAL PRIMARY KEY,
    title            VARCHAR(255) NOT NULL,
    publication_year INTEGER,
    author_id        INTEGER REFERENCES Authors (id),
    price            DECIMAL(10, 2)
);
CREATE TABLE Customers
(
    id    SERIAL PRIMARY KEY,
    name  VARCHAR(255) NOT NULL,
    email VARCHAR(255)
);
CREATE TABLE Orders
(
    id          SERIAL PRIMARY KEY,
    book_id     INTEGER REFERENCES Books (id),
    customer_id INTEGER REFERENCES Customers (id),
    order_date  DATE,
    quantity    INTEGER
);
```

Sample Data

```sql
INSERT INTO Authors (id, name, country)
VALUES (1, 'J.K. Rowling', 'United Kingdom'),
       (2, 'George Orwell', 'United Kingdom'),
       (3, 'Leo Tolstoy', 'Russia'),
       (4, 'Agatha Christie', 'United Kingdom'),
       (5, 'Mark Twain', 'United States'),
       (6, 'Dan Brown', 'United States'),
       (7, 'J.R.R. Tolkien', 'United Kingdom'),
       (8, 'Stephen King', 'United States'),
       (9, 'Virginia Woolf', 'United Kingdom'),
       (10, 'Haruki Murakami', 'Japan');

INSERT INTO Books (id, title, publication_year, author_id, price)
VALUES (1, 'Harry Potter and the Philosopher''s Stone', 1997, 1, 20.00),
       (2, '1984', 1949, 2, 15.00),
       (3, 'War and Peace', 1869, 3, 25.00),
       (4, 'Murder on the Orient Express', 1934, 4, 18.00),
       (5, 'The Adventures of Tom Sawyer', 1876, 5, 12.00),
       (6, 'Harry Potter and the Chamber of Secrets', 1998, 1, 22.00),
       (7, 'Animal Farm', 1945, 2, 17.00),
       (8, 'Death on the Nile', 1937, 4, 19.00),
       (9, 'The Da Vinci Code', 2003, 6, 18.00),
       (10, 'The Hobbit', 1937, 7, 20.00),
       (11, 'The Shining', 1977, 8, 15.00),
       (12, 'Mrs Dalloway', 1925, 9, 14.00),
       (13, 'Kafka on the Shore', 2002, 10, 21.00),
       (14, 'Inferno', 2013, 6, 16.00),
       (15, 'The Lord of the Rings', 1954, 7, 22.00),
       (16, 'It', 1986, 8, 20.00),
       (17, 'Harry Potter and the Prisoner of Azkaban', 1999, 1, 23.00),
       (18, 'Harry Potter and the Goblet of Fire', 2000, 1, 24.00),
       (19, 'Harry Potter and the Order of the Phoenix', 2003, 1, 25.00),
       (20, 'Homage to Catalonia', 1938, 2, 16.00),
       (21, 'The Road to Wigan Pier', 1937, 2, 17.00);

INSERT INTO Customers (id, name, email)
VALUES (1, 'John Doe', 'john.doe@example.com'),
       (2, 'Jane Smith', 'jane.smith@example.com'),
       (3, 'Emily Johnson', 'emily.johnson@example.com'),
       (4, 'Michael Brown', 'michael.brown@example.com'),
       (5, 'Alice Johnson', 'alice.johnson@example.com'),
       (6, 'David Lee', 'david.lee@example.com'),
       (7, 'Maria Garcia', 'maria.garcia@example.com'),
       (8, 'James Wilson', 'james.wilson@example.com'),
       (9, 'Sophia Martinez', 'sophia.martinez@example.com'),
       (10, 'Liam Nguyen', 'liam.nguyen@example.com'),
       (11, 'Olivia Patel', 'olivia.patel@example.com'),
       (12, 'Noah Kim', 'noah.kim@example.com'),
       (13, 'Emma Rodriguez', 'emma.rodriguez@example.com'),
       (14, 'Ava Huang', 'ava.huang@example.com'),
       (15, 'William Garcia', 'william.garcia@example.com'),
       (16, 'Charlotte Lee', 'charlotte.lee@example.com'),
       (17, 'Benjamin Singh', 'benjamin.singh@example.com'),
       (18, 'Mia Anderson', 'mia.anderson@example.com'),
       (19, 'Lucas Chen', 'lucas.chen@example.com'),
       (20, 'Amelia Smith', 'amelia.smith@example.com');

INSERT INTO Orders (id, book_id, customer_id, order_date, quantity)
VALUES (1, 1, 1, '2021-01-15', 2),
       (2, 5, 2, '2021-02-20', 1),
       (3, 3, 1, '2021-03-05', 1),
       (4, 2, 3, '2021-03-15', 1),
       (5, 4, 1, '2021-04-10', 1),
       (6, 6, 2, '2021-04-22', 3),
       (7, 9, 4, '2022-05-10', 1),
       (8, 10, 5, '2022-05-15', 2),
       (9, 12, 6, '2022-06-01', 1),
       (10, 13, 7, '2022-06-20', 1),
       (11, 14, 4, '2022-07-05', 1),
       (12, 15, 5, '2022-07-15', 1),
       (13, 11, 6, '2022-08-05', 2),
       (14, 16, 7, '2022-08-20', 1),
       (15, 2, 8, '2023-09-01', 1),
       (16, 5, 8, '2023-09-10', 2),
       (17, 1, 2, '2023-09-15', 1),
       (18, 6, 3, '2023-10-05', 2),
       (19, 7, 4, '2023-10-20', 1),
       (20, 8, 5, '2023-11-01', 3);
```

* **List all books published after 2010.**
```sql
SELECT id, title, publication_year, author_id, price 
FROM books 
WHERE publication_year > 2010;
```
* **Find the total number of books sold for each author.**
```sql
SELECT a.name, COUNT(b.id) AS books 
FROM books b JOIN authors a ON b.author_id = a.id 
GROUP BY a.id;
```
* **Retrieve the details of the most expensive book.**
```sql
EXPLAIN ANALYZE
SELECT a.name, b.title, b.price 
FROM books b JOIN "public".authors a on b.author_id = a.id
ORDER BY b.price LIMIT 1;
```
```sql
EXPLAIN ANALYZE
SELECT a.name, b.title, b.price
FROM books b
         JOIN "public".authors a on b.author_id = a.id
WHERE b.price = (SELECT MAX(price) FROM Books);
```
* **List customers who have not made any orders.**
```sql
SELECT c.id, c.name, c.email 
FROM customers c LEFT JOIN orders o ON c.id = o.customer_id 
WHERE o.id IS NULL; 
```
* **Find all authors who have more than 3 books published.**
```sql
SELECT a.name, COUNT(b.id) AS books 
FROM books b JOIN authors a ON b.author_id = a.id 
GROUP BY a.id HAVING COUNT(b.id) > 3;
```
* **Get the average price of books published before 2000.**

```sql
SELECT AVG(price)
FROM books
WHERE publication_year < 2000;
```
* **List the names of books along with their author's names.**
```sql
SELECT a.name AS author_name, b.title AS book
FROM authors a
         JOIN books b ON a.id = b.author_id
ORDER BY a.name;
```
* **Count the number of orders made each year.**
```sql
SELECT EXTRACT(YEAR FROM order_date) AS year, COUNT(id) AS count 
FROM orders
GROUP BY year;
``` 
* **Show the total sales (quantity of books sold) for each book title.**
* **List all books along with their authors' names, sorted by publication year in descending order.**
* **Find the average price of books for each author, including only authors who have published more than 2 books.**
* **Retrieve the top 3 most expensive books and their authors' names.**
* **List customers and the total amount they have spent on orders, sorted by the total amount in descending order.**
* **Show the number of books each author has published after 1950.**
* **Find all books that have never been ordered.**
* **List the most recent order for each customer, including customer name, book title, and order date.**
* **Display the total number of books sold per year, along with the year.**
* **Identify customers who have ordered the same book multiple times.**
* **Show all authors, along with the total revenue generated from their books.**
* **Find the name and email of customers who have ordered more than 3 books in total.**
* **List books along with their author names, but only for books published in the last 20 years, sorted by price.**
* **Determine the most popular book, based on the number of times it has been ordered.**
* **Retrieve a list of books that have not been ordered since 2020.**
* **Find the oldest book that has been ordered in 2023.**
* **Calculate the average number of books ordered per customer.**
* **Identify authors whose books have never been ordered.**
* **Display the total sales (quantity of books sold) for each genre (assuming a genre column exists in the books
    table).**
* **Find the month with the highest number of orders, including the total number of orders in that month.**
* **Show a list of authors and the number of different countries their books have been ordered in.**

These queries cover a range of SQL concepts, including joins, aggregations, sorting, and subqueries, making them useful
for demonstrating SQL skills in an interview context.
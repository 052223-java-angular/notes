# SQL and PostgreSQL with Docker Tutorial

SQL is a language used for interacting with databases. PostgreSQL is a specific implementation of SQL that provides additional features. Docker is a platform that makes it easier to create, deploy, and run applications by using containers.

## SQL Basics

SQL stands for Structured Query Language. It's a language designed to interact with databases, allowing you to create, read, update, and delete database records.

## SQL Statements

Here are some basic SQL statements:

- `SELECT`: used to select data from a database
- `UPDATE`: used to update data in a database
- `DELETE`: used to delete data from a database
- `INSERT INTO`: used to insert new data into a database
- `CREATE DATABASE`: used to create a new database
- `ALTER DATABASE`: used to modify an existing database
- `CREATE TABLE`: used to create a new table
- `ALTER TABLE`: used to modify an existing table
- `DROP TABLE`: used to delete a table

## PostgreSQL

PostgreSQL is an open-source relational database management system (RDBMS) that implements the SQL standard and offers many advanced features.

## Docker

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run.

## Running a PostgreSQL instance with Docker

You can run a PostgreSQL instance using Docker by executing the following command in your terminal:

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

This command will start a new Docker container named some-postgres, with the environment variable POSTGRES_PASSWORD set to mysecretpassword. The -d flag tells Docker to run the container in the background.
Connecting to a PostgreSQL Database in Docker

You can connect to a PostgreSQL database in Docker using the psql command:

```bash
docker exec -it some-postgres psql -U postgres
```

This command uses the docker exec command to run psql -U postgres inside the some-postgres container. The -it flag tells Docker to allocate a pseudo-TTY connected to the container’s stdin, allowing you to interact with the psql shell.
Basic PostgreSQL Commands

- `CREATE` DATABASE: Creates a new database.

```sql
CREATE DATABASE test_db;
```

<br>

- `CREATE TABLE`: Creates a new table.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(40),
    last_name VARCHAR(40),
    birth_day DATE,
    sex VARCHAR(1),
    salary INT,
    super_id INT,
    branch_id INT
);
```

<br>

- `SELECT`: Retrieves data from a database.

```sql
SELECT * FROM employees; -- Retrieves all records from the employees table
SELECT first_name, last_name FROM employees; -- Retrieves only the first_name and last_name fields from the employees table
```

<br>

- `INSERT INTO`: Adds new data into a database.

```sql
INSERT INTO employees (employee_id, first_name, last_name, birth_day, sex, salary, super_id, branch_id)
VALUES (1, 'John', 'Doe', '1980-01-01', 'M', 50000, null, 100);
```

<br>

- `UPDATE`: Modifies existing data in a database.

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;
```

<br>

- `DELETE`: Removes data from a database.

```sql
DELETE FROM employees
WHERE employee_id = 1;
```

## Advanced Features

PostgreSQL includes several advanced features, such as:

- Complex queries
- Foreign keys
- Views
- Transactional integrity
- Multiversion concurrency control

## Understanding Database Keys and Normal Forms

Designing a database is a critical process that ensures the efficiency, accuracy, and performance of your applications. A poorly designed database can result in data redundancy and can make the data hard to manage, which can further lead to inconsistent data.

### Primary Keys

A primary key is a column or group of columns used to uniquely identify a row in a table. No two rows can have the same primary key value. This allows you to retrieve and manipulate each row independently and accurately.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(40),
    last_name VARCHAR(40),
    email VARCHAR(40)
);
```

In this example, `customer_id` is the primary key of the `customers` table.

### Foreign Keys

A foreign key is a column or group of columns in a table that is used to establish a link between the data in two tables. It is a field in a table, that is a primary key in another table. This relationship allows you to perform operations that involve multiple tables more effectively.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    product_name VARCHAR(40),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers (customer_id)
);
```

In this example, `customer_id` in the `orders` table is a foreign key that references `customer_id` in the `customers` table.

### Composite Keys

A composite key is a combination of two or more columns in a table that can be used to uniquely identify each row in the table. Composite keys are useful when a single column is not sufficient to uniquely identify a row.

```sql
CREATE TABLE order_details (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

In this order_details table, neither order_id nor product_id alone are sufficient to uniquely identify a record. The combination of order_id and product_id is unique for each row, forming a composite key.

## Normalization

Normalization is a database design technique that reduces data redundancy and eliminates undesirable characteristics like insertion, update, and deletion anomalies. Normalization rules, including First Normal Form (1NF), Second Normal Form (2NF), and Third Normal Form (3NF), help you structure your data in a way that is both efficient and easy to work with.

### First Normal Form (1NF)

Each table cell should contain a single value, and each record needs to be unique. This eliminates duplicative columns from the same table and creates separate tables for each group of related data.

For example, consider a table `orders`:

| order_id | product_ids |
|----------|-------------|
| 1        | 1,2,3       |
| 2        | 1,2         |
| 3        | 3,4         |

This table is not in 1NF because the `product_ids` column contains multiple values.

After converting it into 1NF, it will look like this:

| order_id | product_id |
|----------|------------|
| 1        | 1          |
| 1        | 2          |
| 1        | 3          |
| 2        | 1          |
| 2        | 2          |
| 3        | 3          |
| 3        | 4          |

### Second Normal Form (2NF)

It follows all the rules of 1NF, and there should be no partial dependencies of any column on the primary key. In other words, non-key columns should depend on all parts of the composite primary key.

For example, consider a table `order_details`:

| order_id | product_id | product_price |
|----------|------------|---------------|
| 1        | 1          | 100           |
| 1        | 2          | 200           |
| 2        | 1          | 100           |
| 2        | 2          | 200           |

Here `order_id` and `product_id` together form a primary key. The `product_price` is dependent on `product_id`, not on the entire primary key. So this table is not in 2NF.

To bring it into 2NF, we can split it into two tables: `orders` and `products`:

`orders`:
| order_id | product_id |
|----------|------------|
| 1        | 1          |
| 1        | 2          |
| 2        | 1          |
| 2        | 2          |

`products`:
| product_id | product_price |
|------------|---------------|
| 1          | 100           |
| 2          | 200           |

### Third Normal Form (3NF)

A table is in 3NF if it is in 2NF and no column is transitively dependent on the primary key.

Consider a table `products`:

| product_id | product_price | category_id | category_name |
|------------|---------------|-------------|---------------|
| 1          | 100           | 10          | Electronics   |
| 2          | 200           | 20          | Books         |
| 3          | 300           | 10          | Electronics   |

Here `category_name` is transitively dependent on the primary key (`product_id`) through `category_id`. To bring this table into 3NF, we can create a separate `categories` table:

`products`:
| product_id | product_price | category_id |
|------------|---------------|-------------|
| 1          | 100           | 10          |
| 2          | 200           | 20          |
| 3          | 300           | 10          |

`categories`:
| category_id | category_name |
|-------------|---------------|
| 10          | Electronics   |
| 20          | Books         |

Now, each table is in 3NF. The `products` table has no transitive dependencies, and the `category_name` in the `categories` table is functionally dependent on `category_id`.

By applying these normalization rules, you can ensure your database is structured efficiently, reducing redundancy and the potential for errors in your data.



# CSE 211 - Mid Solve - Spring 2023 [Question: https://drive.google.com/file/d/1i4Zn1EfytzCPUsWrofOH6vvXJEalX1uW/view?usp=drive_link]

## 1. a) Discuss any two types of database users from below: a. Naive users b. Application programmers c. Sophisticated users d. Database administrators

1. **Naive Users**:
   - Naive users are typically end-users who have minimal understanding of database systems or SQL.
   - They interact with the database through simple interfaces such as forms or predefined queries.
   - Their primary goal is to access information or perform basic operations like data retrieval, insertion, or updating.
   - Examples include clerical staff, receptionists, or non-technical personnel who use database applications as part of their daily tasks.
   - Naive users often rely on user-friendly interfaces provided by application software to interact with the database without needing to know the underlying complexities.

2. **Application Programmers**:
   - Application programmers are professionals who develop software applications that interact with databases.
   - They have intermediate to advanced knowledge of database concepts and SQL.
   - Their primary responsibility is to design, develop, and maintain database-driven applications.
   - Application programmers write code to perform CRUD (Create, Read, Update, Delete) operations, implement business logic, and optimize database interactions.
   - They often work with frameworks and libraries that provide database abstraction layers to simplify database access and management.

3. **Sophisticated Users**:
   - Sophisticated users possess advanced knowledge and skills in database systems and SQL.
   - They include data analysts, business intelligence professionals, and power users who require complex data querying, analysis, and reporting capabilities.
   - Sophisticated users are proficient in writing complex SQL queries, optimizing database performance, and designing efficient database schemas.
   - They often leverage tools such as data visualization software, statistical analysis packages, or advanced database management systems to extract insights from large datasets.
   - Their tasks may involve data mining, predictive modeling, or decision support based on database-derived insights.

4. **Database Administrators (DBAs)**:
   - Database administrators are responsible for managing and maintaining the database system.
   - They have in-depth knowledge of database architecture, configuration, security, and performance tuning.
   - DBAs handle tasks such as database installation, configuration, backup and recovery, user management, and monitoring.
   - They ensure data integrity, availability, and security by implementing access controls, enforcing data consistency, and performing regular maintenance tasks.
   - DBAs also play a crucial role in capacity planning, scaling databases to accommodate growing data volumes, and troubleshooting issues to ensure the smooth operation of the database system.

Each category of users plays a vital role in the successful operation of a database system, with responsibilities ranging from basic data entry to advanced database management and analysis.

## 1. b) The following relational schema form a part of an event management company database held in a relational DBMS

```s
Event (E_ID, E_Name, E_Type)
Guest (G_ID, G_Name, E_ID, V_ID)
Venue (V_ID, V_Name, V_Address)
```

Construct (write down) the Relational Algebra for the following queries:
a) The guest's name having guest ID as 010203.
b) The event's name having the event type as Wedding but not Birthday.
c) The venue IDs where the address is Green Road, Dhaka.

1. **Relational Algebra for Query (a)**:
   - The guest's name having guest ID as 010203.

    ```sql
    π_{G_Name} (σ_{G_ID = '010203'} (Guest))
    ```

2. **Relational Algebra for Query (b)**:
    - The event's name having the event type as Wedding but not Birthday.
  
     ```sql
     π_{E_Name} (σ_{E_Type = 'Wedding' ∧ E_Type ≠ 'Birthday'} (Event))
     ```

3. **Relational Algebra for Query (c)**:
    - The venue IDs where the address is Green Road, Dhaka.

     ```sql
     π_{V_ID} (σ_{V_Address = 'Green Road, Dhaka'} (Venue))
     ```

## 2. a) Construct (write down) the DDL for the above tables with necessary datatypes and constraints

```sql
CREATE TABLE users (
  user_id INT PRIMARY KEY,
  first_name VARCHAR(255),
  last_name VARCHAR(255),
  address VARCHAR(255),
  email VARCHAR(255)
);

CREATE TABLE products (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(255),
  description TEXT,
  price DECIMAL(10,2)
);

CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  user_id INT,
  product_ordered INT,
  total_paid DECIMAL(10,2),
  FOREIGN KEY (user_id) REFERENCES users(user_id),
  FOREIGN KEY (product_ordered) REFERENCES products(product_id)
);
```

## 2. b) The following relational schema form a part of an event management company database held in a relational DBMS

```s
Event (E_ID, E_Name, E_Type)
Guest (G_ID, G_Name, E_ID, V_ID)
Venue (V_ID, V_Name, V_Address)
```

Construct (write down) the SQL for the following queries:
a) The guests' names having the venue address starting with 'E' and ending with 'a" (using subquery).
b) The total number of events for each type of events.
c) The guest IDs for the event ID as 3579.

1. **SQL for Query (a)**:
   - The guests' names having the venue address starting with 'E' and ending with 'a" (using subquery).

    ```sql
    SELECT G_Name
    FROM Guest
    WHERE V_ID IN (SELECT V_ID FROM Venue WHERE V_Address LIKE 'E%a')
    ```

2. **SQL for Query (b)**:
    - The total number of events for each type of events.

    ```sql
    SELECT E_Type, COUNT(*) AS TotalEvents
    FROM Event
    GROUP BY E_Type
    ```

3. **SQL for Query (c)**:
    - The guest IDs for the event ID as 3579.

    ```sql
    SELECT G_ID
    FROM Guest
    WHERE E_ID = 3579
    ```

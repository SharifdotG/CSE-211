# CSE 211 - Final Solve - Spring 2023

## 1. a) Discuss database applications examples in different sectors, such as enterprise information, banking and finance, universities, airlines, telecommunications and navigation systems

**Database Applications Examples in Different Sectors**:

1. **Enterprise Information**:
   - **Sales:** customers, products, purchases, orders, invoices.
   - **Accounting:** payments, receipts, assets, liabilities, financial reports.
   - **Human Resources:** Information about employees, salaries, benefits and payroll taxes.
2. **Manufacturing:** management of production, inventory, orders, supply chain.
3. **Banking and finance**:
   - customer information, accounts, loans, and banking transactions.
   - Credit card transactions and fraud detection.
   - **Finance:** sales and purchases of financial instruments (e.g., stocks and bonds; storing real-time market data)
4. **Universities**: registration, student information, courses, grades, faculty information, research publications.
5. **Airlines**: reservations, schedules, passengers, flights, aircraft maintenance.
6. **Telecommunications**: records of calls, texts, and data usage, generating monthly bills, maintaining balances on prepaid calling cards or mobile phones.
7. **Web-based services:**
   - **Online retailers:** order tracking, customized recommendations based on purchase history.
   - **Social media platforms:** user profiles, connections, posts, likes, comments.
   - **Online advertisements:** targeting ads based on user behavior and preferences.
8. **Document databases:** storing and retrieving unstructured data such as text documents, images, videos, and audio files.
9. **Navigation systems:** For maintaining the locations of varies places of
interest along with the exact routes of roads, train systems, buses, etc.
10. **Healthcare:** patient records, medical history, prescriptions, appointments, billing.

## 1. b) Explain the two-tier and three-tier architectures of database applications with proper examples

**Database applications are usually partitioned into two or three parts**:

1. **Two-Tier Architecture**: the application resides at the client machine, where it invokes database system functionality at the server machine. The client sends SQL queries to the server and receives results. The server processes the queries and sends back the results.
   - **Example**: A simple client-server application where the client interacts directly with the database server. For instance, a desktop application that connects to a central database server to retrieve and update data.
2. **Three-Tier Architecture**: the client machine acts as a front end and does not contain any direct database calls. The application server is the middle tier,which processes the client requests and interacts with the database server to retrieve or update data. The client end communicates with an application server, usually through a forms interface. The application server in turn communicates with a database system to access data.
   - **Example**: A web-based application where the client interacts with a web server that communicates with an application server, which in turn interacts with the database server. For example, an online shopping website where the user interacts with the website (client), which sends requests to the application server to process orders and retrieve product information from the database server.

<img src="https://www.guru99.com/images/1/101318_0734_ThreeTierArchite1.png" alt="Three-Tier Architecture"/>

## 1 OR. a) Discuss the four ACID properties in transaction management

**ACID (Atomicity, Consistency, Isolation, Durability) Properties in Transaction Management:**

1. **Atomicity**: A transaction is atomic, meaning it is an all-or-nothing operation. Either all the operations in the transaction are completed successfully, or none of them are. If any part of the transaction fails, the entire transaction is rolled back to its initial state.
2. **Consistency**: Execution of a transaction in isolation (that is, with no other transaction executing concurrently) preserves the consistency of the database. The database transitions from one consistent state to another consistent state after the transaction is completed.
3. **Isolation**: Even though multiple transactions may execute concurrently, the system guarantees that, for every pair of transactions Ti and Tj , it appears to Ti that either Tj finished execution before Ti started or Tj started execution after Ti finished. Thus, each transaction is unaware of other transactions executing concurrently in the system.
4. **Durability**: After a transaction completes successfully, the changes it has made to the database persist, even if there are system failures. The changes are stored permanently in the database and are not lost due to crashes or power failures.

## 1 OR. b) Explain the logical schema, physical schema, instance and physical data independence in database systems

**Logical Schema**: It is the overall logical structure of the database as seen by the Database Administrator. It describes what data is stored in the database and how the data is related to each other. It includes the tables, columns, keys, constraints, and relationships between tables.

- **Example**: In a university database, the logical schema would define tables for students, courses, instructors, grades, etc., along with the relationships between these entities.

**Physical Schema**: It is the overall physical structure of the database as seen by the operating system. It describes how the data is stored on the storage devices (e.g., hard disks) and the indexing mechanisms used to access the data efficiently.

- **Example**: The physical schema would define the file organization, indexing methods, storage allocation, and access paths used to store and retrieve data efficiently.

**Instance**: It is the actual content of the database at a particular point in time (snapshot). It includes the data stored in the tables, the values of attributes, and the relationships between entities.

- **Example**: An instance of the university database would include the specific student records, course information, instructor details, and grades stored in the database at a given moment.

**Physical Data Independence**: It is the ability to modify the physical schema without changing the logical schema. Applications that use the database are unaffected by changes in the physical storage structures or access methods. Applications depend on the logical schema. In general, the interfaces between the various levels and components should be well defined so that changes in some parts do not seriously influence others.

- **Example**: Changing the storage mechanism from a traditional hard disk to a solid-state drive (SSD) without requiring changes to the application code.

## 2. The following relational schema form a part of a restaurant database held in a relational DBMS

```s
Food (F_ID (PK), F_Name, F_Type, F_Price)
Customer (C_ID (PK), C_Name, F_ID, W_ID)
Waiter (W_ID (PK), W_Name, W_Salary)
```

Construct (write down) the Relational Algebra for the following queries:

a) The food names having fast-food type.
b) The customer names, where the food id is 00101.
c) The waiter names having salary of more than 15,000 taka.
d) The food price of Chicken Fried Rice.
e) The customer IDs, where the waiter ID is 107.

1. **Relational Algebra for Query (a)**:
   - The food names having fast-food type.

    ```sql
    π_{F_Name} (σ_{F_Type = 'Fast-Food'} (Food))
    ```

2. **Relational Algebra for Query (b)**:
    - The customer names, where the food id is 00101.

     ```sql
     π_{C_Name} (σ_{F_ID = '00101'} (Customer))
     ```

3. **Relational Algebra for Query (c)**:
    - The waiter names having salary of more than 15,000 taka.

     ```sql
     π_{W_Name} (σ_{W_Salary > 15000} (Waiter))
     ```

4. **Relational Algebra for Query (d)**:
    - The food price of Chicken Fried Rice.

     ```sql
     π_{F_Price} (σ_{F_Name = 'Chicken Fried Rice'} (Food))
     ```

5. **Relational Algebra for Query (e)**:
    - The customer IDs, where the waiter ID is 107.

     ```sql
     π_{C_ID} (σ_{W_ID = 107} (Customer))
     ```

## 3. Construct (write down) the SQL commands for the following queries

```s
Food (F_ID (PK), F_Name, F_Type, F_Price)
Customer (C_ID (PK), C_Name, F_ID, W_ID)
Waiter (W_ID (PK), W_Name, W_Salary)
```

a) The food type of the most expensive food.
b) The customer names with the food names.
c) The waiter name with the lowest salary.
d) The food prices of the food names starting with 'B' and ending with 'r'.
e) The customer IDs, where the food ID is 200 but not 300.

1. **SQL for Query (a)**:
   - The food type of the most expensive food.

    ```sql
    SELECT F_Type
    FROM Food
    ORDER BY F_Price DESC
    LIMIT 1;
    ```

2. **SQL for Query (b)**:
    - The customer names with the food names.

     ```sql
     SELECT C_Name, F_Name
     FROM Customer
     JOIN Food ON Customer.F_ID = Food.F_ID;
     ```

3. **SQL for Query (c)**:
    - The waiter name with the lowest salary.

     ```sql
     SELECT W_Name
     FROM Waiter
     ORDER BY W_Salary
     LIMIT 1;
     ```

4. **SQL for Query (d)**:
    - The food prices of the food names starting with 'B' and ending with 'r'.

     ```sql
     SELECT F_Price
     FROM Food
     WHERE F_Name LIKE 'B%r';
     ```

5. **SQL for Query (e)**:
    - The customer IDs, where the food ID is 200 but not 300.

     ```sql
     SELECT C_ID
     FROM Customer
     WHERE F_ID = 200 AND C_ID NOT IN (
        SELECT C_ID
        FROM Customer
        WHERE F_ID = 300
     );
     ```

## 4

<img src="https://scontent.fdac24-3.fna.fbcdn.net/v/t1.15752-9/440997720_748667647428547_8899567511663416651_n.png?_nc_cat=104&ccb=1-7&_nc_sid=5f2048&_nc_eui2=AeFHfU5K-SMBwUe8R2N1TaiI989GWU2AuJP3z0ZZTYC4kzZ8qOGXSP2-R-SmQTVOPTxbZB44SjqU3NENMTMYjmjf&_nc_ohc=vQd5iab9QboQ7kNvgEgxFX6&_nc_ht=scontent.fdac24-3.fna&oh=03_Q7cD1QGKPQ0DStQ0oLh5IY0mpSXDF-BuRefFkt7C1qralbXHTg&oe=66702F06" alt="ER Diagram"/>

**Solution**:

<img src="https://images2.imgbox.com/1d/17/s4rIcckV_o.png" alt="ER Diagram"/>

**Explanations**:

1. `EMPLOYEE` table captures personal details of employees with Ssn as the primary key.
2. `DEPARTMENT` table captures department details with Number as the primary key.
3. `PROJECT` table captures project details with Number as the primary key.
4. `DEPENDENT` table captures dependents of employees, using a composite primary key (`Emp_ssn`, `Name`) and `Emp_ssn` as a foreign key referencing `EMPLOYEE`.
5. `WORKS_FOR` table represents the relationship between employees and departments, with a composite primary key (`Emp_ssn`, `Dept_no`) and foreign keys referencing `EMPLOYEE` and `DEPARTMENT`.
6. `MANAGES` table captures the management relationship, where each department is managed by one employee, with foreign keys referencing `EMPLOYEE` and `DEPARTMENT`.
7. `WORKS_ON` table captures which projects employees work on, with `Emp_ssn` and `Proj_no` as a composite primary key and foreign keys referencing `EMPLOYEE` and `PROJECT`.
8. `CONTROLS` table captures which projects are controlled by which departments, with foreign keys referencing `DEPARTMENT` and `PROJECT`.
9. `SUPERVISION` table captures the supervision relationship among employees, with a composite primary key (`Supervisor_ssn`, `Supervisee_ssn`) both referencing `EMPLOYEE`.

## 5. a) Write down two important conditions for each of the following normalization methods: i)INF, ii) 2NF, iii) 3NF

**Normalization Methods**:

1. **INF (1st Normal Form)**:
   - **Conditions**:
     1. Contains only atomic values.
     2. There are no repeating groups or arrays.
2. **2NF (Second Normal Form)**:
   - **Conditions**:
     1. It is in first normal form.
     2. All non-key attributes are fully functional dependent on the primary key.
3. **3NF (Third Normal Form)**:
   - **Conditions**:
     1. It is in second normal form.
     2. There are no transitive functional dependency.

## 5. b)

<img src="https://scontent.fdac24-2.fna.fbcdn.net/v/t1.15752-9/440918569_816667287053661_2225280075197460753_n.png?_nc_cat=111&ccb=1-7&_nc_sid=5f2048&_nc_eui2=AeHRV1Yhgz2-EriMiJATDdO9gHLYzOA2oAeActjM4DagB8D5iLV3G4Ptk5iokWPo7wJRr_mkRogqtOwZa8jRVNHk&_nc_ohc=0Ddet6poI68Q7kNvgEtQB70&_nc_ht=scontent.fdac24-2.fna&oh=03_Q7cD1QELZpdyoQc0b0lohT7IwVFE4u67PfQyY_s8BBFGdud2EA&oe=66705267" alt="ER Diagram"/>

**Solution:**

The given table is already in **1NF** since all values are *atomic*. The primary key here is `Student-ID`. Currently, all attributes (`Name`, `Age`, `Post-Code`, and `City`) depend on `Student-ID`. So, the table is in **2NF**.

***3rd Normal Form (3NF)***: A table is in 3NF if it is in 2NF and all the attributes are functionally dependent only on the primary key and not on any other non-key attribute (i.e., no transitive dependency).

In this case, there is a transitive dependency because City depends on Post-Code, not directly on Student-ID.

To eliminate this, we need to split the table into multiple tables to remove the transitive dependency.

**Table 1: Student:**

| Student-ID | Name | Age |
|------------|------|-----|
| 101        | Mark | 20  |
| 102        | Zakir| 19  |
| 103        | Johny| 21  |
| 104        | Fahim| 20  |
| 105        | Ashik| 21  |

**Table 2: Location:**

| Post-Code | City |
|-----------|------|
| N-45      | New York |
| 1510      | Dhaka    |
| 1200      | Rangpur |
| 1515      | Chittagong |

**Table 3: Student-Location:**

| Student-ID | Post-Code |
|------------|-----------|
| 101        | N-45      |
| 102        | 1510      |
| 103        | 1200      |
| 104        | 1515      |
| 105        | 1200      |

## 5. c) Discuss the weak entity set with an appropriate example

**Weak Entity Set**: A weak entity set in database design is an entity that cannot be uniquely identified by its own attributes alone and relies on a strong entity (identifying entity) through a relationship to provide the necessary identification. A weak entity does not have a primary key unless attributes of the strong entity set it is related to are included.

**Example**: In a library system where information gets managed about books and the specific copies of each book available in the library.

- **Strong Entity Set**: ***Book***
  - Attributes: `ISBN`, `title`, `author`, `publisher`
  - Primary Key: `ISBN`

Each book in the library has a unique ISBN number, this makes it a strong entity set.

- **Weak Entity Set**: ***BookCopy***
  - Attributes: `copy_number`, `condition`, `location`
  - Determined by: `copy_number` (within the context of a specific book)
  - Primary Key: (`ISBN`, `copy_number`)

A specific copy of a book cannot be uniquely identified by `copy_number` alone since `copy_number` might be repeated across different books. Thus, `BookCopy` is a weak entity set that depends on Book for its identification.

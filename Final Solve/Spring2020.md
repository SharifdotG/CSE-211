# CSE 211 - Final Solve (Query and Relational Algebra Only) - Spring 2020 [Question: https://drive.google.com/file/d/1a3FrVFqufxevmaO2ccMlbRP5H80XASYV/view?usp=drive_link]

## 3. The following relational schema form a part of a software company database held in a relational DBMS

```s
Product (Prod_ID (PK), Prod_Name, Prod_Version, Prod_Price)
Developer (Dev_ID (PK), Dev_Name, Prod_ID (FK), T_ID (FK))
Manager (M_ID (PK), M_Name, Prod_ID (FK))
Technology (T_ID (PK), Platform, IDE)
```

Please write down the DML statements (MySQL) for the following queries:
a. Find the developer's name who is working in the Linux platform and his/her ID is equal to the last 5 digits of your own registration number.
b. Show the names of managers working on a product resulting a social media app with version number equal to your own registration number divided by 7 (please calculate the fractional number on your calculator).
c. Find the names of the managers beginning with an 'A' and ends with the last letter of your own last name.
d. List the products developed in Microsoft Visual Studio only and the product name's length is equal to the length of your own name.
e. Show the names of developers with their respective managers' names where substring of their names must match with your own last name. Please sort the results in an alphabetically descending order of the managers' names.
f. List the Windows product names but not the Apple ones.

**Solution:**

a. Find the developer's name who is working in the Linux platform and his/her ID is equal to the last 5 digits of your own registration number.

```sql
SELECT Dev_Name
FROM Developer
WHERE T_ID = 'Linux' AND Dev_ID = 10128;
```

b. Show the names of managers working on a product resulting a social media app with version number equal to your own registration number divided by 7 (please calculate the fractional number on your calculator).

```sql
SELECT M_Name
FROM Manager
WHERE Prod_ID = 'SocialMedia' AND Prod_Version = 3157304.00;
```

c. Find the names of the managers beginning with an 'A' and ends with the last letter of your own last name.

```sql
SELECT M_Name
FROM Manager
WHERE M_Name LIKE 'A%f';
```

d. List the products developed in Microsoft Visual Studio only and the product name's length is equal to the length of your own name.

```sql
SELECT Prod_Name
FROM Product
WHERE Prod_Name LIKE 'Microsoft Visual Studio' AND LENGTH(Prod_Name) = 17;
```

e. Show the names of developers with their respective managers' names where substring of their names must match with your own last name. Please sort the results in an alphabetically descending order of the managers' names.

```sql
SELECT Dev_Name, M_Name
FROM Developer, Manager
WHERE Dev_Name LIKE '%Yousuf' AND Dev_ID = M_ID
ORDER BY M_Name DESC;
```

f. List the Windows product names but not the Apple ones.

```sql
SELECT Prod_Name
FROM Product
WHERE Prod_Name LIKE 'Windows' AND Prod_Name NOT LIKE 'Apple';
```

## 3 OR. The following relational schema form a part of a software company database held in a relational DBMS

```s
Product (Prod_ID (PK), Prod_Name, Prod_Version, Prod_Price)
Developer (Dev_ID (PK), Dev_Name, Prod_ID (FK), T_ID (FK))
Manager (M_ID (PK), M_Name, Prod_ID (FK))
Technology (T_ID (PK), Platform, IDE)
```

Please write down the DML statements for the following queries:
a. Find the total number of developers working on Android Studio with a product ID same as your own registration number.
b. Show the total product price developed for iOS divided by the last two digits of your own registration number.
c. List the product pricing in a descending order where the price is lower than the average price of a Linux product.
d. Show the cheapest iPhone products managed by you. (Hint: you are the manager and you use your own registration number as M_ID)
e. Find the most expensive products managed by you. (Hint: you are the manager and you have to use your own name as M_Name)
f. List the manager's name same as your own name and manages products developed by the senior-most developer. (Hint: the more senior a developer is, the lesser his/her Dev_ID is in terms of length)

**Solution:**

a. Find the total number of developers working on Android Studio with a product ID same as your own registration number.

```sql
SELECT COUNT(Dev_ID)
FROM Developer
WHERE T_ID = 'Android Studio' AND Prod_ID = 22101128;
```

b. Show the total product price developed for iOS divided by the last two digits of your own registration number.

```sql
SELECT SUM(Prod_Price) / 28
FROM Product
WHERE Prod_Name LIKE 'iOS%';
```

c. List the product pricing in a descending order where the price is lower than the average price of a Linux product.

```sql
SELECT Prod_Price
FROM Product
WHERE Prod_Price < (
    SELECT AVG(Prod_Price)
    FROM Product
    WHERE Prod_Name LIKE 'Linux%'
) ORDER BY Prod_Price DESC;
```

d. Show the cheapest iPhone products managed by you. (Hint: you are the manager and you use your own registration number as M_ID)

```sql
SELECT Prod_Name
FROM Product
WHERE Prod_Name LIKE 'iPhone%' AND Prod_Price = (
    SELECT MIN(Prod_Price)
    FROM Product
    WHERE M_ID = 22101128
);
```

e. Find the most expensive products managed by you. (Hint: you are the manager and you have to use your own name as M_Name)

```sql
SELECT Prod_Name
FROM Product
WHERE Prod_Price = (
    SELECT MAX(Prod_Price)
    FROM Product
    WHERE M_Name = 'Sharif Md. Yousuf'
);
```

f. List the manager's name same as your own name and manages products developed by the senior-most developer. (Hint: the more senior a developer is, the lesser his/her Dev_ID is in terms of length)

```sql
SELECT M_Name
FROM Manager
WHERE M_Name = 'Sharif Md. Yousuf' AND Prod_ID = (
    SELECT Prod_ID
    FROM Developer
    WHERE Dev_ID = (
        SELECT MIN(Dev_ID)
        FROM Developer
    )
);
```

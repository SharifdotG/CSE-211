# CSE 211 - Final Solve (Query and Relational Algebra Only) - Spring 2022 [Question: https://drive.google.com/file/d/1-Cxuf89WOHHnFg6NL87x46JJsXUnHvw2/view?usp=drive_link]

## 1. The following relational schema form a part of the 45th ICPC World Finals Dhaka Volunteers database stored in a relational DBMS

```s
Volunteers (V_ID (PK), V_firstName, V_lastName, V_WhatsApp)
Hospitality (H_ID (PK), English_Skills_Level, Communication_Skills_Level)
Technical (T_ID (PK), Computer_Skills_Level)
```

Construct the Relational Algebra to find out the following:
a. Last name of the volunteer having WhatsApp number +8801971512022.
b. IDs of hospitality volunteers having fluent English skills.
c. Skill level of technical volunteers having ID as 0045.
d. IDs of volunteers having first name as "Md.".
e. Communication level of hospitality volunteers having average English skills.

**Solution:**

a. Last name of the volunteer having WhatsApp number +8801971512022.

```s
π V_lastName (σ V_WhatsApp = '+8801971512022' (Volunteers))
```

b. IDs of hospitality volunteers having fluent English skills.

```s
π H_ID (σ English_Skills_Level = 'Fluent' (Hospitality))
```

c. Skill level of technical volunteers having ID as 0045.

```s
π Computer_Skills_Level (σ T_ID = '0045' (Technical))
```

d. IDs of volunteers having first name as "Md.".

```s
π V_ID (σ V_firstName = 'Md.' (Volunteers))
```

e. Communication level of hospitality volunteers having average English skills.

```s
π Communication_Skills_Level (σ English_Skills_Level = 'Average' (Hospitality))
```

## 2. The following relational schema form a part of the 45th ICPC World Finals Dhaka Volunteers database stored in a relational DBMS

```s
Volunteers (V_ID (PK), V_firstName, V_lastName, V_WhatsApp)
Hospitality (H_ID (PK), English_Skills_Level, Communication_Skills_Level)
Technical (T_ID (PK), Computer_Skills_Level)
```

Construct the DML statements to find out the following:
a. First name of the volunteer having WhatsApp number ending with 2022.
b. IDs of hospitality volunteers having fluent English skills but average communication skills.
c. Skill level of technical volunteers having IDs from 001 to 275.
d. Number of volunteers having last name as "Rahman".
e. Communication level of hospitality volunteers having above average English skills with IDs starting with 1.

**Solution:**

a. First name of the volunteer having WhatsApp number ending with 2022.

```sql
SELECT V_firstName
FROM Volunteers
WHERE V_WhatsApp LIKE '%2022';
```

b. IDs of hospitality volunteers having fluent English skills but average communication skills.

```sql
SELECT H_ID
FROM Hospitality
WHERE English_Skills_Level = 'Fluent' AND Communication_Skills_Level = 'Average';
```

c. Skill level of technical volunteers having IDs from 001 to 275.

```sql
SELECT Computer_Skills_Level
FROM Technical
WHERE T_ID BETWEEN '001' AND '275';
```

d. Number of volunteers having last name as "Rahman".

```sql
SELECT COUNT(*)
FROM Volunteers
WHERE V_lastName = 'Rahman';
```

e. Communication level of hospitality volunteers having above average English skills with IDs starting with 1.

```sql
SELECT Communication_Skills_Level
FROM Hospitality
WHERE English_Skills_Level = 'Above Average' AND H_ID LIKE '1%';
```

## 3. The following relational schema form a part of the 45th ICPC World Finals Dhaka Volunteers database stored in a relational DBMS

```s
Volunteers (V_ID (PK), V_firstName, V_lastName, V_WhatsApp)
Hospitality (H_ID (PK), English_Skills_Level, Communication_Skills_Level)
Technical (T_ID (PK), Computer_Skills_Level)
```

Construct the DML statements (MySQL) to find out the following:
a. Full name of the volunteers having IDs starting with 2 and ending with 0.
b. IDs of volunteers having excellent computer skills and fluent English skills.
c. Skill level of hospitality volunteers having ID from 100 to 150.
d. Volunteers having first name updated from "Md." to "Muhammad".
e. Hospitality volunteers removed from database having below average English skills.

**Solution:**

a. Full name of the volunteers having IDs starting with 2 and ending with 0.

```sql
SELECT CONCAT(V_firstName, ' ', V_lastName) AS Full_Name
FROM Volunteers
WHERE V_ID LIKE '2%0';
```

b. IDs of volunteers having excellent computer skills and fluent English skills.

```sql
SELECT V_ID
FROM Volunteers
WHERE V_ID IN (
    SELECT H_ID
    FROM Hospitality
    WHERE English_Skills_Level = 'Fluent' AND Communication_Skills_Level = 'Excellent'
);
```

c. Skill level of hospitality volunteers having ID from 100 to 150.

```sql
SELECT English_Skills_Level
FROM Hospitality
WHERE H_ID BETWEEN '100' AND '150';
```

d. Volunteers having first name updated from "Md." to "Muhammad".

```sql
UPDATE Volunteers
SET V_firstName = 'Muhammad'
WHERE V_firstName = 'Md.';
```

e. Hospitality volunteers removed from database having below average English skills.

```sql
DELETE FROM Hospitality
WHERE English_Skills_Level = 'Below Average';
```

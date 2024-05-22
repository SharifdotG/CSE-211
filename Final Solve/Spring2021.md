# CSE 211 - Final Solve (Query and Relational Algebra Only) - Spring 2021 [Question: https://drive.google.com/file/d/1c7AjYI9Zz-LFeIPUWbfS8_RY85WG3qGt/view?usp=sharing]

## 1. The following relational schema form a part of a hospital database held in a relational DBMS

```s
Patient (P_ID (PK), P_Name, P_Age, P_Contact)
Doctor (D_ID (PK), D_First_Name, D_Last_Name, Specialization)
Appointment (A_ID (PK), P_ID (FK), D_ID (FK), Date, Time)
```

Please write down the Relational Algebra for the following queries:
a. Find the age of the patient having ID same as your own registration number.
b. Show the patient’s contact whose ID is same as last 4 digits of your own registration number.
c. List the doctors specialized in Surgery and having the same last name as yours.
d. Show the date and time of an appointment where patient ID is same as the last 2 digits of your own registration number.
e. Find the patients’ names who have taken appointments for the doctors specialized in Cardiology but not in Neurology.
f. List the doctor’s first name whose ID is same as first 3 digits of your own registration number.

**Solution:**

a. Find the age of the patient having ID same as your own registration number.

```s
π P_Age (σ P_ID = 22101128 (Patient))
```

b. Show the patient’s contact whose ID is same as last 4 digits of your own registration number.

```s
π P_Contact (σ P_ID = 1128 (Patient))
```

c. List the doctors specialized in Surgery and having the same last name as yours.

```s
π D_First_Name, D_Last_Name (σ Specialization = 'Surgery' ^ D_Last_Name = 'Sharif' (Doctor))
```

d. Show the date and time of an appointment where patient ID is same as the last 2 digits of your own registration number.

```s
π Date, Time (σ P_ID = 28 (Appointment))
```

e. Find the patients’ names who have taken appointments for the doctors specialized in Cardiology but not in Neurology.

```s
π P_Name (σ Specialization = 'Cardiology' ^ Specialization ≠ 'Neurology' (Patient ⨝ Appointment ⨝ Doctor))
```

f. List the doctor’s first name whose ID is same as first 3 digits of your own registration number.

```s
π D_First_Name (σ D_ID = 221 (Doctor))
```

## 1 OR. The following relational schema form a part of a hospital database held in a relational DBMS

```s
Patient (P_ID (PK), P_Name, P_Age, P_Contact)
Doctor (D_ID (PK), D_First_Name, D_Last_Name, Specialization)
Appointment (A_ID (PK), P_ID (FK), D_ID (FK), Date, Time)
```

Please write down the DML statements (MySQL) for the following queries:
a. Show the total number of doctors specialized in Surgery.
b. List the date and time of the appointments where patients’ ages are same as yours.
c. Find the total age of the patients having name starting with the first letter of your own last name and ending with the last letter of your own first name.
d. List the doctors specialized in Neurology or Cardiology.
e. Show the names of the patients having contact number same as the first 5 digits of your own registration number.
f. Find the specialization of the doctors whose first names are same as yours.

**Solution:**

a. Show the total number of doctors specialized in Surgery.

```sql
SELECT COUNT(*) AS Total_Surgeons
FROM Doctor
WHERE Specialization = 'Surgery';
```

b. List the date and time of the appointments where patients’ ages are same as yours.

```sql
SELECT Date, Time
FROM Appointment
WHERE P_ID IN (
    SELECT P_ID
    FROM Patient
    WHERE P_Age = 23
);
```

c. Find the total age of the patients having name starting with the first letter of your own last name and ending with the last letter of your own first name.

```sql
SELECT SUM(P_Age) AS Total_Age
FROM Patient
WHERE P_Name LIKE 'S%f';
```

d. List the doctors specialized in Neurology or Cardiology.

```sql
SELECT D_First_Name, D_Last_Name
FROM Doctor
WHERE Specialization IN ('Neurology', 'Cardiology');
```

e. Show the names of the patients having contact number same as the first 5 digits of your own registration number.

```sql
SELECT P_Name
FROM Patient
WHERE P_Contact LIKE '22101%';
```

f. Find the specialization of the doctors whose first names are same as yours.

```sql
SELECT Specialization
FROM Doctor
WHERE D_First_Name = 'Sharif';
```

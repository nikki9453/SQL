# 🏥 Hospital Data Analysis Using PostgreSQL

A PostgreSQL SQL project focused on analyzing hospital data and answering real-world healthcare business questions.

The project uses SQL to analyze patient volumes, doctors, hospital departments, medical expenses, patient length of stay, city-wise patient distribution, and monthly healthcare expenses.

---

## 📌 Project Overview

This project analyzes hospital-related data using PostgreSQL.

The dataset contains information related to:

* Hospitals
* Departments
* Patient counts
* Doctor counts
* Medical expenses
* Admission dates
* Discharge dates
* Hospital locations

The project contains **10 SQL business questions** designed to practice and demonstrate practical SQL and data analysis skills.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Analyze the total number of patients
* Compare doctors across hospitals
* Identify departments with the highest patient volume
* Find hospitals with the highest medical expenses
* Calculate average daily medical expenses
* Identify the longest hospital stay
* Analyze patients by city
* Calculate average length of stay by department
* Identify departments with the lowest patient volume
* Create a monthly medical expenses report

---

## 🗃️ Dataset

The analysis is performed on a hospital dataset containing fields such as:

| Column           | Description                   |
| ---------------- | ----------------------------- |
| Hospital Name    | Name of the hospital          |
| Department       | Hospital department           |
| Patients Count   | Number of patients            |
| Doctors Count    | Number of doctors             |
| Medical Expenses | Medical expenses recorded     |
| Admission Date   | Patient admission date        |
| Discharge Date   | Patient discharge date        |
| Location         | City/location of the hospital |

---

## 📊 SQL Questions Solved

### 1. Total Number of Patients

Find the total number of patients across all hospitals.

**Result:** 9,347 patients.

---

### 2. Average Number of Doctors per Hospital

Calculate the average number of doctors available in each hospital.

The analysis compares hospitals such as City Hospital, Healing Touch, Global Medicare, Fortis Care, Sunrise Medical, Green Valley Hospital, Heritage Hospital, Metro Hospital, Apollo Health, and Wellness Clinic.

---

### 3. Top 3 Departments with the Highest Number of Patients

Identify the three departments with the highest patient volume.

**Results:**

| Department | Total Patients |
| ---------- | -------------: |
| Urology    |          1,766 |
| Neurology  |          1,229 |
| ENT        |          1,064 |

---

### 4. Hospital with the Maximum Medical Expenses

Identify the hospital with the highest recorded medical expense.

**Result:**

**Healing Touch — 49,955.41**

---

### 5. Daily Average Medical Expenses

Calculate the average medical expense per hospital stay day.

This analysis converts admission and discharge date strings into PostgreSQL date values and calculates the length of stay before determining the daily average expense.

---

### 6. Longest Hospital Stay

Find the patient/hospital record with the longest stay by calculating the difference between discharge and admission dates.

**Result:**

| Hospital      | Department |    Stay |
| ------------- | ---------- | ------: |
| Apollo Health | ENT        | 15 days |

---

### 7. Total Patients Treated Per City

Calculate the total number of patients treated in each city.

**Top cities:**

| City      | Total Patients |
| --------- | -------------: |
| Jaipur    |          1,505 |
| Ahmedabad |          1,467 |
| Lucknow   |          1,264 |
| Hyderabad |          1,261 |
| Bangalore |            955 |

---

### 8. Average Length of Stay per Department

Calculate the average number of days patients spend in each department.

**Results include:**

| Department       | Average Stay |
| ---------------- | -----------: |
| Neurology        |    9.25 days |
| Pediatrics       |    9.11 days |
| Urology          |    8.72 days |
| Oncology         |    8.11 days |
| ENT              |    8.08 days |
| Gynecology       |    7.67 days |
| General Medicine |    7.43 days |
| Orthopedics      |    7.14 days |
| Cardiology       |    6.86 days |
| Dermatology      |    5.60 days |

---

### 9. Department with the Lowest Number of Patients

Identify the department with the lowest total number of patients.

**Result:**

**Cardiology — 544 patients**

---

### 10. Monthly Medical Expenses Report

Calculate total medical expenses for each month.

| Month     | Total Medical Expenses |
| --------- | ---------------------: |
| January   |             173,971.54 |
| February  |             301,722.72 |
| March     |             199,247.42 |
| April     |              88,995.93 |
| May       |             222,986.72 |
| June      |             165,926.36 |
| July      |             211,527.13 |
| August    |             181,039.55 |
| September |             341,284.23 |
| October   |             158,450.68 |
| November  |             334,370.33 |
| December  |             337,788.45 |

The monthly analysis shows **September** as the month with the highest recorded medical expenses.

---

## 🧠 SQL Concepts Used

This project demonstrates practical PostgreSQL concepts including:

### Aggregate Functions

* `SUM()`
* `AVG()`
* `MAX()`

### Grouping & Sorting

* `GROUP BY`
* `ORDER BY`
* `LIMIT`

### Date Functions

* `TO_DATE()`
* `TO_CHAR()`
* `EXTRACT()`

### Conditional Logic

* `CASE`
* `WHEN`
* `ELSE`

### Data Transformation

* Converting text-based dates into PostgreSQL dates
* Calculating date differences
* Calculating average stay duration
* Calculating daily medical expenses

### SQL Analysis Techniques

* Hospital-wise analysis
* Department-wise analysis
* City-wise analysis
* Monthly trend analysis
* Ranking and top-N analysis

---

## 💻 Example SQL Queries

### Total Number of Patients

```sql
SELECT
    SUM("Patients Count") AS "Total Patients"
FROM hospital_data;
```

---

### Top 3 Departments by Patient Count

```sql
SELECT
    "Department",
    SUM("Patients Count") AS "Total Patients"
FROM hospital_data
GROUP BY "Department"
ORDER BY "Total Patients" DESC
LIMIT 3;
```

---

### Department with Lowest Patient Count

```sql
SELECT
    "Department",
    SUM("Patients Count") AS "Total Patients"
FROM hospital_data
GROUP BY "Department"
ORDER BY "Total Patients" ASC
LIMIT 1;
```

---

### Longest Hospital Stay

```sql
SELECT
    "Hospital Name",
    "Department",
    "Admission Date",
    "Discharge Date",
    (
        CASE
            WHEN "Discharge Date" LIKE '%/%'
            THEN TO_DATE("Discharge Date", 'DD/MM/YYYY')
            ELSE TO_DATE("Discharge Date", 'DD-MM-YYYY')
        END
        -
        CASE
            WHEN "Admission Date" LIKE '%/%'
            THEN TO_DATE("Admission Date", 'DD/MM/YYYY')
            ELSE TO_DATE("Admission Date", 'DD-MM-YYYY')
        END
    ) AS "Stay Days"
FROM hospital_data
ORDER BY "Stay Days" DESC
LIMIT 1;
```

---

## 🛠️ Tools & Technologies

* **PostgreSQL**
* **SQL**
* **pgAdmin 4**
* **Git**
* **GitHub**

## 🚀 How to Run the Project

### 1. Install PostgreSQL

Install PostgreSQL and use pgAdmin 4 or another PostgreSQL client.

### 2. Create a Database

Create a new PostgreSQL database.

```sql
CREATE DATABASE hospital_analysis;
```

### 3. Create the Table

Create the `hospital_data` table using the SQL schema provided in the project.

### 4. Import the Dataset

Import the hospital dataset into the `hospital_data` table.

### 5. Run the Queries

Open:

```text
sql/hospital_analysis.sql
```

Execute the queries in PostgreSQL.


## 🎓 Skills Demonstrated

This project demonstrates practical knowledge of:

* PostgreSQL
* SQL querying
* Data aggregation
* Healthcare data analysis
* Date manipulation
* String-to-date conversion
* Business question solving
* Grouping and ranking
* Hospital and department analysis
* Time-based analysis

---

## 🚀 Future Improvements

This project can be extended by:

* Creating a Power BI healthcare dashboard
* Adding patient demographic analysis
* Analyzing hospital performance
* Comparing medical expenses between departments
* Creating monthly patient trends
* Calculating revenue/expense KPIs
* Adding window functions
* Using CTEs for complex analysis
* Creating interactive visualizations


## 📜 License

This project is created for educational and portfolio purposes.

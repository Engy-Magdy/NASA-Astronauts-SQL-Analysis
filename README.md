# 🚀 NASA Astronauts SQL Database Analysis

![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Relational_Database-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## 📋 Overview
This project models and analyzes a sample dataset of **33 NASA Astronauts** selected between **1990 and 2009** using **SQLite**. It demonstrates core relational database concepts, including schema creation, data insertion, conditional logic (`CASE`), aggregate functions, and grouping filters (`GROUP BY` & `HAVING`).

---

## 🗂️ Database Schema
The database consists of a single table, `NASA_Astronauts_Sample`, structured as follows:

| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `id` | `INTEGER` | `PRIMARY KEY AUTOINCREMENT` — Unique identifier for each astronaut |
| `Name` | `TEXT` | Full name of the astronaut |
| `Year` | `INTEGER` | Year selected into the NASA astronaut program |
| `Groups` | `INTEGER` | NASA Astronaut Group number |
| `Status` | `TEXT` | Current status (`Active`, `Retired`, `Management`, `Deceased`) |
| `Birth_Day` | `TEXT` | Date of birth (`YYYY-MM-DD`) |
| `Birth_Place` | `TEXT` | City and state/country of birth |
| `Gender` | `TEXT` | Gender (`Male`, `Female`) |
| `Alma_Mater` | `TEXT` | Universities/institutions attended |
| `Undergraduate_Major` | `TEXT` | Undergraduate field of study (nullable) |
| `Graduate_Major` | `TEXT` | Graduate field of study (nullable) |

---

## 🔍 Key Queries & Analysis

### 1. Chronological Sorting
Retrieves all astronaut records ordered by their selection year to observe recruitment timelines.
```sql
SELECT * FROM NASA_Astronauts_Sample ORDER BY Year;

### 2. Average Tenure Calculation
Calculates the average number of years elapsed since the astronauts joined NASA (referenced to 2026), rounded to one decimal place.

SQL
SELECT ROUND(AVG(2026 - Year), 1) AS "Average_Years_Since_Joining"
FROM NASA_Astronauts_Sample;

### 3. Experience Level Classification (CASE Statement)
Categorizes astronauts currently in service (Active or Management) into experience tiers based on years since selection, labeling Retired and Deceased astronauts as N/A:

Astronaut Candidate: Less than 4 years

Mission Specialist: 4 to 11 years

Veteran Astronaut: More than 11 years

SQL
SELECT Name, Year,
  CASE
    WHEN (2026 - Year) < 4 AND Status IN ('Active', 'Management') THEN 'Astronaut Candidate'
    WHEN (2026 - Year) <= 11 AND Status IN ('Active', 'Management') THEN 'Mission Specialist'
    WHEN (2026 - Year) > 11 AND Status IN ('Active', 'Management') THEN 'Veteran Astronaut'
    ELSE 'N/A'
  END AS 'The experience'
FROM NASA_Astronauts_Sample;

### 4. Gender Distribution
Aggregates the total count of astronauts by gender.

SQL
SELECT Gender, COUNT(*) AS Number 
FROM NASA_Astronauts_Sample 
GROUP BY Gender;

### 5. Cohort Size Filtering (GROUP BY & HAVING)
Identifies NASA astronaut groups in the sample that contain 3 or more members.

SQL
SELECT Groups, COUNT(*) AS Members
FROM NASA_Astronauts_Sample
GROUP BY Groups
HAVING COUNT(*) >= 3;

###🚀 How to Run
Clone the repository:

Bash
git clone [https://github.com/Engy-Magdy/your-repo-name.git](https://github.com/Engy-Magdy/your-repo-name.git)
Open in SQLite:

Launch DB Browser for SQLite (or any SQLite client).

Create a new database and open the .sql script in the Execute SQL tab.

Run the script to build the table, populate the 33 records, and view the query outputs.

###📄 Data Notes
Some records contain NULL values in Undergraduate_Major or Graduate_Major where degree details were unavailable in the source sample

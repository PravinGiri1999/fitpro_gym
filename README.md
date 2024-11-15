---

# FitPro Gym SQL Project

![Project Image Placeholder](https://wallpaperaccess.com/full/4722389.jpg) 

Welcome to my first SQL project, where I analyze real-time gym data from **FitPro Gym**! This project uses a dataset of **10,000 visit records** to explore and analyze gym membership and visit data, answering key business questions that can help a fitness center understand its customer base better and optimize its services.

## Table of Contents
- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Business Problems](#business-problems)
- [SQL Queries & Analysis](#sql-queries--analysis)
- [Getting Started](#getting-started)
- [Questions & Feedback](#questions--feedback)
- [Contact Me](#contact-me)

---

## Introduction

This project aims to demonstrate essential SQL skills by analyzing a dataset from FitPro Gym. Using SQL, I explored membership details, member demographics, and visit patterns to derive actionable insights. This project showcases fundamental SQL techniques, including creating tables, writing queries, and analyzing data.

## Project Structure

1. **SQL Scripts**: Code to create the database schema and queries for analysis.
2. **Dataset**: Real-time data on gym visits, membership, and member demographics.
3. **Analysis**: SQL queries solving practical business problems, each one crafted to address specific questions.

---

## Database Schema

Here’s an overview of the database structure:

### 1. **Members Table**
- **member_id**: Unique identifier for each member
- **name**: Name of the member

### 2. **Memberships Table**
- **member_id**: Unique identifier linked to the `members` table
- **age**: Age of the member
- **gender**: Gender of the member ('M' or 'F')
- **membership_type**: Type of membership (e.g., Monthly, Quarterly)
- **join_date**: Date when the member joined
- **status**: Membership status (e.g., Active, Cancelled)

### 3. **Visits Table**
- **visit_id**: Unique identifier for each visit
- **member_id**: Linked to the `members` table
- **visit_date**: Date of the visit
- **check_in_time**: Check-in time of the visit
- **check_out_time**: Check-out time of the visit

## Business Problems

The following queries were created to solve specific business questions. Each query is designed to provide insights based on gym membership and visit data.

1. Retrieve the **name** and **membership_type** of female members.
  ```sql
SELECT 
m.name,
ms.membership_type
FROM members as m
INNER JOIN memberships as ms
ON m.member_id=ms.member_id
WHERE ms.gender='F';
```
2. Find members who have a **Monthly membership** and joined after **2023-11-01**.
 ```sql
SELECT m.name,
ms.membership_type,
ms.join_date
FROM members AS m
INNER JOIN memberships AS ms
ON m.member_id=ms.member_id
WHERE 
membership_type = 'Monthly'
AND 
join_date > '2023-11-01';
 ```
3. List the **name** and **status** of active members over **25**.
 ```sql
SELECT m.name, ms.status
FROM members AS m
INNER JOIN memberships AS ms
ON m.member_id=ms.member_id
WHERE status = 'Active' 
AND
age > 25;
 ```
4. Get details of **visits** on a specific date (**2024-01-01**).
```sql
SELECT * FROM visits
WHERE visit_date = '2024-01-01';
```
5. List members with a **Quarterly membership** aged between **20 and 30**.
```sql
SELECT * FROM memberships
WHERE membership_type = 'Quaterly'
AND
age BETWEEN 20 AND 30;
```

Additional aggregations and grouping:

6. Count total visits made by each member.
```sql
SELECT 
member_id,
COUNT(visit_id) AS total_visits
FROM visits
GROUP BY member_id
ORDER BY 1 ASC;
```
7. Count members by membership type (e.g., Monthly, Weekly, Quarterly).
```sql
SELECT 
membership_type,
COUNT(member_id) AS members
FROM memberships
GROUP BY membership_type;
```
8. Calculate the average age of members, grouped by membership type.
```sql
SELECT 
membership_type,
AVG(member_id) AS members_avg
FROM memberships
GROUP BY membership_type;
```
9. Total visits for each visit date.
```sql
SELECT 
visit_date,
COUNT(visit_id) AS total_visits
FROM visits
GROUP BY visit_date;
```
10. Count members by status (e.g., Active or Cancelled).
```sql
SELECT 
status,
COUNT(member_id) AS  members
FROM memberships
WHERE status = 'Active'
OR
status = 'Cancelled'
GROUP BY status;
```

Advanced queries:
11. Top 3 members with the highest visits.
```sql
SELECT 
m.name,
COUNT(v.visit_id) AS total_visits
FROM visits AS v
INNER JOIN members AS m
ON v.member_id=m.member_id
GROUP BY m.name
HAVING COUNT(v.visit_id) > 0
ORDER BY total_visits DESC
LIMIT 3;
```
12. Active Monthly members grouped by membership type, sorted by recent join dates.
```sql
SELECT
membership_type,
COUNT(member_id) AS members
FROM memberships
WHERE status = 'Active'
AND
membership_type = 'Monthly'
GROUP BY membership_type;
```
13. Members with more than 2 visits, sorted by total visits, displaying the top 5.
```sql
SELECT
member_id,
COUNT(visit_id) AS total_visits
FROM visits
GROUP BY member_id
HAVING COUNT(visit_id) > 2
ORDER BY total_visits ASC
LIMIT 5;
```
14. Members who joined in 2023, grouped by membership type (where each group has >1 member).
```sql
SELECT 
membership_type,
COUNT(member_id) AS total_members
FROM memberships
WHERE EXTRACT(YEAR FROM join_date) = 2023
GROUP BY membership_type
HAVING COUNT(member_id) > 1;
```
15. Average age of active members, grouped by membership type, limited to the top 3 results.
```sql
SELECT 
membership_type,
AVG(age) AS avg_age
FROM memberships
WHERE status = 'Active'
GROUP BY membership_type
ORDER BY membership_type ASC
LIMIT 3;
```
---

## SQL Queries & Analysis

The `analysis.sql` file contains all SQL queries developed for this project. Each query corresponds to a business problem and demonstrates skills in SQL syntax, data filtering, aggregation, grouping, and ordering.

## Getting Started

### Prerequisites
- PostgreSQL (or any SQL-compatible database)
- Basic understanding of SQL

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/fitpro-gym-sql-project.git
   ```
2. **Set Up the Database**:
   - Run the `schema.sql` script to set up tables and insert sample data.

3. **Run Queries**:
   - Execute each query in `analysis.sql` to explore and analyze the data.

---

## Questions & Feedback

If you have any questions or feedback, feel free to create an issue or reach out!

---

## Contact Me

📄 **[Resume](#)**  
📧 **[Email](mailto:your.pravingiri2222@example.com)**  
📞 **Phone**: +123-456-7890  

--

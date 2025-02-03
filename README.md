# 📊 Data Analyst Job Market Analysis

## Introduction
Dive into the **data analyst job market!** This project explores:
- 💰 **Top-paying jobs**
- 🔥 **In-demand skills**
- 📈 **Where high demand meets high salary** in data analytics

🔍 **SQL queries?** Check them out in the [project_sql folder](/project_sql/) folder.

---
## 📌 Background
This project was born from a desire to navigate the **data analyst job market** effectively by pinpointing **top-paid and in-demand skills.** The goal is to help others streamline their job search and focus on optimal skills.

### 📂 **Dataset**
The data comes from lukebarousse's SQL Course and contains insights on:
- Job titles 🏢
- Salaries 💵
- Locations 🌍
- Essential skills 🎯

### ❓ **Key Questions Answered**
- What are the **top-paying** data analyst jobs?
- What **skills** are required for these high-paying roles?
- Which **skills** are most in demand?
- What skills are associated with **higher salaries**?
- What are the **most optimal** skills to learn?

---
## 🛠 Tools Used
For this deep dive into the **data analyst job market**, I leveraged:
- **SQL** – The backbone of the analysis, extracting critical insights
- **PostgreSQL** – My database management system of choice
- **Visual Studio Code** – For database management and executing SQL queries
- **Git & GitHub** – Version control and collaboration

---
## 🔎 Analysis & SQL Queries
Each query investigates a specific aspect of the data analyst job market.

### 1️⃣ **Top-Paying Data Analyst Jobs**
To find the highest-paying roles, I filtered job postings by **average salary and location** (remote jobs only).

```sql
SELECT
	job_id, job_title, job_location, job_schedule_type,
	salary_year_avg, job_posted_date, name AS company_name
FROM job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE job_title_short = 'Data Analyst'
AND job_location = 'Anywhere'
AND salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10;
```

### 📊 **Findings:**
- **Wide Salary Range**: Top 10 salaries range from **$184,000 to $650,000**
- **Diverse Employers**: Companies like **SmartAsset, Meta, and AT&T** pay well
- **Varied Job Titles**: Roles range from **Data Analyst** to **Director of Analytics**

---
### 2️⃣ **Skills for Top-Paying Jobs**
I analyzed the most common skills in the highest-paying job listings.

```sql
WITH top_paying_jobs AS (
    SELECT job_id, job_title, salary_year_avg, name AS company_name
    FROM job_postings_fact
    LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
    WHERE job_title_short = 'Data Analyst'
    AND job_location = 'Anywhere'
    AND salary_year_avg IS NOT NULL
    ORDER BY salary_year_avg DESC
    LIMIT 10)

SELECT top_paying_jobs.*, skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY salary_year_avg DESC;
```

### 📊 **Findings:**
- **Most common skills in high-paying jobs:**
  - **SQL** (8 times)  
  - **Python** (7 times)  
  - **Tableau** (6 times)  
  - Other skills: **R, Snowflake, Pandas, Excel**

---
### 3️⃣ **Most In-Demand Skills**
I examined the most frequently required skills in **data analyst job postings**.

```sql
SELECT skills, COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE job_title_short = 'Data Analyst'
AND job_work_from_home = True
GROUP BY skills
ORDER BY demand_count DESC
LIMIT 5;
```

### 📊 **Findings:**
| Skill | Demand Count |
|------------|--------------|
| **SQL** | 7291 |
| **Excel** | 4611 |
| **Python** | 4330 |
| **Tableau** | 3745 |
| **Power BI** | 2609 |

🔹 **SQL and Excel** remain fundamental 🏆  
🔹 **Python, Tableau, and Power BI** are essential for data storytelling 📊

---
### 4️⃣ **Skills Based on Salary**
I explored which skills are associated with **higher salaries**.

```sql
SELECT skills, ROUND(AVG(salary_year_avg), 0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE job_title_short = 'Data Analyst'
AND salary_year_avg IS NOT NULL
AND job_work_from_home = True
GROUP BY skills
ORDER BY avg_salary DESC
LIMIT 25;
```

### 📊 **Findings:**
| Skill | Avg Salary ($) |
|------------|--------------|
| **PySpark** | 208,172 |
| **Bitbucket** | 189,155 |
| **Couchbase** | 160,515 |
| **Watson** | 160,515 |
| **DataRobot** | 155,486 |

🔹 **Big Data & ML Skills** like PySpark, Pandas, and DataRobot offer high salaries  
🔹 **Cloud & DevOps Skills** like Elasticsearch, Kubernetes, and Airflow are highly paid 💰

---
## 🎯 Key Takeaways
✅ **SQL is the most demanded skill** in the job market.  
✅ **Python and Tableau are essential** for career growth.  
✅ **Big data, cloud computing, and machine learning skills** can significantly boost salary potential.  
✅ **The highest-paying remote job offers up to $650,000 per year!**  

## 🚀 Conclusion
This project strengthened my **SQL skills** and provided valuable insights into the **data analyst job market**. By focusing on **high-demand, high-salary skills**, job seekers can strategically position themselves for success.

🔹 Want to explore the **SQL queries**? Check out the `project_sql` folder!  
🔹 Found this helpful? ⭐ Star this repository to support my work!  

---
#### 🔗 **Connect with Me:**  
📧 Email: enes.siranli@hotmail.com  
💼 LinkedIn: https://www.linkedin.com/in/enes-siranli/?locale=en_US


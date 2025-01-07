# INTRODUCTION
Mainly focusing on data analyst roles, this project explores top-paying jobs, in-demand skills and where high demands meets high salary in data analytics

sql queries!check them out here:[ sql_project_folder](/project_sql/)
# BACKGROUND
This project was to pinpoint the top-paid and in-demand skills, and other work to find optimal jobs

#### Queries are:
1.what are top-paying analyst jobs?
2.skills required for these top-paying jobs?
3.which skills are most in-demand for data analyst?
4.which skills are asociated with higher salary?
5.what are most optimal skills to learn?
# TOOLS USED
- SQL: The backbone of my analysis, allowing me to query the database and unearth critical insights.
- PostgreSQL: The chosen database management system, ideal for handling the job posting data.
- Visual Studio Code: My go-to for database management and executing
SOL queries.
- Git & GitHub: Essential for version control and sharing my SOL scripts and analysis, ensuring collaboration and project tracking.
# ANALYSIS
The approach i used is :
### For top Pyaing jobs:
To identify the highest-paying roles, I filtered data analyst positions by average yearly salary and location, focusing on remote jobs. This query highlights the high paying opportunities in the field.
```sql
SELECT	
	job_id,
	job_title,
	job_location,
	job_schedule_type,
	salary_year_avg,
	job_posted_date,
    name AS company_name
FROM
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'Anywhere' AND 
    salary_year_avg IS NOT NULL
ORDER BY
    salary_year_avg DESC
LIMIT 10;
```
Here's the breakdown of the top data analyst jobs in 2023:
- *Wide Salary Range:* Top 10 paying data analyst roles span from $184,000 to $650,000, indicating significant salary potential in the field.
- *Diverse Employers:* Companies like SmartAsset, Meta, and AT&T are among those offering high salaries, showing a broad interest across different industries.

### In-demand skills for data analyst:
This query helped to identify the skills most freuently requested in job postings,directing focus to areas with high demand
```sql
SELECT 
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' 
    AND job_work_from_home = True 
GROUP BY
    skills
ORDER BY
    demand_count DESC
LIMIT 5;
```
Here's the breakdown of the most demanded skills for data analysts in 2023

• SQL and Excel remain fundamental, emphasizing the need for strong foundational skills in data processing and spreadsheet manipulation.

• Programming and Visualization Tools like Python, Tableau, and Power BI are essential, pointing towards the increasing importance of technical skills in data storytelling and decision support.

#### top five skills are;
- SQL      = 72961,
- EXCEL    = 4611,
- PYTHON   = 4330,
- TABLEAU  = 3745,
- POWER BI = 2699

### TOP 5 SKILLS WITH HIGH PAY ARE;
- pyspark with $208172
- bitbucket with $189155
- couchbase with $160515
- watson with $160515
- datarobot with $155486

```SQL
SELECT 
    skills,
    ROUND(AVG(salary_year_avg), 0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
    AND salary_year_avg IS NOT NULL
    AND job_work_from_home = True 
GROUP BY
    skills
ORDER BY
    avg_salary DESC
LIMIT 5;
```

# LEARNED OUTCOME
My SQL Journey:

- Complex Queries: I learned how to write advanced SQL queries, combining tables and using WITH clauses to create temporary tables easily.

- Data Aggregation: I practiced using GROUP BY and aggregate functions like COUNT() and AVG() to summarize data.

- Analytical Skills: I improved my problem-solving skills by creating SQL queries that answer real-world questions.

# CONCLUSIONS
This project enhanced my SQL skills and provided valuable insights into the data analyst job market. The findings from the analysis serve as a guide to prioritizing skill development and job search efforts. Aspiring data analysts can better position themselves in a competitive job market by focusing on high-demand, high-salary skills. This exploration highlights the importance of continuous learning and adaptation to emerging trends in the field of data analyticsI
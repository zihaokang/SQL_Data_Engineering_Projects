# Exploratory Data Analysis w/ SQL: Job Market Analytics

![Project 1 Overview](../Project%20images/1_1_Project1_EDA.png)

A SQL project analyzing the data engineer job market using real world job posting data. It demonstrates my ability to **write production-quality analytical SQL, design efficient queries, and turn business questions into data-driven insights.**

## Executive Summary

**Project scope:** Built analytical SQL queries to evaluate trends in the data engineer job market.\
**Data modeling:** Joined fact and dimension tables to create a unified analytical dataset.\
**Analytics:** Applied aggregations, filtering, and sorting to identify top skills by demand, salary, and combined value.\
**Outcomes:** Highlighted dominant skills (SQL, Python), cloud technology trends, and salary distribution patterns.

If you only have a minute, review these:
1. [`top_demanded_skills.sql`](./01_top_demanded_skills.sql) - demand analysis with multi-table joins
2. [`top_paying_skills.sql`](./02_top_paying_skills.sql) - salary analysis with aggregations

## Problem & Context

Job market analysts need to answer questions like:

- Which skills are most in-demand for data engineers?
- Which skills command the highest salaries?
- What is the optimal skill set balancing demand and compensation?

This project analyzes a data warehouse built using a star schema design. The warehouse structure consists of the following:

![Data Warehouse](../Project%20images/1_2_Data_Warehouse.png)

`job_postings_fact` - Central table containing job posting details (job titles, locations, salaries, dates, etc.)
`company_dim` - Company information linked to job postings\
`skills_dim` - Skills catalog with skill names and types\
`skills_job_dim` - Resolves the many-to-many relationship between job postings and skills

By querying across these interconnected tables, I extracted insights about skill demand, salary patterns, and optimal skill combinations for data engineering roles.

## Tech Stack
**Query engine:**
DuckDB for local analytical queries and MotherDuck for cloud execution when needed\
**Language:** SQL (ANSI-style with analytical functions)\
**Data modeling:** Star schema with fact, dimension, and bridge tables\
**Development environment:** VS Code with integrated terminal for running DuckDB CLI\
**Version control:** Git and GitHub for versioned SQL scripts and project tracking

## Repository Structure
```
1_EDA/
├── 01_top_demanded_skills.sql    # Demand analysis query
├── 02_top_paying_skills.sql      # Salary analysis query
├── 03_optimal_skills.sql         # Combined demand/salary optimization
└── README.md                     # You are here
```
## Analysis Overview
###  Query Structure
[Top Demanded Skills](./01_top_demanded_skills.sql) – Identifies the 10 most in-demand skills for remote data engineer positions\
[Top Paying Skills](./02_top_paying_skills.sql) – Analyzes the 25 highest-paying skills with salary and demand metrics\
[Optimal Skills](./03_optimal_skills.sql) – Calculates an optimal score using natural log of demand combined with median salary to identify the most valuable skills to learn

### Key Insights:
- Core languages: SQL and Python each appear in ~29,000 job postings, making them the most demanded skills
- Cloud platforms: AWS and Azure are critical for modern data engineering roles-
- Infra & tooling: Kubernetes, Docker, and Terraform are associated with premium salaries
- Big data tools: Apache Spark shows strong demand with competitive compensation

## SQL Skills Demostrated
### Query Design & Optimization
- **Complex Joins** - Multi-table `INNER JOIN` operations across job_postings_fact, skills_job_dim, and skills_dim
- **Aggregations** - `COUNT()`, `MEDIAN()`, `ROUND()` for statistical analysis
- **Filtering:** - Boolean logic with `WHERE` clauses and multiple conditions (job_title_short, job_work_from_home, salary_year_avg `IS NOT NULL`)
- **Sorting & Limiting** - ORDER BY with DESC and LIMIT for top-N analysis
### Data Analysis Techniques
- **Grouping** - `GROUP BY` for categorical analysis by skill
- **Mathematical Functions** - `LN()` for natural logarithm transformation to normalize demand metrics
- **Calculated Metrics** - Derived optimal score combining log-transformed demand with median salary
- **HAVING Clause** - Filtering aggregated results (skills with >= 100 postings)
- **NULL Handling** - Proper filtering of incomplete records (salary_year_avg `IS NOT NULL`)

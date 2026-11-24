## Insurance Claims and Risk Analysis

## Project Overview
This project focuses on analysing insurance claims and employee data to understand historical claims behaviour, employee utilisation patterns and the financial exposure associated with approved insurance claims.

The project addresses a business challenge faced by insurance management: understanding rising claims costs, identifying patterns in claims utilisation, monitoring financial exposure and supporting better decision-making through data.

Using SQL in Google BigQuery and Power BI, I transformed multiple insurance datasets into analytical tables, investigated claims patterns and developed a weighted historical claims exposure scoring framework.

The final deliverable includes interactive dashboards designed to provide management with insights into claims performance, employee utilisation, regional performance and historical financial exposure.

> **Important:** The exposure score is an exploratory, historical claims classification framework. It is not a clinically validated health-risk model, an actuarial underwriting score or a prediction of future claims.

---

## Business Problem

Insurance management needs better visibility into claims behaviour and financial exposure across its covered employee population.

Key concerns include:

- Increasing insurance claims expenditure.
- Differences in claims utilisation among employees.
- Identifying employees and groups associated with higher historical claims costs.
- Understanding claims approval, pending and rejection patterns.
- Monitoring regional and company-level claims performance.
- Supporting evidence-based decisions through reliable reporting.

The objective was to use historical insurance data to uncover meaningful patterns and develop an analytical reporting solution that could support these decisions.

---

## Project Objectives

1. Analyse historical insurance claims and employee information.
2. Investigate claims frequency, approval rates and financial exposure.
3. Identify patterns across employee demographics and employment characteristics.
4. Examine claims utilisation across companies and regions.
5. Develop a historical claims exposure classification framework.
6. Build interactive Power BI dashboards for management reporting.

---

## Dataset Overview

The project used multiple relational datasets stored in Google BigQuery.

Key datasets included:

- Claims
- Covered Employees
- Companies
- Branches
- Insurance
- Beneficiaries
- Claim Workflow
- Premium Payments

### Dataset Summary

| Metric | Value |
|---|---:|
| Covered employees | 1,974 |
| Total recorded claims | 2,500 |
| Approved claims | 1,736 |
| Pending claims | 508 |
| Rejected claims | 256 |
| Total approved claim amount | GHS 47,248,039 |

The claims records cover January 2024 to December 2025, while recorded premium payments cover February 2024 to June 2026.

**Data limitation:** The claims and premium records cover different periods. Therefore, comparisons between approved claims and recorded premiums should be interpreted as historical comparisons, not as a definitive insurance loss ratio or profitability measure.

---

## Tools and Technologies

| Tool | Application |
|---|---|
| Google BigQuery | Data storage, transformation and SQL analysis |
| SQL | Data exploration, joins, aggregations, analytical queries and table creation |
| Power BI | Interactive dashboards, KPI reporting and data visualisation |
| Excel | Initial dataset review and preparation |
| Python / Pandas | Dataset cleaning and preparation |

---

## Data Preparation and Transformation

The project involved working with multiple insurance datasets and preparing them for analysis.

Key activities included:

- Reviewing source tables and understanding their structures.
- Cleaning and preparing datasets for analysis.
- Examining relationships between claims, covered employees, companies and branches.
- Using SQL joins to combine relevant datasets.
- Aggregating claims information at employee level.
- Creating reusable analytical tables in BigQuery.
- Validating record counts, unique employee IDs and financial totals.

### Analytical Tables Created

**1. employee_risk_analysis**

An employee-level analytical table containing employee characteristics and aggregated claims information, including:

- Total submitted claims.
- Approved claims.
- Pending claims.
- Rejected claims.
- Total approved claim amount.
- Average claim amount.

**2. employee_risk_scored**

An extended employee-level table containing frequency categories, cost exposure categories, scoring points, historical exposure scores and final classifications.

**3. risk_exposure_summary**

A management-level summary table containing employee counts, exposure classifications, claims statistics and approved claim amounts.

---

## Exploratory Data Analysis

I investigated several factors that could help explain differences in historical claims utilisation and financial exposure.

### 1. Age Analysis

Employees were grouped into age categories:

- 18–29
- 30–39
- 40–49
- 50–59

The 50–59 age group recorded the highest average approved claim amount per employee, at approximately GHS 25,950.76.

This indicated differences in historical claims expenditure across age groups.

### 2. Smoking Status Analysis

A comparison of smokers and non-smokers showed that non-smokers had slightly higher average approved claim amounts per employee in this dataset.

This demonstrated the importance of investigating actual data rather than assuming that a particular characteristic necessarily corresponds to higher claims costs.

### 3. Gender Analysis

Historical claims frequency and average approved claim amounts were relatively similar between male and female employees.

Gender was therefore excluded from the individual exposure scoring framework.

### 4. Occupation Analysis

Claims utilisation and average approved claim amounts varied across occupational groups.

The findings highlighted differences in historical claims experience, although these differences do not establish that occupation causes higher claims expenditure.

### 5. Salary and Grade-Level Analysis

Employees were compared across salary bands and grade levels.

The results showed some differences in historical claims expenditure, but no sufficiently established basis for automatically assigning individual exposure penalties based on salary or grade.

### 6. Claims Frequency Analysis

Employee claims frequency was examined to understand how repeated claims activity related to approved claims and financial exposure.

The analysis showed that employees with higher submitted claims frequency generally had higher average approved claim amounts.

However, claims severity did not increase consistently with frequency.

### 7. Claims Status Analysis

The claims dataset contained three main statuses:

| Status | Number of claims | Percentage |
|---|---:|---:|
| Approved | 1,736 | 69.44% |
| Pending | 508 | 20.32% |
| Rejected | 256 | 10.24% |
| **Total** | **2,500** | **100%** |

The analysis also investigated approval and rejection patterns across submitted claims frequency categories.

No strong evidence was found that employees submitting more claims consistently experienced higher rejection rates.

---

## Historical Claims Exposure Scoring Framework

One of the major deliverables was developing an employee-level historical claims exposure classification framework.

The objective was to combine two dimensions:

1. **Submitted Claim Frequency:** Measures how frequently an employee submitted claims.
2. **Approved Claim Cost Exposure:** Measures the total historical financial amount of approved claims associated with an employee.

### Step 1: Claim Frequency Classification

Employees were classified according to their total submitted claims.

| Category | Number of submitted claims |
|---|---:|
| No Claims | 0 |
| Low | 1 |
| Moderate | 2 |
| High | 3 |
| Very High | 4 or more |

### Step 2: Cost Exposure Classification

Percentiles were calculated among employees with positive approved claim amounts.

The resulting thresholds were:

| Category | Total approved claim amount |
|---|---:|
| No Approved Claims | GHS 0 |
| Lower Exposure | GHS 1–12,619 |
| Moderate Exposure | Above GHS 12,619–27,021 |
| High Exposure | Above GHS 27,021–58,107 |
| Very High Exposure | Above GHS 58,107 |

### Step 3: Scoring Points

Each category was assigned points on a scale of 0–100.

**Claim Frequency Points**

| Category | Points |
|---|---:|
| No Claims | 0 |
| Low | 25 |
| Moderate | 50 |
| High | 75 |
| Very High | 100 |

**Cost Exposure Points**

| Category | Points |
|---|---:|
| No Approved Claims | 0 |
| Lower Exposure | 25 |
| Moderate Exposure | 50 |
| High Exposure | 75 |
| Very High Exposure | 100 |

### Step 4: Weighted Historical Exposure Score

The model assigned:

- 60% weight to approved claim cost exposure.
- 40% weight to submitted claim frequency.

The scoring formula was:

`Historical Exposure Score = (Cost Exposure Points × 0.60) + (Frequency Points × 0.40)`

These weights were selected as initial modelling assumptions based on the project's focus on historical financial exposure. They were not statistically learned or independently validated.

### Step 5: Final Classification

| Score | Classification |
|---|---|
| 0–19 | Very Low |
| 20–39 | Low |
| 40–59 | Moderate |
| 60–79 | High |
| 80–100 | Very High |

### Scoring Results

The framework classified all 1,974 employees.

| Classification | Employees | Percentage |
|---|---:|---:|
| Very Low | 773 | 39.16% |
| Low | 322 | 16.31% |
| Moderate | 364 | 18.44% |
| High | 268 | 13.58% |
| Very High | 247 | 12.51% |
| **Total** | **1,974** | **100%** |

---

## Key Business Insights

### 1. Concentration of Approved Claims Expenditure

The 247 employees classified as Very High exposure accounted for GHS 24,080,576 in approved claims expenditure.

This represented approximately 50.96% of the total approved claims amount.

This finding highlights the concentration of historical claims expenditure within a relatively small employee group.

### 2. Differences in Historical Claims Utilisation

Average approved claims per employee increased across the exposure categories:

| Classification | Average approved claims |
|---|---:|
| Very Low | 0.00 |
| Low | 0.86 |
| Moderate | 1.15 |
| High | 1.69 |
| Very High | 2.38 |

### 3. Higher Historical Financial Exposure

Average approved claim amounts per employee increased across the categories:

| Classification | Average approved claim amount |
|---|---:|
| Very Low | GHS 0 |
| Low | GHS 5,915.24 |
| Moderate | GHS 23,430.91 |
| High | GHS 47,514.57 |
| Very High | GHS 97,492.21 |

### 4. Frequency and Cost Exposure Provide Different Insights

Some employees submitted multiple claims without having approved claims, while others had very high approved claim amounts despite submitting relatively few claims.

This reinforced the importance of considering claim frequency and approved claim cost as separate dimensions.

---

## Power BI Dashboard Development

Four analytical dashboard areas were developed, with a dedicated historical exposure dashboard added to the project.

### 1. Executive Overview

Provides a high-level summary of insurance performance using key performance indicators and management visuals.

### 2. Employee Risk and Utilisation

Explores employee characteristics and historical claims utilisation across demographic and employment groups.

### 3. Claims Analysis and Trends

Examines claims volumes, statuses, approved claim amounts and historical claims trends.

### 4. Regional Performance Analysis

Provides insights into claims performance across regions and companies.

### 5. Historical Claims Exposure

Visualises:

- Employee distribution by exposure classification.
- Total approved claims amount by exposure classification.
- Average historical exposure score by classification.
- Average approved claims per employee.
- Employee distribution by claim frequency and cost exposure.

---

## Limitations and Future Improvements

This project provides a historical view of claims behaviour and financial exposure. Several improvements would strengthen the framework.

### Limitations

- The scoring weights are initial assumptions rather than statistically optimised parameters.
- The framework uses historical claims information and does not predict future medical claims.
- Claims and premium records cover different periods, limiting direct financial comparisons.
- Some employee categories contain relatively small populations.
- The analysis does not establish causal relationships between employee characteristics and claims expenditure.

### Future Improvements

- Conduct sensitivity analysis to examine how alternative scoring weights affect employee classifications.
- Test the scoring framework against a separate future claims period to evaluate predictive performance.
- Develop more detailed claims severity and frequency analysis.
- Investigate regional and company-level drivers of claims expenditure.
- Improve premium and claims period alignment for more meaningful financial performance analysis.
- Introduce automated data refresh and reporting pipelines.
- Explore statistical models for forecasting claims expenditure, subject to appropriate validation and responsible use.

---

## Conclusion

This project demonstrates how SQL, cloud data warehousing and business intelligence tools can be combined to solve a practical insurance analytics problem.

By transforming multiple datasets into reusable analytical tables, investigating historical claims behaviour and developing an employee-level historical exposure classification framework, I created a reporting solution that helps management understand claims utilisation and the concentration of historical financial exposure.

The project strengthened my practical experience in SQL, BigQuery, data transformation, exploratory data analysis, analytical modelling and Power BI dashboard development.

---

## Irene Ampiaw

**Data Analyst Portfolio Project**

**Tools:** SQL | Google BigQuery | Power BI | Excel | Python


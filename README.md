## Insurance Claims & Risk Analysis

Tools: Python · Pandas · SQL · Google BigQuery · Power BI · DAX

Project Overview

How can an insurance provider use claims and premium data to better understand financial exposure, identify patterns in healthcare utilization, and make more informed business decisions?

This project explores that question using healthcare insurance data covering employees of corporate organizations.

The goal is to analyze claims, examine potential risk factors, compare approved claim costs with recorded premium payments, and develop an interactive Power BI dashboard that makes the findings easier to understand.

The project follows an end-to-end analytics workflow, from data cleaning and database exploration to SQL analysis, data visualization, and business recommendations.

Business Problem

Insurance providers need to understand not only how much they pay in claims, but also which factors contribute to claim costs, how healthcare utilization varies across employees, and whether recorded premium payments appear sufficient relative to recorded claims.

This analysis investigates several questions:

- How does claim frequency and cost vary across employee age groups?
- Do employees with frequent claims have higher claim costs per employee?
- How do approved claim amounts compare with recorded paid premiums across companies?
- Which companies account for the largest share of approved claim costs?
- What patterns in claims data could support future risk assessment and financial planning?

Project Objectives

1. Prepare and validate insurance datasets for analysis.
2. Explore the database structure and relationships between tables.
3. Use SQL to investigate insurance risk assumptions and business questions.
4. Build reusable measures and interactive visuals in Power BI.
5. Communicate findings, limitations, and potential business implications.
6. Establish a foundation for a future custom insurance Risk Score model.

Tools and Technologies

| Tool | Purpose |
|---|---|
| Python | Data preparation and cleaning |
| Pandas | Data manipulation and validation |
| SQL | Data exploration, joins, aggregations, and risk analysis |
| Google BigQuery | Cloud data storage and SQL analysis |
| Power BI Desktop | Interactive dashboard development |
| DAX | Measures and calculations for dashboard KPIs |
| GitHub | Project documentation and portfolio presentation |

Dataset and Database Structure

The project uses eight related tables:

- `beneficiaries`
- `claim_workflow`
- `claims`
- `companies`
- `covered_employees`
- `insurance`
- `branch`
- `premium_payments`

The tables contain information related to employees, companies, branches, insurance claims, beneficiaries, and premium payments.

The database relationships were explored and documented using an entity relationship diagram (ERD). The data was loaded into Google BigQuery for SQL-based analysis.

- Data Preparation

Python and Pandas were used to prepare the datasets for analysis.

Key activities included:

- Reviewing the structure and quality of the source files.
- Cleaning data and addressing inconsistencies.
- Investigating name and gender inconsistencies.
- Creating validation flags, including gender mismatch indicators.
- Reviewing table relationships and preparing the data for loading into BigQuery.

- Data quality checks were important because inconsistencies can affect the reliability of downstream analysis.

- Analytical Approach

SQL was used to explore the data, calculate key metrics, and investigate business assumptions.

1. Age and Healthcare Utilization

Business question: Do older employees require more medical attention?

Employees were grouped into age bands and compared using claim counts, claims per employee, claim amounts, and approval rates.

Finding: Claims per employee increased slightly across the analyzed age groups, from approximately 1.43 among employees aged 18–29 to 1.48 among employees aged 40–49 and 50–59.

The results suggest differences in healthcare utilization across age groups, but they do not establish that age alone causes higher medical costs.

2. Frequent Claimants and Financial Exposure

Business question: Do employees with frequent claims represent higher insurance exposure?

Employees were grouped according to their number of claims:

- Low utilization: 1–2 claims
- Moderate utilization: 3–4 claims
- High utilization: 5–6 claims

The analysis compared employee counts, claim frequency, total claim costs, average claim amounts, and claim cost per employee.

Finding: The high-utilization group had the highest claim cost per employee, at approximately GHS 122,963. However, it contained only 13 employees. Its average claim amount was lower than that of the low- and moderate-utilization groups.

This suggests that higher cumulative costs may be associated with repeated claims rather than greater cost per individual claim. The small high-utilization group should be interpreted cautiously.

3. Corporate Claims and Recorded Premium Payments

Business question: How do approved claim costs compare with recorded paid premiums across companies?

Claims and premium payments were aggregated separately before being compared to reduce the risk of double-counting caused by joins across related tables.

The analysis examined:

- Total approved claim amounts by company.
- Recorded paid premiums by company.
- Approved claims compared with recorded paid premiums.
- Claim-to-recorded-premium ratios.

The dataset contained approximately GHS 47.25 million in approved claims and GHS 5.60 million in recorded paid premiums for the respective analysis periods.

Finding: Recorded approved claims exceeded recorded paid premiums for every company analyzed.

This indicates a potential financial exposure that deserves further investigation. However, these ratios are not definitive insurance loss ratios because policy coverage periods, earned premiums, and complete premium obligations were not available for verification.

- Power BI Dashboard

Power BI Desktop was connected to BigQuery, and relationships between the tables were configured to support analysis across the dataset.

The Executive Overview page is being developed to summarize key metrics and claim patterns.

Key Performance Indicators

The dashboard includes or is being developed to include:

- Total claims.
- Number of approved claims.
- Total approved claim amount.
- Average approved claim amount.
- Claim approval rate.
- Recorded paid premiums.
- Total covered employees.
- Pending and denied claims, where supported by the source status values.

Visualizations

The Executive Overview includes existing charts and a monthly approved-claim trend. Additional dashboard components support analysis of:

- Approved claim amounts by company.
- Claim patterns by claim type.
- Claim activity over time.
- Company-level financial exposure and claim costs.

Date filtering is being configured using a dedicated date table to support exploration by year, month, and date range.

Further dashboard development will focus on employee risk and utilization, corporate financial risk, and claims operations where the available data supports reliable analysis.

Key Findings

The analysis has produced several preliminary findings:

1. Claim frequency per employee varies modestly across age groups.
2. Employees with frequent claims can have higher cumulative claim costs per employee.
3. The small high-utilization group requires careful interpretation because of its limited size.
4. Recorded approved claim costs exceed recorded paid premiums across the companies analyzed.
5. Data limitations must be addressed before drawing definitive conclusions about profitability or insurance loss ratios.

These findings can inform further investigation, but they should not be treated as causal conclusions or final underwriting decisions.

Data Limitations

Several limitations affect interpretation:

- The available data does not fully establish policy coverage periods or earned premiums.
- Recorded premium payments may not represent all premium obligations for the corresponding claims period.
- Approval status does not necessarily indicate that a claim has been paid.
- The high-utilization employee group is relatively small.
- Observed differences across demographic groups do not establish causation.
- Additional validation is needed before using the analysis to make individual-level insurance decisions.

These limitations are documented to ensure that the findings are interpreted responsibly.

Project Status and Next Steps

This project is being developed iteratively.

Completed work includes data preparation, exploration of the eight-table database, loading data into BigQuery, SQL-based risk analyses, and initial Power BI dashboard development.

Planned next steps include:

- Complete and validate the Executive Overview dashboard.
- Develop the Employee Risk & Utilization dashboard page.
- Expand corporate financial risk and claims operations analysis.
- Develop and validate a transparent custom Risk Score model.
- Prepare an executive summary with actionable recommendations.
- Publish the finalized project artifacts and dashboard screenshots on GitHub.

Skills Demonstrated

- Data cleaning and validation using Python and Pandas.
- Relational database exploration and data modeling.
- SQL joins, aggregations, conditional logic, and analytical queries.
- Cloud data analysis using Google BigQuery.
- DAX measures and KPI development.
- Power BI dashboard design and date filtering.
- Business problem formulation and risk analysis.
- Communicating findings with appropriate limitations.


- Next Steps:
Develop a custom Risk Score model: Define transparent risk indicators and scoring rules, then evaluate whether the resulting scores meaningfully distinguish different levels of claim utilization and financial exposure.

Prepare an executive report: Summarize the main findings, business implications, data limitations, and recommendations for insurance management.

Update the Published portfolio project: Re-organize the SQL scripts, data-cleaning notebook, database relationship diagram, dashboard screenshots, and documentation in a GitHub repository.

Prepare a project presentation: Develop a concise walkthrough explaining the business problem, analytical approach, key findings, and lessons learned.

Conclusion

This project demonstrates how insurance data can be transformed into business insights through a structured analytics workflow.

By combining Python, SQL, BigQuery, and Power BI, the project investigates healthcare utilization, claim frequency, and corporate financial exposure while highlighting the importance of data quality and sound interpretation.

The longer-term objective is to build on these findings to develop a transparent risk assessment framework that can support insurance analysis and decision-making.


Project type: Data Analytics / Business Intelligence

Author: Data Analyst

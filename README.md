# Northloop Attrition Data

Used Python to clean a dataset for readability and analysis. Used SPSS to craft a model that predicts employees who are most likely to make a voluntary departure in the next three months.

## The Business Problem

Northloop Software, a publicly traded software company that sells workflow automation software, is having employees voluntarily depart the company quicker than they can replace them. 

The Chief People Officer (CPO) is asking the People Analytics team to create a model that flags employees were are most likely to leave voluntarily in the next three months. HR Business Partners (HRBP) has the bandwidth to have 40 proactive retention conversations with employees each month.

## Data Characteristics

- **Size:** ~15,000 rows and 16 columns, 900 unique employees
- **Grain:** One row per employee per month, from January 2024 to December 2026
- **Target Variable:** Voluntary_Exit_Next_3_Months

## Variables

- **Employee_ID:** Unique employee identifier. Repeats once per month. Type: Text.
- **Snapshot_Date:** First day of the month the snapshot was taken. Type: Date.
- **Region:** Sales region: AMS (Americas), EMEA, APJ (Asia Pacific & Japan). Type: Category.
- **Department:** Enterprise Sales, Commercial, or Customer Success. Type: Category
- **Job_Level:** Job level from 3 (early career) to 7 (senior). Type: Ordinal.
- **Work_Arrangement:** Remote, Hybrid, or Onsite. Type: Category.
- **Hire_Source:** External, Referral, or Internal Transfer. Type: Category.
- **Tenure_Months:** Months since hire. Type: Integer.
- **Months_Since_Last_Move:** Months since hire, last promotion, or last role change, whichever is most recent. Type: Integer.
- **Manager_Changes_Last_12M:** Number of times the employee's manager changed in the past 12 months. Type: Integer.
- **Team_Size:** Active headcount on the employee's team at the snapshot date. Type: Integer.
- **Team_Voluntary_Exits_Last_6M:** Voluntary exits from the same team in the 6 months before the snapshot. Type: Integer.
- **Territory_Change_Last_6M:** 1 if the employee's territory or account book was reassigned in the past 6 months. Type: 0/1.
- **Sales_Quota_Attainment_Last_Qtr:** Quote attainment for the last completed quota (1.0 = 100%). Comes from the Sales Ops system. Not applicable to Customer Success or reps still ramping. Type: Decimal.
- **Has_Given_Notice:** 1 if the employee has submitted a resignation notice in the HRIS. Type: 0/1.
- **Voluntary_Exit_Next_3_Months:** **Target.** 1 if the employee voluntarily left within 3 months of the snapshot date. Involuntary exits are 0. Type: 0/1.

## Issues with the Data

- **Accuracy is misleading:** The first model showed 93% accuracy. However, 8% of the records show an upcoming exit.
- **Data is not consistent:** The data comes from two separate systems: HRIS (employee and org data) and Sales Operations (quota attainment). The HRIS was replaced during the period, and code and format changes were not documented.
- **Fields are not always up to date:** Voluntary leaves are noted before the employee's final day.
- **The data is repetitive:** Because each employee repeats every month, the data may need to be split into training and test data.
- **Scores don't give enough information:** HRBPs need to identify specific groups and employees rather than just having a score.

## Hypotheses to Test

- **H1: Stagnation:** Employees who have gone a long period of time without a promotion are more likely to leave.
- **H2: Mid-Tenure Slump:** Attrition risk is not linear with tenure. Rather, it peaks mid-tenure (18-30 months) before major equity vests.

## The Assignment

- **Prepare the data:** Clean up data file using Python.
- **Test H1 and H2:** Use a model-based test to reject or accept each null hypothesis.
- **Build and evaluate a model:** Compare against the 93% "everyone stays" model. Evaluate precision and recall, choose a train/test split, and pick a reasonable threshold that Northloop can use the utilize the 40 proactive conversations that HRBPs can use per month.

# Step 1: Clean the data using Python


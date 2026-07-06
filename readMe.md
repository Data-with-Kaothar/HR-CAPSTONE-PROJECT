# HR Employee Data Cleaning & Analysis

## Project Objective

The objective of this project was to clean, transform, and prepare an HR employee dataset for analysis using Microsoft Excel. The cleaned dataset was then used to perform exploratory analysis, answer key business questions using Pivot Tables, and develop an HR analytics dashboard that provides insights into workforce composition, employee performance, compensation, attrition, and hiring trends.

## Tools & Techniques Used

### Software

* Microsoft Excel

### Excel Features

* Pivot Tables
* Pivot Charts
* Find & Replace
* Text to Columns
* Cell Formatting

### Excel Functions

* XLOOKUP
* TEXTJOIN
* YEARFRAC
* INT
* IFS
* SUMIF
* COUNTIF
* VALUE
* TRIM
* TODAY

### Data Cleaning Techniques

* Duplicate removal
* Missing value imputation using department averages
* Data type conversion
* Text standardization
* Date standardization
* Lookup table integration
* Feature engineering (creation of new calculated columns)

## Overview

The dataset was assessed for data quality issues, cleaned, standardized, and enriched with additional calculated fields to improve consistency, accuracy, and analytical value before analysis and dashboard creation.

## Initial Data Exploration

During the initial exploration of the dataset, several data quality issues were identified:

* Duplicate records.
* Missing values in key fields such as Salary and Performance Score.
* Inconsistent data types across multiple columns.
* Inconsistent text formatting and spelling in categorical fields.
* Invalid date values that were stored as text.
* Missing department names, where only department codes were provided.

These issues were addressed before performing any analysis to ensure reliable and accurate results.

## Data Cleaning Process

### 1. Removed Duplicate Records

Duplicate records were identified and removed to ensure that each employee was represented only once in the dataset.

### 2. Corrected Data Types and Formatting

The appropriate data types were assigned to each column:

* **First Name**, **Last Name**, and **Employment Status** were formatted as text.
* **Salary** was formatted as currency.
* **Hire Date** was formatted as a Short Date using the **Day/Month/Year (D/M/Y)** format.

While formatting the Hire Date column, some dates remained left-aligned, indicating that Excel had stored them as text rather than dates. The **Text to Columns** feature was used to convert these text values into valid date values before applying the desired date format.

### 3. Standardized Text Values

Several text columns contained inconsistent formatting and spelling.

#### Department Code

* Extra spaces were removed using the **TRIM** function.
* Inconsistent department codes were standardized using **Find and Replace** to ensure consistent capitalization and naming.

#### Employment Status

* Leading and trailing spaces were removed using **TRIM**.
* Variations and spelling inconsistencies were corrected using **Find and Replace**, resulting in three standardized values:

  * Active
  * Left
  * Resigned

### 4. Handled Missing Values

Rather than replacing missing numeric values with the overall dataset average, department-level averages were used to preserve departmental salary and performance patterns.

#### Salary

* A helper table was created using **SUMIF** and **COUNTIF** to calculate the average salary for each department.
* Missing salary values were replaced with the corresponding departmental average.
* The **VALUE(TRIM())** function was then used to remove unwanted spaces and convert salary values into numeric format where necessary.

#### Performance Score

* A similar helper table was created using **SUMIF** and **COUNTIF** to calculate the average performance score for each department.
* Missing performance scores were replaced with the corresponding departmental average.

### 5. Created Additional Columns

Several calculated columns were added to enrich the dataset for analysis.

#### Full Name

* The **TEXTJOIN** function was used to combine the First Name and Last Name columns.
* TEXTJOIN was selected instead of CONCAT to avoid unwanted leading or trailing spaces when either name was missing.

#### Department Name

* The **XLOOKUP** function was used to retrieve the corresponding department name from the department lookup table using each employee's department code.

#### Years of Service

* The **YEARFRAC** function was used to calculate the fraction of years between each employee's hire date and the current date.
* The **INT** function was applied to return completed years of service as whole numbers.

#### Performance Band

* The **IFS** function was used to categorize employees into performance bands based on their performance scores.

#### Projected Bonus

* A lookup table containing the bonus percentage assigned to each performance band was referenced using the **XLOOKUP** function.
* The projected bonus for each employee was then calculated by multiplying the employee's salary by the corresponding performance bonus percentage.

## Analysis

Pivot Tables were created on a separate **Analysis** worksheet to answer the following business questions:

* Total headcount and average salary by department.
* Attrition rate by department.
* Average performance score by employment status.
* Total projected bonus payout by performance band.

The attrition rate was calculated by displaying employee counts as the **percentage of the parent row total**, allowing the proportion of employees who had left each department to be determined.

## Assumptions and Transformations

* Missing Salary and Performance Score values were replaced using departmental averages rather than the overall dataset average, assuming employees within the same department have similar compensation and performance characteristics.
* TEXTJOIN was used instead of CONCAT to ensure clean full names even when one of the name fields was blank.
* Years of service were reported as completed whole years rather than fractional years.

## Challenges Encountered

Several Hire Date values were stored as text and could not be formatted using standard date formatting. This issue was identified by their left alignment in Excel and was resolved using the **Text to Columns** feature to convert them into valid date values before formatting.

Another challenge involved converting salary values into usable numeric values after removing unnecessary spaces. This was resolved using the **VALUE(TRIM())** function, which simultaneously cleaned the text and converted it into numeric data suitable for calculations.

Following the completion of the cleaning process, the dataset was consistent, complete, and ready for exploratory analysis and dashboard development.

## Key Insights

* The Marketing Department recorded the highest average performance score among all departments, indicating consistently strong employee performance.
* The Information Technology (IT) Department experienced the highest attrition rate, suggesting a greater proportion of employees left the department compared to others.
* Employees with a Resigned employment status had a higher average performance score than those who remained Active, indicating that some high-performing employees left the organization.
* Employees in the Achieving performance band accounted for the highest projected bonus payout, reflecting the concentration of employees and bonus allocation within this performance category.
* Employee hiring reached its peak in 2017 before declining in subsequent years, while 2013 recorded the lowest number of hires during the period under review. 

## Recommendations

* Investigate the factors contributing to high attrition in departments with above-average turnover.
* Review compensation and performance management strategies where appropriate.
* Develop targeted retention initiatives for high-performing employees.
* Use hiring trends to support future workforce planning and budgeting.
* Investigate why strong-performing employees are resigning to avoid brain loss.
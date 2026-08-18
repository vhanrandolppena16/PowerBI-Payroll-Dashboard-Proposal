# Payroll Analytics Dashboard

A **payroll analytics and business intelligence project** that demonstrates how sensitive payroll data can be sanitized and transformed for portfolio, demonstration, and proof-of-concept purposes while retaining its analytical structure.

The project combines **Python-based data masking and preparation** with an interactive **Power BI payroll dashboard** for analyzing compensation, payroll trends, employee headcount, organizational structure, and payroll contributions.

> **Important:** The dataset used in this repository is a masked/sanitized representation prepared for demonstration purposes. It is not intended to expose or reproduce confidential payroll information.

---

## Project Overview

Payroll datasets often contain highly sensitive information, including employee identities, bank account details, government identification numbers, compensation, taxes, deductions, and other personal information.

This project demonstrates a workflow for preparing payroll data for analytics without exposing the original sensitive information.

The workflow consists of two major components:

1. **Data Masking & Preparation using Python**
2. **Payroll Analytics Dashboard using Power BI**

The resulting dataset preserves important relationships and analytical categories such as employee classification, departments, cost centers, designations, payroll periods, compensation components, deductions, taxes, and contributions.

This allows the sanitized dataset to remain useful for demonstrating business intelligence and payroll analytics capabilities.

---

## Project Workflow

```text
Original Payroll Dataset
          │
          ▼
   Python / Pandas
          │
          ▼
Sensitive Data Removal
          │
          ├── Remove government IDs
          ├── Remove bank account information
          ├── Mask employee IDs
          ├── Generate synthetic employee names
          ├── Mask departments
          ├── Mask cost centers
          ├── Mask group identifiers
          ├── Mask job designations
          └── Transform monetary values
          │
          ▼
   Masked Payroll Dataset
          │
          ▼
      Power BI
          │
          ▼
Payroll Analytics Dashboard
```

---

## Key Features

### 🔐 Privacy-Preserving Data Preparation

The Python notebook sanitizes sensitive payroll information before the dataset is used for analytics.

The masking process includes:

* Removal of employee bank account information
* Removal of Tax Identification Numbers (TIN)
* Removal of SSS numbers
* Removal of Pag-IBIG numbers
* Removal of PhilHealth numbers
* Replacement of employee numbers with synthetic IDs
* Generation of synthetic employee names
* Masking of organizational identifiers
* Masking of department names
* Masking of cost center names and codes
* Masking of group identifiers
* Masking of job designations
* Transformation of payroll-related monetary values

---

### 👤 Synthetic Employee Identities

Original employee numbers are replaced with synthetic identifiers following a format such as:

```text
EMP-1000
EMP-1001
EMP-1002
...
```

Synthetic employee names are generated using the **Faker** library.

The mapping is performed consistently so that the same employee retains the same masked identity throughout the dataset.

---

### 💰 Payroll Value Masking

Payroll-related monetary fields are transformed using employee-specific random multipliers combined with record-level random noise.

The transformation follows the general approach:

```text
Masked Value
    =
Original Value
    × Employee-Specific Multiplier
    × Record-Level Noise
```

The notebook generates an employee-specific multiplier within a defined range and applies additional random variation to individual payroll records.

A fixed NumPy random seed is used so that the transformation can be reproduced when the same source data and environment are used.

This approach changes the original monetary values while preserving their numerical structure for analytical demonstrations.

---

## Power BI Dashboard

The sanitized dataset is used to create a payroll analytics dashboard in **Microsoft Power BI**.

The dashboard provides an overview of payroll performance and workforce composition across different organizational dimensions.

### Dashboard KPIs

The dashboard includes key payroll indicators such as:

* Total Salary
* Total Benefits
* Total Gross Pay
* Withholding Tax
* Employee Government Contributions
* Employer Government Contributions
* Payroll comparison against a previous period

The dashboard covers the period from **September 1, 2018 to June 30, 2024**.

---

## Payroll Analysis

The dashboard provides analysis of different payroll components, including:

* Regular Pay
* Overtime Pay
* Night Differential Pay
* Overtime/Night Differential Pay
* Undertime/Absent
* Adjustments
* Bonuses
* Allowances
* Other Earnings

These measures provide a breakdown of how total payroll expenditure is composed.

---

## Payroll Trend Analysis

A **Payroll Comparison Over Time** visualization is included to examine changes in gross payroll across different payroll periods.

Payroll periods are represented using labels such as:

```text
Apr 2019 P1
Apr 2019 P2
Apr 2020 P1
Apr 2021 P1
Apr 2021 P2
...
```

This allows payroll values to be compared across historical payroll periods.

---

## Organizational Analysis

The dashboard supports payroll analysis across multiple organizational dimensions.

### Cost Center

Gross pay and employee headcount can be analyzed by cost center.

### Department

Gross pay and headcount can also be analyzed by department.

The dashboard contains masked department categories while maintaining their usefulness for workforce segmentation.

### Designation

Payroll expenditure and headcount can be analyzed by employee designation.

---

## Workforce Analysis

The dashboard includes employee headcount analysis by:

* Employee Class
* Group ID
* Cost Center
* Department
* Designation
* Employee

Employee class categories include:

```text
Regular
Resign
Blank
```

---

## Government Contributions

The dashboard separates employee and employer government contributions.

### Employee Contributions

* SSS
* Pag-IBIG
* PhilHealth
* Other Contributions

### Employer Contributions

* SSS
* Pag-IBIG
* PhilHealth
* Other Contributions

This provides visibility into payroll-related contribution costs from both employee and employer perspectives.

---

## Employee-Level Analysis

The dashboard also provides an employee details section with filters for:

* Employee Full Name
* Employee Class
* Group ID
* Department
* Designation
* Cost Center

Employee-level records include payroll period, department, cost center, designation, regular pay, and overtime pay.

Because employee identities have been replaced with synthetic identifiers and names, this section can be demonstrated without displaying the original employee identities.

---

## Data Masking Process

The masking process can be summarized as follows:

### 1. Load Source Data

The notebook loads all worksheets from the source Excel workbook using Pandas.

```python
df = pd.read_excel(
    data_source,
    sheet_name=None
)
```

### 2. Mask Organizational Information

Mappings are used to replace:

* Cost center names
* Cost center codes
* Department names
* Group names
* Group codes
* Job designations

Using mappings ensures that identical source values receive consistent masked values.

### 3. Remove Highly Sensitive Fields

The following categories of information are removed from the payroll history dataset:

```text
Bank Account
Tax Identification Number
SSS Number
Pag-IBIG Number
PhilHealth Number
```

### 4. Generate Synthetic Employee IDs

Employee identifiers are replaced with synthetic values:

```text
EMP-1000
EMP-1001
EMP-1002
...
```

### 5. Generate Synthetic Names

Synthetic employee names are generated using Faker and associated consistently with the masked employee IDs.

### 6. Mask Monetary Values

Payroll monetary fields are transformed using:

```text
Original Value
× Employee-Specific Multiplier
× Random Record-Level Noise
```

This applies the transformation consistently while introducing variation between employees and payroll records.

### 7. Validate Relationships

The notebook validates that masked identifiers remain consistent between related tables.

For example, cost center codes in the `costcenter` and `payhisto` tables are compared after masking to ensure that their categorical relationships remain intact.

The same validation is performed for group identifiers.

### 8. Export the Sanitized Dataset

The resulting workbook contains the following worksheets:

```text
costcenter
depm
empClass
groupid
payhisto
```

---

## Repository Structure

```text
.
├── Masked Payroll Dataset.ipynb
├── Masked Payroll Dataset.xlsx
├── Masked Payroll Dashboard.pdf
└── README.md
```

> File names can be adjusted depending on how the repository is organized.

---

## Technologies Used

### Data Processing

* Python
* Pandas
* NumPy
* Faker
* OpenPyXL

### Business Intelligence

* Microsoft Power BI

### Data Format

* Microsoft Excel
* Jupyter Notebook

---

## Skills Demonstrated

This project demonstrates experience with:

* Data anonymization
* Data masking
* Privacy-preserving data preparation
* Data cleaning
* Data transformation
* Pandas
* NumPy
* Synthetic data generation
* Relational data validation
* Excel data processing
* Payroll analytics
* Business intelligence
* Power BI dashboard development
* KPI development
* Data visualization
* Workforce analytics
* Financial analytics

---

## Data Privacy & Disclaimer

The original payroll dataset contains sensitive information and is **not included in this repository**.

The data presented in this project has been prepared specifically for demonstration and portfolio purposes.

Sensitive identifiers are removed, employee identities are replaced with synthetic values, organizational identifiers are masked, and monetary values are transformed before being used for visualization.

The dashboard therefore demonstrates the **analytical structure and functionality of a payroll reporting solution**, rather than representing the original confidential payroll records.

The displayed payroll values should not be interpreted as actual current or historical compensation information.

---

## Dashboard Preview

The Power BI dashboard provides an executive-style payroll overview with KPI cards, payroll trends, organizational analysis, workforce headcount, contribution breakdowns, and employee-level filtering.

Add screenshots to this section when publishing the repository:

```markdown
![Payroll Dashboard Overview](screenshots/dashboard-overview.png)

![Payroll Cost Center Analysis](screenshots/cost-center-analysis.png)

![Payroll Department Analysis](screenshots/department-analysis.png)

![Employee Details](screenshots/employee-details.png)
```

---

## Purpose

This project was developed as a **portfolio and proof-of-concept business intelligence project** to demonstrate how sensitive payroll data can be transformed into a privacy-conscious analytical dataset while retaining enough structure for meaningful payroll and workforce reporting.

The primary objective is to demonstrate the complete workflow from:

**Sensitive Data → Data Masking → Data Validation → Business Intelligence Dashboard**

rather than simply presenting the final Power BI visualization.

---

## Author

**Vhan Randolp Pena**

Computer Engineering — Data Science

Technological Institute of the Philippines – Quezon City

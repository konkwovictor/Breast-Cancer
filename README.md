# 🎗️ Patient & Cancer Analytics Dashboard | Power BI

> **An end-to-end Power BI analytics project focused on patient demographics, cancer characteristics, treatment outcomes, survival, and recurrence patterns.**

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-5B2C83?style=for-the-badge)
![Data Analysis](https://img.shields.io/badge/Data%20Analysis-Healthcare-8E3A5D?style=for-the-badge)

---

## 📌 Project Overview

This project demonstrates how I transformed a raw patient/cancer dataset into an interactive **two-page healthcare analytics dashboard in Microsoft Power BI**.

The goal was not simply to create charts, but to build a dashboard that allows a user to move from:

**Patient Profile → Cancer Characteristics → Treatment Outcomes → Survival & Recurrence**

The dashboard is divided into two analytical views:

### 1. Patient & Cancer Profile

This page focuses on understanding the patient population and the distribution of cancer characteristics.

It answers questions such as:

- How many patients are represented in the dataset?
- How many patients survived?
- What is the average patient age?
- What is the average tumor size?
- How long do patients survive on average?
- How are patients distributed across cancer stages?
- Which cancer types appear most frequently?
- How are patients distributed by receptor status?
- Which affected breast is most represented?
- How does tumor size vary across cancer stages?

### 2. Treatment & Patient Outcomes

This page focuses on outcomes after treatment and provides a view of survival and recurrence.

It answers questions such as:

- How many patients survived versus died?
- What is the overall survival rate?
- What is the recurrence rate?
- What is the average recurrence value?
- How does survival rate change across cancer stages?
- How does survival rate differ by cancer type?
- Which cancer types have higher recurrence rates?
- How does the patient count change across months?

---

# 🎯 Project Objectives

The main objectives of this project were to:

1. Clean and prepare the raw dataset for analysis.
2. Identify relevant healthcare and patient-level metrics.
3. Create calculated columns and measures required for analysis.
4. Build an appropriate date/month structure for time-based analysis.
5. Develop KPIs that summarize the dataset at a glance.
6. Analyze cancer stage, cancer type, receptor status, and affected breast.
7. Analyze survival and recurrence outcomes.
8. Design an interactive dashboard with consistent navigation and visual hierarchy.
9. Present insights in a way that can be understood by both technical and non-technical users.
10. Demonstrate an end-to-end Power BI workflow suitable for a real-world analytics portfolio.

---

# 🗂️ Dataset

The project uses a patient/cancer dataset containing information about patients, cancer characteristics, treatment/outcome fields, and time-related information.

### Key analytical fields used

| Category | Examples |
|---|---|
| Patient Information | Patient ID, Age |
| Cancer Characteristics | Cancer Stage, Cancer Type, Tumor Size |
| Biological Characteristics | Receptor Status |
| Patient/Cancer Location | Affected Breast |
| Outcome | Survival Status |
| Survival | Survival Months |
| Recurrence | Recurrence / Recurrence-related fields |
| Time | Month / Date-related fields |

> **Note:** The dashboard is intended for analytical/portfolio purposes. The visualized relationships should not be interpreted as medical advice, clinical guidance, or causal medical conclusions.

---

# 🧹 1. Data Preparation & Cleaning

Before creating the dashboard, I first focused on understanding the structure and quality of the raw data.

## Step 1 — Imported the dataset

The dataset was imported into **Power BI** and inspected in Power Query.

The first checks included:

- Number of rows and columns
- Column names
- Data types
- Missing values
- Duplicate records
- Invalid values
- Inconsistent text values
- Numerical fields
- Date/month fields
- Categorical fields

---

## Step 2 — Checked data types

Each column was reviewed to make sure it had the appropriate data type.

Examples:

- Patient IDs → Text/whole number depending on the source
- Age → Whole number
- Tumor Size → Decimal number
- Survival Months → Decimal/whole number
- Cancer Stage → Text/category
- Cancer Type → Text/category
- Receptor Status → Text/category
- Survival Status → Text/category
- Month/Date → Date or appropriate time field

Correct data types are important because Power BI uses them when calculating measures, building relationships, filtering, and creating visualizations.

---

## Step 3 — Checked for missing values

I reviewed the dataset for blanks and null values.

The purpose was to determine whether missing values:

- Could be safely removed
- Needed replacement
- Represented a meaningful category
- Could affect KPI calculations

Rather than blindly deleting missing records, the cleaning process considered how each field would be used during analysis.

---

## Step 4 — Standardized categorical values

Categorical columns were reviewed for inconsistent spelling, spacing, capitalization, and naming.

For example, fields such as:

- Cancer Type
- Cancer Stage
- Receptor Status
- Survival Status
- Affected Breast

need consistent categories so that Power BI does not treat slightly different spellings as separate groups.

---

## Step 5 — Validated numerical fields

Numerical fields such as:

- Age
- Tumor Size
- Survival Months
- Recurrence-related values

were checked for unreasonable or inconsistent values.

This step helps prevent incorrect averages and misleading visualizations.

---

## Step 6 — Created/validated time fields

A month field was prepared for the monthly trend analysis.

The month structure allows the dashboard to display patient counts from:

**January → December**

rather than treating months as random text categories.

---

# 🧮 2. Data Modeling & Calculations

After cleaning the data, I moved into the modeling and calculation stage.

The focus was on creating reusable measures instead of manually calculating values inside individual visuals.

## Core Measures

### Total Patients

```DAX
Total Patients =
COUNTROWS('Cancer Data')
```

### Survival Patients

```DAX
Survival Patients =
CALCULATE(
    [Total Patients],
    'Cancer Data'[Survival Status] = "Survived"
)
```

### Deceased Patients

```DAX
Deceased Patients =
CALCULATE(
    [Total Patients],
    'Cancer Data'[Survival Status] = "Deceased"
)
```

### Average Age

```DAX
Avg. Age =
AVERAGE('Cancer Data'[Age])
```

### Average Tumor Size

```DAX
Avg. Tumor Size =
AVERAGE('Cancer Data'[Tumor Size])
```

### Average Survival Months

```DAX
Avg. Survival Months =
AVERAGE('Cancer Data'[Survival Months])
```

### Survival Rate

```DAX
Survival Rate % =
DIVIDE(
    [Survival Patients],
    [Total Patients],
    0
)
```

Format as **Percentage**.

### Recurrence Rate

```DAX
Recurrence Rate % =
DIVIDE(
    [Recurrence Patients],
    [Total Patients],
    0
)
```

> Replace `[Recurrence Patients]` with the measure/logic matching the recurrence field in the actual dataset.

### Average Recurrence

```DAX
Avg. Recurrence =
AVERAGE('Cancer Data'[Recurrence])
```

---

# 📊 3. KPI Design

The dashboard uses KPI cards to provide an immediate summary before the user begins exploring the charts.

## Page 1 — Patient & Cancer Profile

The main KPIs are:

| KPI | Purpose |
|---|---|
| Total Patients | Shows the size of the patient population |
| Survival Patients | Shows the number of patients recorded as surviving |
| Avg. Age | Shows the average patient age |
| Avg. Tumor Size | Shows the average tumor size |
| Avg. Survival Months | Shows the average recorded survival duration |

### Values shown in the dashboard

- **Total Patients:** 5,000
- **Survival Patients:** 3,750
- **Avg. Age:** 55
- **Avg. Tumor Size:** 4.3
- **Avg. Survival Months:** 29.5

---

## Page 2 — Treatment & Patient Outcomes

The main KPIs are:

| KPI | Purpose |
|---|---|
| Survival Patients | Number of surviving patients |
| Deceased Patients | Number of deceased patients |
| Survival Rate % | Percentage of patients recorded as surviving |
| Recurrence Rate % | Percentage of patients recorded with recurrence |
| Avg. Recurrence | Average recurrence value in the dataset |

### Values shown in the dashboard

- **Survival Patients:** 3,750
- **Deceased Patients:** 1,250
- **Survival Rate:** 75.0%
- **Recurrence Rate:** 30.1%
- **Avg. Recurrence:** 6.4

---

# 🔎 4. Analytical Questions & Visualizations

## Page 1 — Patient & Cancer Profile

### Question 1: How are patients distributed across cancer stages?

**Visual:** Horizontal bar chart

This visual compares the number of patients across:

- Stage 0
- Stage 1
- Stage 2
- Stage 3
- Stage 4

This helps users understand how the patient population is distributed across the available cancer stages.

---

### Question 2: What is the distribution of patients by cancer type?

**Visual:** Column chart

The dashboard compares:

- Inflammatory Breast Cancer
- Ductal Carcinoma
- Lobular Carcinoma
- Triple Negative

The values shown are approximately:

- Inflammatory Breast Cancer — 1,291
- Ductal Carcinoma — 1,249
- Lobular Carcinoma — 1,233
- Triple Negative — 1,227

---

### Question 3: How are patients distributed by affected breast?

**Visual:** Column chart

The dashboard compares:

- Right
- Bilateral
- Left

This provides a simple view of the affected-breast distribution in the dataset.

---

### Question 4: How are patients distributed by receptor status?

**Visual:** Lollipop-style/bar visual

The dashboard compares the available receptor categories:

- HER2+
- ER+/PR+
- ER+/PR-
- ER-/PR-

This helps summarize the distribution of receptor-status groups.

---

### Question 5: How does tumor size vary by cancer stage?

**Visual:** Horizontal bar chart

The dashboard uses the **sum of tumor size** by cancer stage.

This provides a stage-level comparison of the aggregate tumor-size values recorded in the dataset.

> **Important analytical note:** because this is a **sum**, it represents total recorded tumor-size values within each stage. It should not be interpreted as the average tumor size for an individual patient.

---

# 📈 5. Treatment & Patient Outcomes Analysis

## Question 6: How does survival rate vary by cancer stage?

**Visual:** Horizontal bar chart

The dashboard compares survival rates across Stage 0 through Stage 4.

The displayed values are:

- Stage 0 — 96.4%
- Stage 1 — 95.4%
- Stage 2 — 80.3%
- Stage 3 — 55.8%
- Stage 4 — 54.5%

These figures describe the distribution observed in this dataset; they do not establish a medical causal relationship.

---

## Question 7: How does survival rate vary by cancer type?

**Visual:** Column chart

The dashboard compares survival rate across the four cancer-type categories.

Displayed values include approximately:

- Ductal Carcinoma — 76.7%
- Triple Negative — 75.9%
- Lobular Carcinoma — 73.9%
- Inflammatory Breast Cancer — 73.6%

---

## Question 8: How does recurrence rate vary by cancer type?

**Visual:** Horizontal bar chart

The dashboard compares recurrence rates across cancer types.

Displayed values are approximately:

- Lobular Carcinoma — 31.7%
- Ductal Carcinoma — 30.4%
- Inflammatory Breast Cancer — 29.9%
- Triple Negative — 28.4%

Again, these are descriptive results from the dataset and should not be interpreted as clinical risk estimates.

---

## Question 9: How does patient volume change across months?

**Visual:** Line chart

The monthly trend visual displays patient counts from January through December.

This allows the user to identify:

- Higher-volume months
- Lower-volume months
- Changes in patient counts over time
- Seasonal or recurring patterns worth investigating

A trend chart is particularly useful because it turns individual monthly values into an easy-to-read time sequence.

---

# 🎨 6. Dashboard Design

I designed the dashboard around a consistent healthcare-inspired visual system.

## Design principles used

### 1. Clear visual hierarchy

The layout follows:

**Page title → Filter → KPI cards → Analytical visuals**

This allows users to understand the dashboard from high-level KPIs before moving into detailed analysis.

### 2. Consistent color palette

A burgundy/rose color palette was used throughout the dashboard to create a consistent visual identity.

The light background provides contrast while keeping the dashboard visually clean.

### 3. Consistent KPI cards

Each KPI card contains:

- Metric title
- Main value
- Supporting icon
- Consistent spacing

### 4. Consistent navigation

The left-side navigation area separates the dashboard pages and provides a visual navigation structure.

### 5. Interactive filtering

A **Month Short** slicer was included so users can filter the dashboard based on month.

This allows users to move from an overall view to a more focused period.

---

# 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI** | Dashboard development and visualization |
| **Power Query** | Data cleaning and transformation |
| **DAX** | Measures and KPI calculations |
| **Data Modeling** | Structuring fields and analytical relationships |
| **GitHub** | Project documentation and portfolio presentation |

---

# 🔄 End-to-End Workflow

The complete workflow for this project was:

```text
Raw Dataset
     ↓
Data Understanding
     ↓
Power Query
     ↓
Data Cleaning
     ↓
Data Transformation
     ↓
Data Modeling
     ↓
DAX Measures
     ↓
KPI Development
     ↓
Analytical Questions
     ↓
Visualization
     ↓
Dashboard Design
     ↓
Validation
     ↓
Insights & Documentation
```

---

# ✅ Dashboard Validation

Before finalizing the dashboard, I checked the calculations and visuals to make sure:

- KPI totals matched the underlying dataset.
- Survival + deceased patients reconciled with the total patient count where the categories were mutually exclusive.
- Percentages were correctly formatted.
- Category labels were consistent.
- Month values were displayed in the correct order.
- Visual totals responded correctly to filters.
- Charts were using the intended aggregation.
- No unnecessary visual elements were overcrowding the dashboard.
- The two dashboard pages told a logical analytical story.

---

# 💡 Key Observations from the Dashboard

Based on the displayed dashboard results:

### Patient population

The dataset contains **5,000 patients**, with **3,750 recorded as surviving** and **1,250 recorded as deceased**.

### Patient profile

The average age shown is **55 years**, while the average tumor size is approximately **4.3** and the average survival duration is approximately **29.5 months**.

### Cancer stages

The patient population is distributed across five cancer stages, with Stage 2 representing the largest displayed patient group.

### Cancer types

The four cancer-type categories have relatively similar patient counts, with each category representing roughly one-quarter of the overall dataset.

### Survival

The overall survival rate displayed on the dashboard is **75.0%**.

The stage-level visualization shows substantial differences in the recorded survival rates across stages within this dataset.

### Recurrence

The dashboard displays an overall recurrence rate of **30.1%**, with differences across cancer-type categories.

These observations are **descriptive findings from the dataset**, not clinical conclusions.

---

# 🚧 Challenges Encountered

One of the important parts of this project was not just building visuals, but solving the problems that appeared during the process.

### Challenge 1 — Preparing raw data for analysis

Raw datasets are not always ready for visualization. Before creating the dashboard, I had to inspect data types, missing values, categorical fields, and numerical columns.

**Solution:** I used Power Query to profile, clean, standardize, and transform the data before loading it into the report.

---

### Challenge 2 — Choosing the right KPI calculations

A KPI can easily become misleading if the wrong aggregation or denominator is used.

For example, survival rate requires a percentage calculation rather than simply counting records.

**Solution:** I created reusable DAX measures using `CALCULATE()` and `DIVIDE()` so the calculations could respond dynamically to filters.

---

### Challenge 3 — Making month analysis work correctly

Month names are text values, so Power BI can sometimes sort them alphabetically instead of chronologically.

**Solution:** I created a month-number/sorting structure and used it to ensure the monthly trend followed:

```text
Jan → Feb → Mar → Apr → May → Jun
→ Jul → Aug → Sep → Oct → Nov → Dec
```

---

### Challenge 4 — Presenting a large amount of information without overcrowding the dashboard

Healthcare datasets can contain many dimensions.

**Solution:** I separated the analysis into two pages:

**Page 1:** Patient & Cancer Profile

**Page 2:** Treatment & Patient Outcomes

This made the dashboard easier to navigate and allowed each page to answer a distinct group of questions.

---

# 📚 What I Learned

This project strengthened my understanding of:

- Data cleaning with Power Query
- Data transformation
- DAX measures
- KPI development
- Percentage calculations
- Aggregation logic
- Time-series analysis
- Categorical analysis
- Dashboard layout
- Visual hierarchy
- Interactive slicers
- Data validation
- Healthcare-style analytical storytelling

More importantly, I learned that a good dashboard is not just a collection of charts.

The analytical process should connect:

**Business/analytical questions → Data → Calculations → Visuals → Insights**

---

# 🚀 Future Improvements

If I were extending this project, I would consider adding:

- Patient-level drill-through
- More detailed treatment analysis
- Additional age-group analysis
- Survival analysis by demographic characteristics
- Treatment-method comparisons
- Interactive tooltips
- More advanced time intelligence
- Additional filters for cancer stage/type
- A dedicated data dictionary
- Automated data refresh
- A more detailed clinical/outcome analysis page

---

# 📁 Suggested Repository Structure

```text
patient-cancer-analytics/
│
├── README.md
│
├── data/
│   └── cancer_patient_data.csv
│
├── powerbi/
│   └── patient_cancer_dashboard.pbix
│
├── screenshots/
│   ├── patient-cancer-profile.png
│   └── treatment-patient-outcomes.png
│
├── documentation/
│   └── project-notes.md
│
└── LICENSE
```

> If the original dataset has licensing or privacy restrictions, do not upload the raw dataset. In that case, upload a data dictionary or a link to the original public dataset instead.

---

# 📸 Dashboard Preview

## Page 1 — Patient & Cancer Profile $  Treatment & Patient Outcomes
<img width="969" height="1080" alt="WhatsApp Image 2026-09-12 at 11 20 55" src="https://github.com/user-attachments/assets/451b8911-d70a-4a64-b756-d27efdaea423" />


 Treatment & Patient Outcomes



---

# 🎥 Project Walkthrough

A complete walkthrough of this project covers:

1. Understanding the dataset
2. Cleaning the data in Power Query
3. Transforming columns
4. Creating calculated fields
5. Building DAX measures
6. Creating KPIs
7. Developing analytical questions
8. Building the visuals
9. Designing the two dashboard pages
10. Validating the final results
11. Interpreting the dashboard findings

---

# 👤 About the Project

This project is part of my **Data Analytics portfolio** and demonstrates my ability to take a dataset from the preparation stage through to an interactive business-style dashboard.

I focused on making the project demonstrate both sides of analytics:

### Technical skills

- Power Query
- DAX
- Data modeling
- Data transformation
- Visualization

### Analytical skills

- KPI development
- Question-driven analysis
- Trend analysis
- Comparative analysis
- Insight generation
- Dashboard storytelling

---

# ⭐ Skills Demonstrated

`Power BI` `Power Query` `DAX` `Data Cleaning` `Data Transformation` `Data Modeling` `KPI Development` `Data Visualization` `Healthcare Analytics` `Dashboard Design` `Analytical Storytelling`

---

## 📬 Connect

If you are interested in discussing the project, data analytics, Power BI, or opportunities to collaborate, feel free to connect with me on LinkedIn.

**LinkedIn:** [https://www.linkedin.com/in/konkwo-victor-a9aab526b/]
[Breast_Cancer_Analytics (1).pptx](https://github.com/user-attachments/files/32359300/Breast_Cancer_Analytics.1.pptx)


---

## ⭐ If you found this project useful

Feel free to explore the repository and share feedback.

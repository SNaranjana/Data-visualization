# 🏥 Healthcare Data Understanding, Cleaning & Exploratory Analysis

##  Project Overview

The **Healthcare Data Understanding, Cleaning & Exploratory Analysis** project focuses on analyzing healthcare data using Python. The main goal is to clean patient records, organize medical information, and understand patient admissions, billing amounts, and hospital stays.

This project uses data analysis techniques to identify patterns in patient demographics, medical conditions, and admission types.

##  Project Objectives

- Clean missing values in medical codes.
- Standardize date columns into a consistent format.
- Categorize hospital admissions into Emergency, Elective, and Urgent.
- Calculate summary statistics for patient billing amounts.
- Analyze hospital stays in days.
- Study patient demographics based on medical conditions.
- Identify useful patterns in healthcare data.

##  Tools and Technologies

- **Python:** Used to process and analyze healthcare data.
- **Pandas:** Used to clean data and organize patient records.
- **NumPy:** Used for numerical calculations.
- **Matplotlib:** Used to create charts and graphs.
- **Seaborn:** Used to visualize patterns in healthcare data.
- **Google Colab:** Used to write and execute Python code.

## Dataset Description

The dataset contains healthcare-related information about patients, hospital admissions, medical conditions, and billing.

Common columns may include:

| Column Name | Description |
|---|---|
| Patient ID | Unique identification number for each patient |
| Age | Age of the patient |
| Gender | Gender of the patient |
| Medical Condition | Patient's medical condition |
| Medical Code | Code associated with a medical record or diagnosis |
| Admission Type | Type of hospital admission |
| Date of Admission | Date the patient was admitted |
| Discharge Date | Date the patient was discharged |
| Billing Amount | Amount billed for healthcare services |
| Length of Stay | Number of days the patient stayed in the hospital |


##  1. Data Cleaning

Data cleaning helps improve the quality and reliability of healthcare information.

### Tasks Performed

- Identify missing values in the dataset.
- Fill or handle missing medical codes where appropriate.
- Remove duplicate records when necessary.
- Convert date columns into a consistent date format.
- Check data types and correct invalid values.
- Calculate hospital stay duration using admission and discharge dates.

### Example Code

```python
import pandas as pd
import numpy as np

# Load the dataset
df = pd.read_csv('/content/healthcare_dataset.csv')

# Display the first five rows
print(df.head())

# Check missing values
print(df.isnull().sum())

# Remove duplicate records
df = df.drop_duplicates()

# Standardize date columns
df['Date of Admission'] = pd.to_datetime(
    df['Date of Admission'], errors='coerce'
)

df['Discharge Date'] = pd.to_datetime(
    df['Discharge Date'], errors='coerce'
)

# Handle missing medical codes
df['Medical Code'] = df['Medical Code'].fillna('Unknown')

# Calculate hospital stay duration
df['Length of Stay'] = (
    df['Discharge Date'] - df['Date of Admission']
).dt.days

# Display cleaned data
print(df.head())
```

**Explanation:**

- `pd.read_csv()` loads the healthcare dataset.
- `df.head()` displays the first five records.
- `df.isnull().sum()` counts missing values in each column.
- `drop_duplicates()` removes duplicate rows.
- `pd.to_datetime()` converts date columns into a standard date format.
- `fillna()` handles missing medical codes by assigning `Unknown`.
- Date subtraction calculates the number of days between admission and discharge.

Hospital admissions can be grouped into three categories:

- **Emergency:** Patients requiring immediate medical attention.
- **Elective:** Planned admissions for scheduled procedures or treatment.
- **Urgent:** Patients requiring prompt medical attention but not necessarily immediate emergency treatment.

### Example Code

```python
# Check admission categories
print(df['Admission Type'].value_counts())

# Display admission category counts
df['Admission Type'] = df['Admission Type'].str.strip().str.title()

print(df['Admission Type'].value_counts())
```

**Explanation:**

- `value_counts()` counts the number of admissions in each category.
- `str.strip()` removes unnecessary spaces.
- `str.title()` standardizes category capitalization.

The admission categories should be based on the dataset's existing labels and clinical definitions. Do not automatically treat every unknown admission type as Emergency, Elective, or Urgent.

##  3. Patient Billing Analysis

Billing analysis helps understand the amount charged for healthcare services.

### Example Code

```python
# Calculate billing statistics
print("Average Billing:", df['Billing Amount'].mean())
print("Minimum Billing:", df['Billing Amount'].min())
print("Maximum Billing:", df['Billing Amount'].max())
print("Median Billing:", df['Billing Amount'].median())

# Display complete summary statistics
print(df['Billing Amount'].describe())
```

**Explanation:**

- `mean()` calculates the average billing amount.
- `min()` finds the lowest billing amount.
- `max()` finds the highest billing amount.
- `median()` finds the middle billing value.
- `describe()` provides count, mean, standard deviation, minimum, quartiles, and maximum.

These statistics help identify typical billing amounts and unusually high or low values.

##  4. Hospital Stay Analysis

Hospital stay analysis measures how long patients remain admitted.

### Example Code

```python
# Calculate hospital stay statistics
print("Average Stay:", df['Length of Stay'].mean())
print("Minimum Stay:", df['Length of Stay'].min())
print("Maximum Stay:", df['Length of Stay'].max())

# Display summary statistics
print(df['Length of Stay'].describe())
```

**Explanation:**

- The average shows the typical length of a hospital stay.
- The minimum shows the shortest recorded stay.
- The maximum shows the longest recorded stay.
- Summary statistics help compare hospital stay durations.

Check negative or missing stay durations before interpreting the results. A negative value may indicate an incorrect admission or discharge date.

##  5. Demographic Analysis by Medical Condition

Demographic analysis helps identify how patient characteristics vary across medical conditions.

### Example Code

```python
# Patient count by medical condition
print(df['Medical Condition'].value_counts())

# Analyze age by medical condition
print(
    df.groupby('Medical Condition')['Age']
    .mean()
    .sort_values(ascending=False)
)

# Analyze gender by medical condition
print(
    pd.crosstab(
        df['Medical Condition'],
        df['Gender']
    )
)
```

**Explanation:**

- `value_counts()` counts patients or records in each medical condition category.
- `groupby()` groups records by medical condition.
- `mean()` calculates the average age for each condition.
- `pd.crosstab()` compares the recorded gender categories across medical conditions.

These results help summarize demographic patterns in the dataset. They do not establish that a demographic characteristic causes a medical condition.

##  6. Data Visualization

Charts make healthcare data easier to understand.

### Billing Amount Distribution

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.histplot(df['Billing Amount'].dropna(), kde=True)

plt.title('Distribution of Patient Billing Amounts')
plt.xlabel('Billing Amount')
plt.ylabel('Number of Records')

plt.show()
```

**Explanation:**

- `histplot()` displays the distribution of billing amounts.
- `kde=True` adds a smooth density curve.
- The chart helps identify the spread and skewness of billing amounts.

### Admission Type Comparison

```python
sns.countplot(data=df, x='Admission Type')

plt.title('Hospital Admissions by Type')
plt.xlabel('Admission Type')
plt.ylabel('Number of Admissions')

plt.xticks(rotation=15)
plt.show()
```

**Explanation:**

- `countplot()` displays the number of records in each admission category.
- The chart helps compare Emergency, Elective, and Urgent admissions.

### Average Age by Medical Condition

```python
age_data = df.groupby('Medical Condition')['Age'].mean()

age_data.plot(kind='bar')

plt.title('Average Patient Age by Medical Condition')
plt.xlabel('Medical Condition')
plt.ylabel('Average Age')

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

**Explanation:**

- `groupby()` organizes patients by medical condition.
- `mean()` calculates the average age.
- The bar chart compares average patient ages across conditions.

##  7. Expected Outcomes

After completing the analysis, the project can help:

- Identify missing or inconsistent healthcare data.
- Organize medical codes and date attributes.
- Understand the distribution of hospital admission types.
- Summarize patient billing amounts.
- Measure hospital stay durations.
- Compare demographic characteristics across medical conditions.
- Present healthcare findings using charts and summary statistics.


##  8. How to Run the Project in Google Colab

1. Open Google Colab.
2. Create a new notebook.
3. Upload your healthcare CSV dataset.
4. Import Pandas, NumPy, Matplotlib, and Seaborn.
5. Load the dataset using `pd.read_csv()`.
6. Run the data-cleaning code.
7. Perform admission, billing, and hospital stay analysis.
8. Generate charts to visualize the results.
9. Review the outputs and summarize your findings.

##  Conclusion

The **Healthcare Data Understanding, Cleaning & Exploratory Analysis** project demonstrates how Python can be used to clean healthcare records, analyze patient admissions, summarize billing amounts, calculate hospital stays, and explore demographic patterns.

This project provides practical experience in data preprocessing, exploratory data analysis, statistical summaries, and data visualization. These skills are useful for students interested in Python programming, healthcare analytics, and data science.

##  Author

**Name:** NARANJAN S

**Course:**  (BCA)

**College:** Kamaraj College, Thoothukudi, Tamil Nadu

**Project Domain:** Healthcare Data Analysis

**Tools Used:** Python, Pandas, NumPy, Matplotlib, Seaborn, Google Colab

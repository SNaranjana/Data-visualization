# 🏥 Healthcare Data Visualization, Cost Relationship & Policy Insights

##  Project Overview

The **Healthcare Data Visualization, Cost Relationship & Policy Insights** project focuses on analyzing healthcare data using Python. It uses charts, statistical analysis, and data visualization techniques to understand medical costs, patient admissions, insurance providers, and hospital stays.

The project helps identify patterns in healthcare expenses, admission trends, and relationships between patient age, hospital stay duration, and total medical costs.

##  Project Objectives

- Create stacked bar charts to compare billing amounts across medical conditions and insurance providers.
- Use violin plots to understand the distribution of patient billing amounts.
- Create temporal line charts to identify trends and seasonal changes in patient admissions.
- Generate a correlation matrix to study relationships between age, hospital stay duration, and medical costs.
- Prepare an executive summary with healthcare management recommendations.
- Identify useful insights to support healthcare planning and policy decisions.

##  Tools and Technologies

- **Python:** Programming language for data analysis.
- **Pandas:** Data cleaning, grouping, and data manipulation.
- **NumPy:** Numerical calculations.
- **Matplotlib:** Creating charts and graphs.
- **Seaborn:** Statistical data visualization.
- **Google Colab:** Writing and executing Python code.

##  Dataset Description

The dataset contains information about patients, medical conditions, insurance providers, billing amounts, and hospital admissions.

| Column Name | Description |
|---|---|
| Patient ID | Unique patient identifier |
| Age | Age of the patient |
| Gender | Gender of the patient |
| Medical Condition | Medical condition recorded for the patient |
| Insurance Provider | Name of the insurance provider |
| Billing Amount | Amount billed for healthcare services |
| Date of Admission | Date when the patient was admitted |
| Discharge Date | Date when the patient was discharged |
| Length of Stay | Number of days spent in the hospital |


##  1. Stacked Bar Chart: Medical Conditions and Billing

A stacked bar chart compares billing amounts across medical conditions and insurance providers.

### Example Code

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
df = pd.read_csv('/content/healthcare_dataset.csv')

# Create a summary of billing amounts
billing_data = df.pivot_table(
    index='Medical Condition',
    columns='Insurance Provider',
    values='Billing Amount',
    aggfunc='sum',
    fill_value=0
)

# Plot stacked bar chart
billing_data.plot(kind='bar', stacked=True, figsize=(12, 6))

plt.title('Total Billing by Medical Condition and Insurance Provider')
plt.xlabel('Medical Condition')
plt.ylabel('Total Billing Amount')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Explanation

- `pivot_table()` groups billing data by medical condition and insurance provider.
- `aggfunc='sum'` calculates the total billing amount for each group.
- `fill_value=0` fills missing combinations in the summary table with zero.
- `stacked=True` displays insurance-provider values on top of one another.

**Insight:** This chart can help identify which medical conditions and insurance providers account for the largest total billed amounts. Higher totals may reflect patient volume, billing differences, or both.

##  2. Violin Plot: Billing Amount Distribution

A violin plot displays the distribution of billing amounts for different medical conditions.

### Example Code

```python
plt.figure(figsize=(12, 6))

sns.violinplot(
    data=df,
    x='Medical Condition',
    y='Billing Amount',
    inner='quartile'
)

plt.title('Billing Amount Distribution by Medical Condition')
plt.xlabel('Medical Condition')
plt.ylabel('Billing Amount')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Explanation

- `violinplot()` displays the distribution of billing amounts.
- `inner='quartile'` shows the quartiles inside each violin.
- Wider sections indicate where observations are more concentrated.

**Insight:** The chart can reveal differences in billing distributions, variation in patient costs, and potential high-cost cases.

### Compare Billing by Insurance Provider

```python
plt.figure(figsize=(12, 6))

sns.violinplot(
    data=df,
    x='Insurance Provider',
    y='Billing Amount',
    inner='quartile'
)

plt.title('Billing Amount Distribution by Insurance Provider')
plt.xlabel('Insurance Provider')
plt.ylabel('Billing Amount')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

**Insight:** This visualization helps compare the distribution of billed amounts among insurance providers. It does not, by itself, establish differences in reimbursement rates or insurance coverage.

##  3. Temporal Line Chart: Patient Admission Trends

A temporal line chart displays patient admissions over time. It can help identify busy periods and possible seasonal patterns.

### Example Code

```python
# Convert admission date to datetime
df['Date of Admission'] = pd.to_datetime(
    df['Date of Admission'],
    errors='coerce'
)

# Remove records without valid admission dates
admission_data = df.dropna(subset=['Date of Admission']).copy()

# Group admissions by month
admission_data['Month'] = (
    admission_data['Date of Admission'].dt.to_period('M')
)

monthly_admissions = admission_data.groupby('Month').size()

# Plot admission trends
monthly_admissions.index = monthly_admissions.index.to_timestamp()

monthly_admissions.plot(figsize=(12, 6), marker='o')

plt.title('Monthly Patient Admission Trends')
plt.xlabel('Month')
plt.ylabel('Number of Admissions')
plt.grid(True)
plt.tight_layout()
plt.show()
```

### Explanation

- `pd.to_datetime()` converts admission dates into a standard date format.
- `dropna()` excludes records without valid admission dates from this analysis.
- `to_period('M')` groups dates by month.
- `groupby().size()` counts admissions in each month.
- The line chart displays changes in admission volume over time.

**Insight:** Admission peaks may help hospitals plan staffing, beds, and medical supplies.

**Important:** Reliable seasonal analysis requires enough historical data, ideally covering multiple years. A single short period may reveal admission fluctuations but cannot establish a recurring seasonal pattern.

##  4. Correlation Matrix: Age, Hospital Stay, and Medical Cost

A correlation matrix measures the strength and direction of linear relationships between numerical variables.

### Example Code

```python
# Calculate hospital stay duration
df['Discharge Date'] = pd.to_datetime(
    df['Discharge Date'],
    errors='coerce'
)

df['Length of Stay'] = (
    df['Discharge Date'] - df['Date of Admission']
).dt.days

# Select numerical columns
corr_data = df[
    ['Age', 'Length of Stay', 'Billing Amount']
].copy()

# Calculate correlations
correlation_matrix = corr_data.corr()

print(correlation_matrix)

# Visualize the correlation matrix
plt.figure(figsize=(8, 5))

sns.heatmap(
    correlation_matrix,
    annot=True,
    cmap='coolwarm',
    fmt='.2f',
    vmin=-1,
    vmax=1
)

plt.title('Correlation Matrix of Healthcare Variables')
plt.tight_layout()
plt.show()
```

### Explanation

- `Length of Stay` measures the number of days between admission and discharge.
- `corr()` calculates pairwise Pearson correlations between numerical variables.
- `heatmap()` displays the correlation matrix visually.
- `annot=True` displays the correlation values inside the chart.
- Values range from **-1 to +1**.

### Understanding Correlation Values

| Correlation Value | Interpretation |
|---|---|
| Close to +1 | Strong positive linear relationship |
| Close to 0 | Weak or no linear relationship |
| Close to -1 | Strong negative linear relationship |


##  5. Executive Summary and Healthcare Management Recommendations

The analysis can support healthcare managers in understanding billing patterns, admission volumes, and patient stay durations.

### Key Areas to Evaluate

**1. Medical Billing**

Compare total billing amounts across medical conditions and insurance providers. Investigate large differences while considering patient volume and treatment complexity.

**2. Insurance Provider Analysis**

Compare billing distributions to identify differences that may require further review. Before making policy changes, examine contract terms, coverage, patient mix, and reimbursement data.

**3. Admission Planning**

Use monthly admission trends to identify periods of high demand. Hospitals can consider adjusting staffing, bed availability, and medical supply planning accordingly.

**4. Hospital Stay Management**

Study the relationship between hospital stay duration and billing amounts. Review unusually long stays to identify opportunities to improve care coordination without compromising patient safety.

**5. Patient Demographics**

Analyze age and medical condition patterns to support service planning. Demographic findings should be interpreted carefully and should not be used as a substitute for individual clinical assessment.

**6. Data Quality**

Maintain consistent medical codes, admission dates, discharge dates, and billing records. Better data quality improves the reliability of reports and management decisions.

### Sample Executive Summary

This project applies Python-based visualization and statistical analysis to healthcare data. Stacked bar charts compare total billing across medical conditions and insurance providers, while violin plots show the distribution of billed amounts. Monthly admission charts help explore changes in hospital demand, and a correlation matrix examines relationships among patient age, length of stay, and billing amount.

The resulting analysis can help healthcare managers identify areas for further investigation, improve resource planning, and monitor billing patterns. Recommendations should be based on the actual results, data quality, clinical context, and appropriate financial measures.

*This summary describes the purpose of the analysis. Specific findings and recommendations must be confirmed using the actual dataset and generated charts.*

##  6. How to Run the Project in Google Colab

1. Open Google Colab.
2. Create a new Python notebook.
3. Upload your healthcare dataset in CSV format.
4. Import Pandas, NumPy, Matplotlib, and Seaborn.
5. Load the CSV file using `pd.read_csv()`.
6. Check the column names and clean the data.
7. Run the stacked bar chart and violin plot code.
8. Generate the monthly admission trend chart.
9. Calculate and visualize the correlation matrix.
10. Review the outputs and prepare your executive summary.

##  Conclusion

The **Healthcare Data Visualization, Cost Relationship & Policy Insights** project demonstrates how Python can transform healthcare records into meaningful visualizations and statistical summaries.

By analyzing billing distributions, insurance-provider patterns, admission trends, and relationships between patient age, hospital stay duration, and billed amounts, the project provides a foundation for data-driven healthcare management.

It also provides practical experience in Python, Pandas, statistical analysis, data visualization, and healthcare analytics.

##  Author

**Name:** NARANJAN S

**Course:** BCA

**College:** Kamaraj College

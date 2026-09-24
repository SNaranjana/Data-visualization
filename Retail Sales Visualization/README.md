# Retail Sales Visualization, Relationship Analysis & Business Insights

##  Project Overview

This project focuses on analyzing and visualizing **retail sales data** using Python.

The main purpose of this project is to understand:

- Sales performance across different categories
- Profit distribution
- Effect of discounts on profit
- Delivery time
- Relationship between numerical variables
- Sales and profit patterns
- Important business insights from the dataset

The project uses **Pandas, NumPy, Matplotlib, and Seaborn** for data analysis and visualization.

---

##  Objectives

The major objectives of this project are:

1. Load and understand the retail sales dataset.
2. Clean and prepare the data for analysis.
3. Convert date columns into proper date format.
4. Calculate delivery time.
5. Analyze sales by category.
6. Analyze profit by category.
7. Understand sales and profit distributions.
8. Study the relationship between discount and profit.
9. Calculate correlations between numerical variables.
10. Create visualizations to identify useful business patterns.
11. Generate business insights from the analysis.

---

##  Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Pandas | Data cleaning and analysis |
| NumPy | Numerical operations |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| Google Colab | Development environment |

---

##  Dataset

The project uses the **Sample Superstore dataset**.

Dataset file:

```text
samplesuperstore.csv
```

The dataset contains retail order information such as:

- Order Date
- Ship Date
- Category
- Sales
- Profit
- Discount
- Customer and product-related information

The dataset can be used to understand sales and business performance.

---

#  Project Workflow

```text
Load Dataset
      ↓
Understand Dataset
      ↓
Check Data Information
      ↓
Check Statistical Summary
      ↓
Convert Date Columns
      ↓
Calculate Delivery Days
      ↓
Check Categories
      ↓
Check Missing Values
      ↓
Analyze Sales
      ↓
Analyze Profit
      ↓
Analyze Discount
      ↓
Correlation Analysis
      ↓
Create Visualizations
      ↓
Generate Business Insights
```

---

# 1. Import Required Libraries

```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
```

### Explanation

- `pandas` is used for data loading, cleaning, and analysis.
- `numpy` is used for numerical operations.
- `matplotlib` is used to create charts.
- `seaborn` is used to create statistical visualizations.

---

# 2. Load the Dataset

```python
df = pd.read_csv("/content/samplesuperstore.csv")
```

The `read_csv()` function loads the CSV file into a Pandas DataFrame.

The DataFrame is stored in the variable:

```text
df
```

---

# 3. View the First Records

```python
df.head()
```

### Purpose

`head()` displays the first five rows of the dataset.

It helps us understand:

- Column names
- Data values
- Dataset structure

---

# 4. Understand Dataset Information

```python
df.info()
```

### Purpose

`info()` provides information about:

- Number of rows
- Number of columns
- Column names
- Data types
- Non-null values

This is useful for identifying incorrect data types and missing values.

---

# 5. Statistical Summary

```python
df.describe()
```

### Purpose

`describe()` provides statistical information for numerical columns.

It includes:

- Count
- Mean
- Standard deviation
- Minimum
- 25% percentile
- 50% percentile
- 75% percentile
- Maximum

This helps us understand the distribution of numerical data.

---

# 6. Convert Date Columns

```python
df['Order Date'] = pd.to_datetime(df['Order Date'])

df['Ship Date'] = pd.to_datetime(df['Ship Date'])
```

The `Order Date` and `Ship Date` columns are converted into proper datetime format.

This allows us to perform date-related calculations.

---

# 7. Calculate Delivery Days

```python
df['Delivery Days'] = (df['Ship Date'] - df['Order Date']).dt.days
```

A new column called:

```text
Delivery Days
```

is created.

It represents the number of days between the order date and shipping date.

### Formula

```text
Delivery Days = Ship Date - Order Date
```

This can help in understanding delivery performance.

---

# 8. Check Categories

```python
df['Category'].unique()
```

This displays all unique product categories available in the dataset.

For example, the Superstore dataset commonly contains categories such as:

```text
Furniture
Office Supplies
Technology
```

---

# 9. Check Missing Values

```python
df.isnull().sum()
```

This checks the number of missing values in every column.

### Purpose

Missing-value checking is important because missing data can affect:

- Calculations
- Visualizations
- Statistical analysis
- Business conclusions

---

# 10. Sales by Category

```python
category_sales = (df.groupby('Category')['Sales'].sum())

category_sales
```

The data is grouped according to `Category`, and total sales are calculated for each category.

### Visualization

```python
category_sales.plot(
    kind='bar',
    figsize=(8,5)
)

plt.title("Sales by Category")
plt.ylabel("Total Sales")
plt.show()
```

### What the chart shows

The bar chart compares total sales between product categories.

This helps identify which categories generate more total sales.

---

# 11. Sales Distribution

```python
plt.figure(figsize=(8,5))

sns.histplot(
    df['Sales'],
    bins=30
)

plt.title("Sales Distribution")
plt.show()
```

A histogram is used to understand how sales values are distributed.

### It helps identify:

- Common sales ranges
- Low-value orders
- High-value orders
- Distribution patterns

---

# 12. Profit by Category

```python
sns.barplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit by Category")
plt.show()
```

This visualization compares profit across different categories.

### Business use

It helps identify categories that generate higher or lower average profit.

---

# 13. Sales Distribution by Category

```python
sns.barplot(
    data=df,
    x="Category",
    y="Sales"
)

plt.title("Sales Distribution by Category")
plt.show()
```

This chart compares the average sales values across categories.

It provides another view of category-level sales performance.

---

# 14. Overall Profit Distribution

```python
sns.boxplot(
    data=df,
    y="Profit"
)

plt.title("Profit Distribution")
plt.show()
```

A box plot is used to understand the distribution of profit.

### It helps identify:

- Median profit
- Spread of profit
- Possible outliers
- Very high or low profit values

---

# 15. Profit Variation Across Categories

```python
sns.boxplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit Variation Across Categories")
plt.show()
```

This compares profit distributions across different categories.

It helps understand whether profit varies significantly within each category.

---

# 16. Check Discount Values

```python
df["Discount"].unique()
```

This displays the unique discount values available in the dataset.

Discount is important because it can influence the final profit obtained from a sale.

---

# 17. Discount vs Profit Analysis

```python
sns.scatterplot(
    data=df,
    x="Discount",
    y="Profit"
)

plt.title("Impact of Discount on Profit")
plt.show()
```

A scatter plot is used to examine the relationship between discount and profit.

### Purpose

The visualization helps identify whether different discount levels are associated with changes in profit.

**Important:** This chart shows an association in the dataset. It does not by itself prove that discount causes a particular profit result.

---

# 18. Select Numerical Columns

```python
numeric_df = df.select_dtypes(
    include="number"
)
```

This selects only numerical columns from the DataFrame.

Examples may include:

- Sales
- Quantity
- Discount
- Profit
- Delivery Days

---

# 19. Calculate Correlation

```python
corr = numeric_df.corr()

corr
```

The `.corr()` function calculates the correlation between numerical variables.

Correlation values generally range from:

```text
-1 to +1
```

### Simple meaning

| Correlation | Meaning |
|---|---|
| +1 | Strong positive relationship |
| 0 | Little or no linear relationship |
| -1 | Strong negative relationship |

Correlation measures association, not causation.

---

# 20. Correlation Heatmap

```python
sns.heatmap(
    corr,
    annot=True
)

plt.title("Correlation Heatmap")
plt.show()
```

The heatmap provides a visual representation of relationships between numerical variables.

The `annot=True` option displays the correlation values inside the cells.

### Purpose

The heatmap helps quickly identify:

- Positive relationships
- Negative relationships
- Weak relationships
- Strong relationships



---

# 📊 Visualizations Created

This project creates several important visualizations:

1. **Sales by Category — Bar Chart**
2. **Sales Distribution — Histogram**
3. **Profit by Category — Bar Chart**
4. **Sales Distribution by Category — Bar Chart**
5. **Profit Distribution — Box Plot**
6. **Profit Variation Across Categories — Box Plot**
7. **Discount vs Profit — Scatter Plot**
8. **Correlation Heatmap**

These visualizations make it easier to understand patterns in the retail data.

---

#  Business Insights

The analysis can be used to identify insights such as:

### 1. Category Performance

Total sales can be compared across categories to understand where sales volume is concentrated.

### 2. Profit Performance

Profit analysis helps identify categories with different profitability patterns.

### 3. Discount and Profit

The scatter plot can be used to investigate whether higher discounts are associated with lower or higher profit values.

### 4. Profit Variation

Box plots show how widely profit varies within each category and help identify unusual values.

### 5. Sales Distribution

The sales histogram shows whether most orders are concentrated in lower-value ranges or whether high-value orders are common.

### 6. Delivery Performance

The `Delivery Days` column provides information about the time taken between order and shipment.

### 7. Relationships Between Variables

The correlation heatmap provides a quick overview of relationships among numerical variables.

---

#  Key Questions Explored

This project explores the following business questions:

- Which product categories generate more sales?
- How is sales distributed across orders?
- How does profit vary between categories?
- How widely does profit vary within categories?
- What relationship can be observed between discount and profit?
- Which numerical variables have stronger relationships?
- How many days are taken between ordering and shipping?
- Are there unusual profit or sales values?

---

#  Data Preparation

The following data preparation steps were performed:

```text
✔ Dataset loaded
✔ Dataset structure checked
✔ Statistical summary checked
✔ Date columns converted
✔ Delivery Days calculated
✔ Categories checked
✔ Missing values checked
✔ Numerical columns selected
✔ Correlation calculated
```

---

#  Project Structure

```text
Retail-Sales-Analysis/
│
├── samplesuperstore.csv
│
├── Retail_Sales_Analysis.ipynb
│
└── README.md
```

---

#  How to Run the Project

## Step 1: Open Google Colab

Open Google Colab and create a new notebook.

## Step 2: Upload Dataset

Upload:

```text
samplesuperstore.csv
```

## Step 3: Import Libraries

Run the required library imports.

## Step 4: Load Dataset

```python
df = pd.read_csv("/content/samplesuperstore.csv")
```

## Step 5: Run the Analysis

Execute the cells step by step.

## Step 6: View Visualizations

The notebook will generate charts for:

- Sales
- Profit
- Discount
- Categories
- Correlation

---

#  Main Python Functions Used

| Function | Purpose |
|---|---|
| `pd.read_csv()` | Read CSV file |
| `df.head()` | Display first rows |
| `df.info()` | Display dataset information |
| `df.describe()` | Statistical summary |
| `pd.to_datetime()` | Convert dates |
| `groupby()` | Group data |
| `sum()` | Calculate total |
| `unique()` | Find unique values |
| `isnull().sum()` | Check missing values |
| `select_dtypes()` | Select numerical columns |
| `.corr()` | Calculate correlation |
| `plt.show()` | Display chart |

---

#  Conclusion

This project demonstrates how Python can be used to perform **retail sales analysis and business data visualization**.

The analysis starts with understanding and preparing the dataset and then uses different visualization techniques to study sales, profit, discounts, delivery time, and relationships between numerical variables.

The project provides a practical introduction to **Exploratory Data Analysis (EDA)** and shows how visualizations can help transform raw retail data into understandable business information.

 # Author

Name: S. Naranjana

Course: BCA

College:Kamaraj College(Face prep campus)

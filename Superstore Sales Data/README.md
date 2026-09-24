# Superstore Sales Data Understanding, Cleaning & Exploratory Analysis

## 1. Project Title

**Superstore Sales Data Understanding, Cleaning & Exploratory Analysis**

---

## 2. Project Overview

This project focuses on understanding, cleaning, and exploring the **Superstore Sales Dataset** using Python.

The dataset contains information about orders, customers, products, sales, quantity, discount, profit, regions, and dates.

The main purpose of this project is to convert raw sales data into useful information through:

- Data Understanding
- Data Cleaning
- Data Preprocessing
- Exploratory Data Analysis (EDA)
- Data Visualization
- Business Insights

Python libraries such as **Pandas, NumPy, Matplotlib, and Seaborn** are used for the analysis.

---

## 3. Objectives

The main objectives of this project are:

1. Understand the structure of the Superstore dataset.
2. Load the dataset using Python.
3. Check the number of rows and columns.
4. Understand the available columns.
5. Check data types.
6. Identify missing values.
7. Identify duplicate records.
8. Clean the dataset.
9. Convert date columns into the correct format.
10. Perform descriptive statistical analysis.
11. Analyze sales and profit.
12. Explore categories, regions, products, and customers.
13. Create meaningful visualizations.
14. Identify useful business insights.

---

## 4. Dataset Description

The Superstore Sales Dataset is a retail dataset containing information about customer orders and product sales.

The dataset generally contains information such as:

| Column | Description |
|---|---|
| Row ID | Unique ID for each row |
| Order ID | Unique order identification number |
| Order Date | Date when the order was placed |
| Ship Date | Date when the order was shipped |
| Ship Mode | Shipping method |
| Customer ID | Unique customer ID |
| Customer Name | Customer name |
| Segment | Customer segment |
| Country | Country |
| City | City |
| State | State |
| Postal Code | Postal code |
| Region | Sales region |
| Product ID | Unique product ID |
| Category | Main product category |
| Sub-Category | Product sub-category |
| Product Name | Name of the product |
| Sales | Sales amount |
| Quantity | Number of products sold |
| Discount | Discount provided |
| Profit | Profit or loss |

> **Note:** The exact columns may vary depending on the Superstore dataset version.

---

## 5. Technologies Used

### Programming Language

- Python

### Python Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn

### Tools

- Jupyter Notebook
- Google Colab
- VS Code

---

## 6. Project Structure

  text
Superstore-Sales-Analysis/
│
├── data/
│   └── superstore.csv
│
├── notebook/
│   └── superstore_analysis.ipynb
│
├── outputs/
│   └── charts/
│
└── README.md


### Folder Description

**data/**  
Contains the Superstore dataset.

**notebook/**  
Contains the Python/Jupyter Notebook used for analysis.

**outputs/**  
Contains generated charts and analysis results.

**README.md**  
Contains the complete project documentation.

---

# 7. Data Understanding

Data understanding is the first step of the project.

In this step, we examine the dataset before performing any cleaning or analysis.

---

## 7.1 Import Libraries

 python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns


### Purpose

- **Pandas** → Data manipulation and analysis
- **NumPy** → Numerical calculations
- **Matplotlib** → Data visualization
- **Seaborn** → Statistical visualization

---

## 7.2 Load the Dataset

 python
df = pd.read_csv("superstore.csv")

The dataset is loaded into a Pandas DataFrame called `df`.

---

## 7.3 Display First Five Rows

 python
df.head()


This displays the first five records of the dataset.

It helps us understand the structure and content of the data.

---

## 7.4 Display Last Five Rows

```python
df.tail()
```

This displays the last five records.

It helps confirm that the dataset has been loaded correctly.

---

## 7.5 Check Dataset Size

```python
df.shape
```

This returns:

```text
(number of rows, number of columns)
```

For example:

```text
(9994, 21)
```

This means the dataset contains 9,994 rows and 21 columns.

> The actual result depends on the dataset version.

---

## 7.6 Check Column Names

```python
df.columns
```

This displays all the column names in the dataset.

---

## 7.7 Check Data Types

```python
df.dtypes
```

This displays the data type of every column.

Common data types are:

- `int64` → Integer
- `float64` → Decimal number
- `object` → Text
- `datetime` → Date and time

---

## 7.8 Check Dataset Information

```python
df.info()
```

This provides information about:

- Number of rows
- Number of columns
- Column names
- Data types
- Non-null values
- Memory usage

---

# 8. Data Cleaning

Data cleaning is performed to improve the quality and accuracy of the dataset.

The main cleaning operations include:

- Checking missing values
- Checking duplicate records
- Converting dates
- Checking incorrect data types
- Checking unusual values

---

## 8.1 Check Missing Values

```python
df.isnull().sum()
```

This displays the number of missing values in each column.

Missing values should be checked because they can affect the accuracy of analysis.

---

## 8.2 Check Duplicate Records

```python
df.duplicated().sum()
```

This identifies duplicate rows.

If duplicate rows are found, they can be removed using:

```python
df = df.drop_duplicates()
```

---

## 8.3 Convert Date Columns

```python
df['Order Date'] = pd.to_datetime(df['Order Date'])
df['Ship Date'] = pd.to_datetime(df['Ship Date'])
```

Converting dates allows us to perform time-based analysis.

For example:

- Monthly sales
- Yearly sales
- Sales trends
- Shipping duration

---

## 8.4 Check Data Types Again

```python
df.dtypes
```

After cleaning, we check the data types again to make sure they are correct.

---

## 8.5 Check Numerical Values

```python
df.describe()
```

This provides statistical information about numerical columns.

It includes:

- Count
- Mean
- Standard deviation
- Minimum
- Maximum
- Quartiles

---

# 9. Exploratory Data Analysis

Exploratory Data Analysis, or **EDA**, is used to understand patterns and relationships in the dataset.

The main areas analyzed are:

- Sales
- Profit
- Quantity
- Discount
- Category
- Sub-Category
- Region
- State
- Products
- Customers
- Time-based sales

---

# 10. Sales Analysis

## 10.1 Total Sales

```python
total_sales = df['Sales'].sum()

print("Total Sales:", total_sales)
```

This calculates the total sales generated from all orders.

---

# 11. Profit Analysis

## 11.1 Total Profit

```python
total_profit = df['Profit'].sum()

print("Total Profit:", total_profit)
```

This calculates the total profit generated from the sales.

Positive values represent profit, while negative values represent loss.

---

# 12. Quantity Analysis

```python
total_quantity = df['Quantity'].sum()

print("Total Quantity Sold:", total_quantity)
```

This calculates the total number of products sold.

---

# 13. Sales by Category

```python
category_sales = df.groupby('Category')['Sales'].sum()

print(category_sales)
```

This calculates the total sales for each product category.

### Visualization

```python
category_sales.plot(kind='bar')

plt.title('Sales by Category')
plt.xlabel('Category')
plt.ylabel('Sales')
plt.show()
```

The bar chart makes it easier to compare sales between categories.

---

# 14. Profit by Category

```python
category_profit = df.groupby('Category')['Profit'].sum()

print(category_profit)
```

### Visualization

```python
category_profit.plot(kind='bar')

plt.title('Profit by Category')
plt.xlabel('Category')
plt.ylabel('Profit')
plt.show()
```

This helps compare the profit generated by different categories.

---

# 15. Sales by Sub-Category

```python
subcategory_sales = df.groupby('Sub-Category')['Sales'].sum()

print(subcategory_sales)
```

### Visualization

```python
subcategory_sales.sort_values(ascending=False).plot(kind='bar')

plt.title('Sales by Sub-Category')
plt.xlabel('Sub-Category')
plt.ylabel('Sales')
plt.xticks(rotation=45)
plt.show()
```

This helps identify high-sales and low-sales sub-categories.

---

# 16. Sales by Region

```python
region_sales = df.groupby('Region')['Sales'].sum()

print(region_sales)
```

### Visualization

```python
region_sales.plot(kind='bar')

plt.title('Sales by Region')
plt.xlabel('Region')
plt.ylabel('Sales')
plt.show()
```

This helps compare sales performance between regions.

---

# 17. Sales by State

```python
state_sales = df.groupby('State')['Sales'].sum().sort_values(ascending=False)

print(state_sales.head(10))
```

This displays the top states based on sales.

### Visualization

```python
state_sales.head(10).plot(kind='bar')

plt.title('Top 10 States by Sales')
plt.xlabel('State')
plt.ylabel('Sales')
plt.xticks(rotation=45)
plt.show()
```

---

# 18. Monthly Sales Analysis

First, create a month column.

```python
df['Month'] = df['Order Date'].dt.month
```

Calculate monthly sales:

```python
monthly_sales = df.groupby('Month')['Sales'].sum()

print(monthly_sales)
```

### Visualization

```python
monthly_sales.plot(kind='line', marker='o')

plt.title('Monthly Sales')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()
```

This helps identify monthly sales patterns.

---

# 19. Yearly Sales Analysis

Create a year column:

```python
df['Year'] = df['Order Date'].dt.year
```

Calculate yearly sales:

```python
yearly_sales = df.groupby('Year')['Sales'].sum()

print(yearly_sales)
```

### Visualization

```python
yearly_sales.plot(kind='line', marker='o')

plt.title('Yearly Sales')
plt.xlabel('Year')
plt.ylabel('Sales')
plt.show()
```

This helps understand changes in sales over the years.

---

# 20. Top 10 Products by Sales

```python
top_products = (
    df.groupby('Product Name')['Sales']
    .sum()
    .sort_values(ascending=False)
    .head(10)
)

print(top_products)
```

### Visualization

```python
top_products.plot(kind='bar')

plt.title('Top 10 Products by Sales')
plt.xlabel('Product')
plt.ylabel('Sales')
plt.xticks(rotation=90)
plt.show()
```

This identifies the products with the highest total sales.

---

# 21. Top 10 Products by Profit

```python
top_profit_products = (
    df.groupby('Product Name')['Profit']
    .sum()
    .sort_values(ascending=False)
    .head(10)
)

print(top_profit_products)
```

This identifies products with the highest total profit.

---

# 22. Loss-Making Products

```python
product_profit = df.groupby('Product Name')['Profit'].sum()

loss_products = product_profit[product_profit < 0]

print(loss_products)
```

This identifies products that generate an overall loss.

This information can help in reviewing:

- Product pricing
- Discounts
- Product costs
- Sales strategies

---

# 23. Discount Analysis

```python
discount_profit = df.groupby('Discount')['Profit'].sum()

print(discount_profit)
```

### Visualization

```python
plt.scatter(df['Discount'], df['Profit'])

plt.title('Discount vs Profit')
plt.xlabel('Discount')
plt.ylabel('Profit')
plt.show()
```

This helps explore the relationship between discount and profit.

---

# 24. Sales Distribution

A histogram can be used to understand the distribution of sales.

```python
plt.hist(df['Sales'], bins=30)

plt.title('Sales Distribution')
plt.xlabel('Sales')
plt.ylabel('Frequency')
plt.show()
```

The histogram shows how sales values are distributed.

---

# 25. Profit Distribution

```python
plt.hist(df['Profit'], bins=30)

plt.title('Profit Distribution')
plt.xlabel('Profit')
plt.ylabel('Frequency')
plt.show()
```

This helps understand the distribution of profit and loss.

---

# 26. Box Plot

A box plot can be used to identify the spread of data and possible outliers.

```python
sns.boxplot(x=df['Sales'])

plt.title('Sales Box Plot')
plt.show()
```

The box plot displays:

- Minimum
- Maximum
- Median
- Quartiles
- Possible outliers

---

# 27. Correlation Analysis

Correlation can be used to understand relationships between numerical columns.

```python
numeric_data = df[['Sales', 'Quantity', 'Discount', 'Profit']]

correlation = numeric_data.corr()

print(correlation)
```

### Correlation Heatmap

```python
sns.heatmap(correlation, annot=True)

plt.title('Correlation Heatmap')
plt.show()
```

The heatmap provides a visual representation of relationships between numerical variables.

---

# 28. Data Visualization

Different charts are used to understand the data easily.

| Chart | Purpose |
|---|---|
| Bar Chart | Compare categories |
| Line Chart | Show trends over time |
| Histogram | Show data distribution |
| Box Plot | Identify spread and outliers |
| Scatter Plot | Show relationships |
| Heatmap | Show correlation |

---

# 29. Business Insights

After completing the analysis, useful business insights can be identified from the actual results.

Examples include:

- High-performing product categories
- Low-performing product categories
- High-sales regions
- High-profit products
- Loss-making products
- Monthly sales patterns
- Yearly sales trends
- Customer segment performance
- Relationship between discount and profit

> The final insights should be based on the actual analysis results and not on assumptions.

---

# 30. Data Cleaning Summary

The following data-cleaning steps are performed:

### Missing Values

```python
df.isnull().sum()
```

Missing values are identified and handled when necessary.

### Duplicate Values

```python
df.duplicated().sum()
```

Duplicate records are checked and removed when required.

### Date Conversion

```python
df['Order Date'] = pd.to_datetime(df['Order Date'])
```

Date columns are converted into the correct format.

### Data Type Checking

```python
df.dtypes
```

Data types are checked and corrected where necessary.

### Invalid Values

Numerical and categorical columns are checked for unusual or incorrect values.

---

# 31. Project Workflow

```text
Superstore Dataset
        ↓
Load Dataset
        ↓
Understand Dataset
        ↓
Check Rows & Columns
        ↓
Check Data Types
        ↓
Check Missing Values
        ↓
Check Duplicates
        ↓
Clean Data
        ↓
Convert Date Columns
        ↓
Descriptive Statistics
        ↓
Exploratory Data Analysis
        ↓
Create Visualizations
        ↓
Identify Business Insights
        ↓
Conclusion
```

---

# 32. Conclusion

The **Superstore Sales Data Understanding, Cleaning & Exploratory Analysis** project demonstrates how raw sales data can be cleaned, analyzed, and visualized using Python.

The project begins with understanding the dataset and checking its structure. Data cleaning is then performed to identify missing values, duplicate records, incorrect data types, and other data-quality issues.

After cleaning, Exploratory Data Analysis is performed to study sales, profit, quantity, discount, products, categories, regions, states, and time-based trends.

Different visualizations such as bar charts, line charts, histograms, box plots, scatter plots, and heatmaps are used to make the analysis easier to understand.

The project helps transform raw sales data into meaningful business information and demonstrates the importance of **data-driven decision-making**.


# 35. Author

**Name:** S. Naranjana

**Course:** BCA

**College:** Kamaraj College(Face Prep Campus)

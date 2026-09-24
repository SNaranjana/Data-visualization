# Shopify Stock Data Understanding, Cleaning & Exploratory Analysis

##  Project Overview

This project focuses on understanding, cleaning, and exploring **Shopify stock market data** using Python.

The main purpose of this project is to analyze historical stock prices and understand how the Shopify stock price changes over time.

The analysis includes:

- Understanding the dataset
- Checking the structure of the data
- Checking missing values
- Removing duplicate records
- Converting dates into the correct format
- Sorting the data by date
- Finding the highest and lowest stock prices
- Calculating the average closing price
- Calculating daily price changes
- Identifying daily losses
- Calculating the total loss
- Visualizing the closing price using a line chart

---

## Objectives

The main objectives of this project are:

1. To understand the Shopify stock dataset.
2. To inspect the columns and data types.
3. To identify missing values.
4. To remove duplicate records.
5. To convert the Date column into the correct date format.
6. To arrange stock records in chronological order.
7. To calculate basic stock price statistics.
8. To calculate daily changes in the closing price.
9. To identify daily losses.
10. To visualize Shopify's closing price trend.

---

##  Dataset

The dataset is stored in an Excel file named:

```text
task 1.xlsx
```

The dataset contains historical Shopify stock information.

Common stock market columns include:

- `Date` – Date of the stock record
- `Open` – Opening price of the stock
- `High` – Highest price during the day
- `Low` – Lowest price during the day
- `Close` – Closing price of the stock
- `Volume` – Number of shares traded

The exact columns depend on the provided dataset.

---

##  Technologies Used

The following tools and libraries are used:

- **Python**
- **Pandas**
- **Matplotlib**
- **Jupyter Notebook / Google Colab / VS Code**
- **Microsoft Excel** for the input dataset

---

##  Python Libraries

### Pandas

Pandas is used for:

- Reading the Excel file
- Data cleaning
- Data manipulation
- Date conversion
- Calculations
- Finding statistics

```python
import pandas as pd
```

### Matplotlib

Matplotlib is used to create the stock price visualization.

```python
import matplotlib.pyplot as plt
```

---

#  Project Workflow

The project follows these main steps:

```text
Load Dataset
     ↓
Understand Dataset
     ↓
Check Missing Values
     ↓
Remove Duplicates
     ↓
Convert Date Format
     ↓
Sort Data by Date
     ↓
Calculate Statistics
     ↓
Calculate Daily Price Change
     ↓
Calculate Loss
     ↓
Visualize Closing Price
     ↓
Analyze Results
```

---

# 1.  Loading the Dataset

The Excel file is loaded using Pandas.

```python
df = pd.read_excel("task 1.xlsx")
```

The `read_excel()` function reads the Excel file and stores the data in a Pandas DataFrame.

The DataFrame is named:

```python
df
```

# 2.  Viewing the Dataset

The first five records are displayed using:

```python
df.head()
```

The last five records are displayed using:

```python
print(df.tail())
```

These commands help us understand how the dataset looks.

---

# 3.  Understanding Dataset Information

The `info()` function is used to understand the structure of the dataset.

```python
print(df.info())
```

It provides information such as:

- Number of rows
- Number of columns
- Column names
- Data types
- Non-null values

This helps identify incorrect data types and missing values.

---

# 4.  Checking Missing Values

Missing values are checked using:

```python
print(df.isnull().sum())
```

This displays the number of missing values in each column.

Checking missing values is important because missing data can affect calculations and analysis.

---

# 5.  Removing Duplicate Records

Duplicate rows are removed using:

```python
df = df.drop_duplicates()
```

Duplicate records can affect the accuracy of statistical analysis.

Removing duplicates ensures that the same stock record is not counted multiple times.

---

# 6.  Converting Date Format

The `Date` column is converted into a proper datetime format.

```python
df["Date"] = pd.to_datetime(df["Date"])
```

This makes it easier to:

- Sort records by date
- Analyze time-based data
- Create time-series graphs

---

# 7.  Sorting Data by Date

The stock records are sorted according to the date.

```python
df = df.sort_values("Date")
```

This ensures that the stock data is arranged in chronological order.

Example:

```text
Old Date
   ↓
Next Date
   ↓
Next Date
   ↓
Recent Date
```

---

# 8.  Finding Highest Stock Price

The highest stock price is found using the `High` column.

```python
print("Highest Price:", df["High"].max())
```

The `max()` function returns the maximum value from the High column.

---

# 9.  Finding Lowest Stock Price

The lowest stock price is found using:

```python
print("Lowest Price:", df["Low"].min())
```

The `min()` function returns the minimum value from the Low column.

---

# 10.  Finding Average Closing Price

The average closing price is calculated using:

```python
print("Average Closing Price:", df["Close"].mean())
```

The `mean()` function calculates the average value of the closing prices.

The average helps us understand the general level of the stock's closing price during the analyzed period.

---

# 11. Calculating Daily Price Change

Daily price change is calculated using:

```python
df["Daily Price Change"] = df["Close"].diff()
```

The `diff()` function calculates the difference between the current day's closing price and the previous day's closing price.

### Example

If the closing prices are:

```text
Day 1 → ₹100
Day 2 → ₹105
Day 3 → ₹102
```

The daily changes are:

```text
Day 1 → NaN
Day 2 → +5
Day 3 → -3
```

A positive value means the closing price increased.

A negative value means the closing price decreased.

---

# 12. 📉 Calculating Daily Loss

Loss is calculated from the daily price change.

```python
df["Loss"] = df["Daily Price Change"].apply(
    lambda x: abs(x) if x < 0 else 0
)
```

The logic is:

```text
Daily Price Change
        ↓
   Is it negative?
      /       \
    Yes       No
     ↓         ↓
 Calculate    Loss = 0
 absolute
 value
```

For example:

| Daily Price Change | Loss |
|---:|---:|
| +10 | 0 |
| -5 | 5 |
| +8 | 0 |
| -3 | 3 |

Only negative price changes are considered losses.

---

# 13.  Calculating Total Loss

The total loss is calculated using:

```python
total_loss = df["Loss"].sum()
```

The result is displayed using:

```python
print("\nTotal Loss:", total_loss)
```

This gives the sum of all daily negative price movements in the analyzed dataset.

**Note:** This is a calculated measure of daily closing-price decreases. It is not the same as an investor's actual monetary trading loss, because actual profit/loss depends on the number of shares owned, purchase price, transaction costs, and other factors.

---

# 14.  Stock Price Visualization

A line chart is created to visualize the closing price.

```python
plt.figure(figsize=(10,5))

plt.plot(df["Date"], df["Close"])

plt.xlabel("Date")
plt.ylabel("Closing Price")

plt.title("Shopify Stock Price Analysis")

plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

### Chart Explanation

- **X-axis:** Date
- **Y-axis:** Closing Price
- **Line:** Shopify closing price over time

The graph helps us visually understand whether the stock price generally increased, decreased, or fluctuated during the selected period.

---

#  Main Analysis Performed

| Analysis | Python Function |
|---|---|
| Load Excel file | `pd.read_excel()` |
| View first rows | `head()` |
| View last rows | `tail()` |
| Dataset information | `info()` |
| Missing values | `isnull().sum()` |
| Remove duplicates | `drop_duplicates()` |
| Convert date | `pd.to_datetime()` |
| Sort records | `sort_values()` |
| Highest price | `max()` |
| Lowest price | `min()` |
| Average closing price | `mean()` |
| Daily change | `diff()` |
| Total loss | `sum()` |
| Visualization | `plt.plot()` |

---

#  Key Concepts Used

### Data Cleaning

Data cleaning is the process of preparing raw data for analysis.

In this project:

- Duplicate records are removed.
- Date values are converted into the correct format.
- Data is sorted chronologically.

### Exploratory Data Analysis

Exploratory Data Analysis (EDA) is the process of examining data to understand its patterns, values, and characteristics.

This project performs EDA using:

- Maximum value
- Minimum value
- Mean value
- Daily price change
- Loss calculation
- Line chart

### Time-Series Analysis

Stock prices are time-based data.

The `Date` column is used to arrange and visualize stock prices over time.

---

#  Results

The project produces the following results:

- Dataset structure and information
- Missing-value information
- Cleaned stock dataset
- Highest stock price
- Lowest stock price
- Average closing price
- Daily closing-price changes
- Daily losses
- Total calculated loss
- Shopify closing-price visualization

The actual numerical results depend on the values present in `task 1.xlsx`.

---


#  Conclusion

This project demonstrates how Python can be used to understand and analyze historical Shopify stock data.

Using **Pandas**, the dataset was loaded, inspected, cleaned, and analyzed. Duplicate records were removed, dates were converted into the correct format, and the data was sorted chronologically.

Basic statistical measures such as the highest price, lowest price, and average closing price were calculated. Daily closing-price changes and daily losses were also calculated.

Finally, a line chart was created using **Matplotlib** to visualize the Shopify closing-price trend over time.

Overall, this project provides a simple introduction to **stock data analysis, data cleaning, exploratory data analysis, and time-series visualization using Python**.

---

##  Author

**S. Naranjana**

** BCA 

Kamaraj College(Face Prep Campus)



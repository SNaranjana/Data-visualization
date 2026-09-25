# 📈 Shopify Stock Data Understanding, Cleaning & Exploratory Analysis

##  Project Overview

This project focuses on understanding, cleaning, and exploring **Shopify stock price data** using Python.

The analysis includes:

* Loading stock data from an Excel file
* Understanding the dataset
* Checking missing values and duplicates
* Cleaning and sorting the data
* Finding the highest, lowest, and average prices
* Calculating daily price changes
* Identifying daily losses
* Visualizing the closing price trend

---

##  Technologies Used

* Python
* Pandas
* Matplotlib
* Jupyter Notebook / Google Colab
* Microsoft Excel

---

##  Dataset

**File:** `task 1.xlsx`

The dataset contains stock market information with columns such as:

* `Date` – Trading date
* `Open` – Opening price
* `High` – Highest price of the day
* `Low` – Lowest price of the day
* `Close` – Closing price
* `Volume` – Trading volume

---

##  Data Analysis Steps

### 1. Import Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
```

### 2. Load the Dataset

```python
df = pd.read_excel("task 1.xlsx")
```

### 3. Understand the Dataset

```python
df.head()
print(df.tail())
print(df.info())
print(df.isnull().sum())
```

These commands help understand the dataset structure, data types, and missing values.

### 4. Remove Duplicate Records

```python
df = df.drop_duplicates()
```

Duplicate records are removed to improve data quality.

### 5. Convert Date Column

```python
df["Date"] = pd.to_datetime(df["Date"])
```

The `Date` column is converted into a proper datetime format.

### 6. Sort Data by Date

```python
df = df.sort_values("Date")
```

The records are arranged chronologically.

---

## Statistical Analysis

### Highest Price

```python
print("Highest Price:", df["High"].max())
```

Finds the highest stock price in the dataset.

### Lowest Price

```python
print("Lowest Price:", df["Low"].min())
```

Finds the lowest stock price.

### Average Closing Price

```python
print("Average Closing Price:", df["Close"].mean())
```

Calculates the average closing price.

---

## Daily Price Change

The daily price change is calculated using the difference between consecutive closing prices.

```python
df["Daily Price Change"] = df["Close"].diff()

print(df[["Date", "Close", "Daily Price Change"]])
```

### Formula

**Daily Price Change = Current Closing Price − Previous Closing Price**

* Positive value → Price increased
* Negative value → Price decreased
* Zero → No change

---

##  Stock Price Visualization

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

This line graph shows how Shopify's closing price changes over time.

---

##  Loss Calculation

A loss is calculated when the daily price change is negative.

```python
df["Loss"] = df["Daily Price Change"].apply(
    lambda x: abs(x) if x < 0 else 0
)

print(df[["Date", "Close", "Loss"]])
```

### Total Loss

```python
total_loss = df["Loss"].sum()

print("Total Loss:", total_loss)
```

This calculates the total amount of daily negative price changes in the dataset.

---


##  Project Structure

```text
Shopify-Stock-Analysis/
│
├── task 1.xlsx
├── Shopify_Stock_Analysis.ipynb
└── README.md
```

##  Future Improvements

The project can be extended by adding:

* Moving Average (MA20 and MA50)
* Daily return percentage
* Volatility analysis
* Trading volume visualization
* Candlestick charts
* Correlation analysis
* Stock price prediction using Machine Learning

---

##  Author

**S. Naranjana**

**BCA**

**College : ** Kamaraj College**

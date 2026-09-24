Big Data Task 1 – Superstore Sales Analysis using Python
Project Title
Big Data Task 1: Exploratory Data Analysis (EDA) on Sample Superstore Dataset

Project Description
This project focuses on performing Exploratory Data Analysis (EDA) on the Sample Superstore Dataset using Python. The main objective is to understand the sales performance of a retail business by cleaning, processing, analyzing, and visualizing the data.

The project demonstrates the complete data analysis workflow, starting from importing the dataset to generating meaningful business insights through graphs and statistical analysis.

The analysis was carried out using Google Colab / Jupyter Notebook with popular Python libraries such as Pandas, NumPy, Matplotlib, and Seaborn.

Objectives
The primary objectives of this project are:

Import and load the dataset.
Explore the dataset structure.
Understand data types and statistical information.
Convert date columns into proper datetime format.
Calculate delivery time between order and shipment.
Detect missing values.
Analyze total sales for each product category.
Create visualizations for better understanding.
Learn the complete process of data preprocessing and visualization.
Repository Structure
Big-Data-Task-1/ │ ├── Big_data_Task_1_naranjana.ipynb ├── big_data_task_1_naranjana.py ├── samplesuperstore.csv ├── README.md └── images/ ├── sales_category.png └── sales_distribution.png

Technologies Used
Technology	Purpose
Python	Programming Language
Google Colab	Development Environment
Jupyter Notebook	Interactive Analysis
Pandas	Data Manipulation
NumPy	Numerical Operations
Matplotlib	Data Visualization
Seaborn	Statistical Visualization
Python Libraries
The project uses the following libraries:

python import pandas as pd import numpy as np import matplotlib.pyplot as plt import seaborn as sns

Pandas
Used for:

Reading CSV files
Data cleaning
Data analysis
Data preprocessing
NumPy
Used for:

Mathematical operations
Numerical computations
Matplotlib
Used for:

Creating graphs
Bar charts
Basic visualizations
Seaborn
Used for:

Attractive statistical plots
Histograms
Data distribution graphs
Dataset Information
Dataset Name:

Sample Superstore Dataset *
The dataset contains retail store transaction details.

Important columns include:

Column	Description
Order Date	Date when customer placed the order
Ship Date	Date when order was shipped
Category	Product category
Sales	Total sales amount
Customer Name	Customer information
Region	Sales region
Profit	Profit earned
Quantity	Number of items sold
Project Workflow
step 1 – Import Libraries
Necessary Python libraries are imported.

Purpose:

Data analysis
Visualization
Numerical operations
Step 2 – Upload Dataset
The dataset is uploaded into Google Colab.

python uploaded = files.upload()

Purpose:

Allow users to upload CSV files.
Step 3 – Load Dataset
python df = pd.read_csv("samplesuperstore.csv")

Purpose:

Read CSV file into a DataFrame.
Step 4 – Display First Records
python df.head()

Purpose:

View first five rows.
Verify successful loading.
Step 5 – Explore Dataset
df.info()
Purpose:

View data types.
Count non-null values.
Understand dataset structure.
Step 6 – Statistical Summary
df.describe()
Purpose:

Calculate:

Mean
Median
Standard Deviation
Minimum
Maximum
Quartiles
Step 7 – Convert Date Columns
df['Order Date']=pd.to_datetime(df['Order Date'])
df['Ship Date']=pd.to_datetime(df['Ship Date'])
Purpose:

Convert text into datetime format.
Enable date calculations.
Step 8 – Calculate Delivery Days
df['Delivery Days']=(df['Ship Date']-df['Order Date']).dt.days
Purpose:

Calculate shipping duration.
Analyze delivery performance.
Example:

Order Date	Ship Date	Delivery Days
01-01-2024	05-01-2024	4
Step 9 – Check Missing Values
df.isnull().sum()
Purpose:

Detect missing data.
Improve data quality.
Step 10 – Category-wise Sales Analysis
category_sales=df.groupby('Category')['Sales'].sum()
Purpose:

Calculate total sales for each category.
Compare business performance.
Example Output:

Category	Total Sales
Furniture	XXXXX
Office Supplies	XXXXX
Technology	XXXXX
Step 11 – Bar Chart Visualization
category_sales.plot(kind='bar')
Purpose:

Compare sales among categories.
Easily identify highest-selling category.
Output:

Sales by Category Bar Chart
Step 12 – Sales Distribution
sns.histplot(df['Sales'],bins=30)
Purpose:

Understand sales frequency.
Identify distribution patterns.
Detect skewness or outliers.
Output:

Histogram of Sales
Results
The project successfully:

✔ Loaded the dataset

✔ Explored dataset information

✔ Generated statistical summary

✔ Converted date columns

✔ Calculated delivery duration

✔ Checked missing values

✔ Calculated category-wise sales

✔ Created bar chart

✔ Created histogram

Visualizations
1. Sales by Category
Displays the total sales for each product category using a bar chart.

Benefits:

Easy comparison
Business decision making
Product performance analysis
2. Sales Distribution
Shows how sales values are distributed.

Benefits:

Detect outliers
Understand customer purchase behavior
Analyze sales trends
Learning Outcomes
After completing this project, you will understand:

Reading CSV files using Pandas
Data exploration techniques
Data preprocessing
Date conversion
Missing value detection
Feature engineering
GroupBy operations
Data visualization
Business data analysis
Exploratory Data Analysis (EDA)
Future Improvements
Possible enhancements include:

Monthly Sales Analysis
Regional Sales Analysis
Customer Segmentation
Profit Analysis
Discount Analysis
Sales Forecasting using Machine Learning
Interactive Dashboards using Plotly
Power BI Dashboard
Streamlit Web Application
How to Run the Project
Clone the Repository
git clone https://github.com/your-username/Big-Data-Task-1.git
Navigate to the Project
cd Big-Data-Task-1
Install Dependencies
pip install pandas numpy matplotlib seaborn
Launch Jupyter Notebook
jupyter notebook
Open:

Big_data_Task_1_naranjana.ipynb
Or execute:

python big_data_task_1_naranjana.py
   Author
S. Naranjana

Course: Bachelor of Computer Applications

College: Kamaraj College(Face prep campus)

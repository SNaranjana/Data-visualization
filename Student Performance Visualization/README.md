# 📊 Student Performance Visualization, Demographic Analysis & Educational Insights

##  1. Project Introduction

Student performance is an important part of education. Students may achieve different marks in Mathematics, Reading, and Writing.

Their performance may be associated with different factors, such as parental education, lunch type, and test preparation.

This project uses Python to analyze student performance data and create different visualizations. These charts help us understand student scores, compare groups, and identify patterns in academic performance.

The main aim of this project is to understand student performance and provide useful educational recommendations.

##  2. Project Objectives

The main objectives of this project are:

- To analyze Mathematics, Reading, and Writing scores.
- To compare average scores across parental education levels.
- To compare student performance by lunch type.
- To analyze scores based on test preparation.
- To create grouped bar charts and box plots.
- To create scatter plots and a correlation heatmap.
- To identify relationships between different subjects.
- To provide educational insights and policy recommendations.

##  3. Dataset Information

The dataset used in this project is called `StudentsPerformance.csv`.

It contains information about 1,000 students.

### Dataset Columns

| Column Name | Description |
|---|---|
| gender | Gender of the student |
| race/ethnicity | Student's race or ethnicity group |
| parental level of education | Parents' highest education level |
| lunch | Type of lunch received by the student |
| test preparation course | Whether the student completed test preparation |
| math score | Mathematics examination score |
| reading score | Reading examination score |
| writing score | Writing examination score |

The dataset contains both categorical data and numerical data.

**Categorical data** describes groups, such as lunch type and parental education.

**Numerical data** contains measurable values, such as Mathematics, Reading, and Writing scores.

##  4. Tools and Technologies

The following tools and libraries are used in this project.

| Tool | Purpose |
|---|---|
| Python | Programming and data analysis |
| Pandas | Loading and analyzing data |
| NumPy | Numerical calculations |
| Matplotlib | Creating charts and graphs |
| Seaborn | Creating statistical visualizations |
| Google Colab | Running Python code online |
| GitHub | Storing and sharing the project |

##  5. Project Workflow

The project follows these steps:

1. Import the required Python libraries.
2. Load the student performance dataset.
3. Examine the dataset and its columns.
4. Check for missing values.
5. Calculate average scores.
6. Create grouped bar charts.
7. Create box plots.
8. Create scatter plots.
9. Generate a correlation heatmap.
10. Analyze the results.
11. Provide educational recommendations.

##  6. Python Code

### Step 1: Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Step 2: Load the Dataset

```python
df = pd.read_csv("StudentsPerformance.csv")

print(df.head())
```

### Step 3: Check the Dataset

```python
print("Dataset Shape:", df.shape)

print("\nColumn Names:")
print(df.columns)

print("\nMissing Values:")
print(df.isnull().sum())

print("\nDataset Information:")
df.info()
```

### Step 4: Calculate Average Scores

```python
score_columns = [
    "math score",
    "reading score",
    "writing score"
]

print(df[score_columns].mean())
```

### Step 5: Grouped Bar Chart by Parental Education

```python
parental_avg = df.groupby(
    "parental level of education"
)[score_columns].mean()

parental_avg.plot(
    kind="bar",
    figsize=(12, 6)
)

plt.title("Average Scores by Parental Education Level")
plt.xlabel("Parental Education Level")
plt.ylabel("Average Score")
plt.xticks(rotation=35, ha="right")
plt.tight_layout()
plt.show()
```

### Step 6: Grouped Bar Chart by Lunch Type

```python
lunch_avg = df.groupby("lunch")[score_columns].mean()

lunch_avg.plot(
    kind="bar",
    figsize=(8, 5)
)

plt.title("Average Scores by Lunch Type")
plt.xlabel("Lunch Type")
plt.ylabel("Average Score")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```

### Step 7: Box Plot for Test Preparation

```python
plt.figure(figsize=(8, 5))

sns.boxplot(
    data=df,
    x="test preparation course",
    y="math score"
)

plt.title("Mathematics Scores by Test Preparation")
plt.xlabel("Test Preparation Course")
plt.ylabel("Mathematics Score")

plt.tight_layout()
plt.show()
```

### Step 8: Scatter Plots for Subject Scores

```python
sns.pairplot(df[score_columns])

plt.show()
```

### Step 9: Correlation Heatmap

```python
correlation = df[score_columns].corr()

plt.figure(figsize=(7, 5))

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)

plt.title("Correlation Between Student Scores")

plt.tight_layout()
plt.show()
```

### Step 10: Compare Test Preparation Groups

```python
preparation_avg = df.groupby(
    "test preparation course"
)[score_columns].mean()

print(preparation_avg)
```

##  7. Detailed Python Code Explanation

### 7.1 Importing Libraries

```python
import pandas as pd
```

Pandas is used to load, organize, and analyze the dataset.

The name `pd` is a short name used to access Pandas functions.

```python
import numpy as np
```

NumPy is used for numerical calculations and working with numerical data.

```python
import matplotlib.pyplot as plt
```

Matplotlib is used to create charts and graphs.

The name `plt` makes it easier to call plotting functions.

```python
import seaborn as sns
```

Seaborn is used to create statistical charts such as box plots and correlation heatmaps.

The name `sns` is a short name used to access Seaborn functions.

### 7.2 Loading the Dataset

```python
df = pd.read_csv("StudentsPerformance.csv")
```

**Explanation:**

- `pd.read_csv()` reads the CSV file.
- `"StudentsPerformance.csv"` is the dataset filename.
- `df` is the variable that stores the dataset.
- The dataset is stored as a Pandas DataFrame.

A DataFrame is a table containing rows and columns, similar to an Excel spreadsheet.

The dataset must be available in the current working environment, and the filename must match.

```python
print(df.head())
```

The `head()` function displays the first five rows of the dataset.

It helps us check whether the dataset has loaded correctly.

### 7.3 Checking Dataset Information

```python
print(df.shape)
```

The `shape` property returns the number of rows and columns.

For this dataset, the expected result is:

```text
(1000, 8)
```

This means the dataset has 1,000 rows and 8 columns.

```python
print(df.isnull().sum())
```

- `isnull()` checks for missing values.
- `sum()` counts the missing values in each column.

This helps us understand whether the dataset contains incomplete information.

```python
df.info()
```

The `info()` function displays column names, data types, and the number of non-missing values.

### 7.4 Selecting Score Columns

```python
score_columns = [
    "math score",
    "reading score",
    "writing score"
]
```

This list stores the names of the three examination score columns.

We use this list to select the required columns without repeatedly typing their names.

### 7.5 Calculating Average Scores

```python
print(df[score_columns].mean())
```

**Explanation:**

- `df[score_columns]` selects the three score columns.
- `.mean()` calculates the average score for each subject.
- `print()` displays the calculated averages.

The average score is calculated by adding the values and dividing by the number of observations.

The overall averages in this dataset are approximately:

| Subject | Average Score |
|---|---:|
| Mathematics | 66.09 |
| Reading | 69.17 |
| Writing | 68.05 |

Reading has the highest average score among the three subjects.

### 7.6 Grouping Data by Parental Education

```python
parental_avg = df.groupby(
    "parental level of education"
)[score_columns].mean()
```

**Explanation:**

- `groupby()` divides students into groups according to parental education.
- `[score_columns]` selects Mathematics, Reading, and Writing.
- `.mean()` calculates the average score for each subject in each group.
- `parental_avg` stores the resulting table of averages.

This analysis helps us compare student performance across parental education categories.

### 7.7 Creating a Grouped Bar Chart

```python
parental_avg.plot(
    kind="bar",
    figsize=(12, 6)
)
```

**Explanation:**

- `plot()` creates a chart.
- `kind="bar"` selects a bar chart.
- `figsize=(12, 6)` sets the chart size.

A grouped bar chart displays multiple bars for each category. Here, the bars represent Mathematics, Reading, and Writing averages.

```python
plt.title("Average Scores by Parental Education Level")
```

This adds a title to the chart.

```python
plt.xlabel("Parental Education Level")
```

This labels the horizontal axis.

```python
plt.ylabel("Average Score")
```

This labels the vertical axis.

```python
plt.xticks(rotation=35, ha="right")
```

This rotates the category labels to make long labels easier to read.

```python
plt.tight_layout()
plt.show()
```

- `tight_layout()` helps prevent labels from overlapping.
- `show()` displays the chart.

### 7.8 Grouping Data by Lunch Type

```python
lunch_avg = df.groupby("lunch")[score_columns].mean()
```

This groups students according to lunch category and calculates the average scores for the three subjects.

```python
lunch_avg.plot(kind="bar", figsize=(8, 5))
```

This creates a grouped bar chart for comparing average scores across lunch categories.

The chart may help educators identify differences between groups and investigate whether students have equal access to learning resources.

However, the chart does not prove that lunch type causes score differences.

### 7.9 Understanding a Box Plot

```python
sns.boxplot(
    data=df,
    x="test preparation course",
    y="math score"
)
```

**Explanation:**

- `data=df` specifies the dataset.
- `x="test preparation course"` places preparation categories on the horizontal axis.
- `y="math score"` places Mathematics scores on the vertical axis.
- `sns.boxplot()` creates the box plot.

A box plot helps us understand:

- The median score.
- The spread of scores.
- The middle 50% of scores.
- Possible outliers.

The box plot helps compare the distribution of Mathematics scores between students who completed preparation and those who did not.

The same code can be used for Reading and Writing by changing the `y` column.

### 7.10 Understanding Scatter Plots

```python
sns.pairplot(df[score_columns])
```

The `pairplot()` function creates scatter plots for pairs of selected numerical columns.

Each dot represents a student's scores.

If the dots generally move upward from left to right, the two subjects tend to have a positive relationship.

For example, students with higher Reading scores often also have higher Writing scores in this dataset.

Scatter plots help us visually investigate relationships between subjects.

### 7.11 Understanding the Correlation Heatmap

```python
correlation = df[score_columns].corr()
```

The `.corr()` function calculates correlation coefficients between the selected numerical columns.

Correlation values range from -1 to +1.

- **+1:** Perfect positive linear relationship.
- **0:** No linear relationship.
- **-1:** Perfect negative linear relationship.

```python
sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)
```

**Explanation:**

- `correlation` provides the values displayed in the heatmap.
- `annot=True` displays the correlation numbers inside the cells.
- `cmap="coolwarm"` selects the color palette.
- `vmin=-1` sets the minimum value of the color scale.
- `vmax=1` sets the maximum value of the color scale.

The heatmap makes it easier to identify strong and weak relationships between the three subjects.

### 7.12 Comparing Test Preparation Groups

```python
preparation_avg = df.groupby(
    "test preparation course"
)[score_columns].mean()

print(preparation_avg)
```

This code groups students according to whether they completed the test preparation course.

It calculates and displays the average Mathematics, Reading, and Writing scores for each group.

In this dataset, students who completed test preparation had higher average scores in all three subjects.

This is an observed association. It does not prove that test preparation alone caused the difference.

---

## 8. Project Visualizations

### Average Scores by Parental Education

![Average Scores by Parental Education](images/average_scores_parental_education.png)

This chart compares average Mathematics, Reading, and Writing scores across parental education groups.

### Average Scores by Lunch Type

![Average Scores by Lunch Type](images/average_scores_lunch_type.png)

This chart compares average scores between lunch categories.

### Test Preparation Box Plots

![Test Preparation Box Plots](images/boxplots_test_preparation.png)

This chart shows the distribution of Mathematics scores according to test preparation status.

### Relationships Between Subject Scores

![Score Relationship Scatter Plots](images/score_relationship_scatterplots.png)

These scatter plots help us explore the relationships between Mathematics, Reading, and Writing scores.

### Correlation Heatmap

![Score Correlation Heatmap](images/score_correlation_heatmap.png)

This heatmap displays the correlation coefficients between the three examination subjects.

---

## 9. Key Findings

### Overall Average Scores

| Subject | Average Score |
|---|---:|
| Mathematics | 66.09 |
| Reading | 69.17 |
| Writing | 68.05 |

**Finding:** Reading has the highest overall average, while Mathematics has the lowest overall average.

### Test Preparation Results

| Subject | Preparation Completed | Preparation Not Completed |
|---|---:|---:|
| Mathematics | 69.70 | 64.08 |
| Reading | 73.89 | 66.53 |
| Writing | 74.42 | 64.50 |

**Finding:** Students who completed test preparation had higher average scores in all three subjects.

### Correlation Results

| Subject Relationship | Correlation |
|---|---:|
| Mathematics and Reading | 0.818 |
| Mathematics and Writing | 0.803 |
| Reading and Writing | 0.955 |

**Finding:** Reading and Writing have the strongest positive relationship among the three subject pairs.

---

##  13. Conclusion

The Student Performance Visualization, Demographic Analysis & Educational Insights project uses Python to analyze and visualize student examination scores.

It compares average scores across parental education and lunch categories, examines test preparation groups, and studies the relationships between Mathematics, Reading, and Writing.

The results show that Reading has the highest overall average score and that Reading and Writing have a strong positive correlation. Students who completed test preparation also had higher average scores in all three subjects in this dataset.

These findings can help educators identify areas for further investigation and consider ways to improve learning opportunities.

The main goal of this project is to use data responsibly to support better educational decisions and fairer learning opportunities.

---

##  Author

**Name:S.Naranjana**
**Course:BCA**


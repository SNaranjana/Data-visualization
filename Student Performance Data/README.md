##  Student Performance Data Understanding, Cleaning & Feature Engineering  ##
## 1. Project Overview

This project uses Python to understand, analyze, and process student performance data. It calculates statistical measures, creates new features such as Total Score and Percentage, and detects outliers in Mathematics, Reading, and Writing scores.

## 2. Objectives

* Understand the student dataset.
* Check missing values and dataset information.
* Calculate statistical measures.
* Create Total Score and Percentage.
* Detect outliers using the IQR method.
* Prepare the final dataset for further analysis.

## 3. Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Google Colab

## 4. Dataset

**File:** `StudentsPerformance (1).csv`

The dataset contains student details and marks in three subjects.

**Categorical Features:**

* Gender
* Race/Ethnicity
* Parental Level of Education
* Lunch
* Test Preparation Course

**Numerical Features:**

* Math Score
* Reading Score
* Writing Score

## 5. Code Explanation

### Step 1: Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

**Explanation:**

* Pandas is used for data analysis.
* NumPy is used for numerical operations.
* Matplotlib is used for creating graphs.
* Seaborn is used for statistical visualizations.

### Step 2: Load the Dataset

```python
df = pd.read_csv("/content/StudentsPerformance (1).csv")
df
```

**Explanation:**

Loads the CSV file into a DataFrame named `df` and displays the dataset.

### Step 3: Understand the Dataset

```python
df.info()
df.head()
df.tail()
df.describe()
df.columns
```

**Explanation:**

* `df.info()` – Displays dataset information.
* `df.head()` – Displays the first five rows.
* `df.tail()` – Displays the last five rows.
* `df.describe()` – Displays statistical summaries.
* `df.columns` – Displays column names.

### Step 4: Check Missing Values

```python
df.isnull().sum()
```

**Explanation:**

Checks the number of missing values in each column.

### Step 5: Select Subject Score Columns

```python
score_columns = [
    'math score',
    'reading score',
    'writing score'
]
score_columns
```

**Explanation:**

Selects the three subject score columns for statistical analysis.

### Step 6: Calculate Statistical Measures

```python
df[score_columns].mean()
df[score_columns].median()
df[score_columns].mode()
df[score_columns].std()
df[score_columns].quantile(0.25)
df[score_columns].quantile([0.5, 0.75])
```

**Explanation:**

* **Mean:** Calculates the average score.
* **Median:** Finds the middle score.
* **Mode:** Finds the most frequently occurring score.
* **Standard Deviation:** Measures the spread of scores.
* **Q1 (25%):** Finds the first quartile.
* **Q2 (50%):** Finds the median.
* **Q3 (75%):** Finds the third quartile.

### Step 7: Create Total Score

```python
df["Total Score"] = (
    df["math score"] +
    df["reading score"] +
    df["writing score"]
)
df
```

**Explanation:**

Adds the marks from all three subjects to calculate each student's total score. The maximum possible score is 300.

### Step 8: Calculate Percentage

```python
df["Percentage"] = (
    df["Total Score"] / 300
) * 100

df[["Total Score", "Percentage"]].head()
```

**Explanation:**

Calculates each student's percentage based on the maximum total score of 300.

**Formula:**

Percentage = (Total Score / 300) × 100

### Step 9: Detect Outliers Using IQR

```python
score_columns = [
    'math score',
    'reading score',
    'writing score'
]

for col in score_columns:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[
        (df[col] < lower) |
        (df[col] > upper)
    ]

    print("\n", col)
    print("Lower Limit:", lower)
    print("Upper Limit:", upper)
    print("Number of Outliers:", len(outliers))
```

**Explanation:**

Uses the Interquartile Range (IQR) method to detect extreme scores in each subject.

* **Q1:** First quartile.
* **Q3:** Third quartile.
* **IQR:** Difference between Q3 and Q1.
* **Lower Limit:** Q1 − 1.5 × IQR.
* **Upper Limit:** Q3 + 1.5 × IQR.
* **Outliers:** Scores below the lower limit or above the upper limit.

The code identifies and counts outliers but does not remove them.

### Step 10: Display the Final Dataset

```python
print("\nFinal Dataset:")
print(df.head())
```

**Explanation:**

Displays the first five rows of the final dataset, including the newly calculated Total Score and Percentage.

<img width="1328" height="622" alt="Screenshot 2026-09-29 092222" src="https://github.com/user-attachments/assets/05226d9f-c69e-4685-9f58-a10e9887a8bc" />
<img width="1330" height="392" alt="Screenshot 2026-09-29 092246" src="https://github.com/user-attachments/assets/0a2f6bb8-3394-443c-9f56-f760490afcc7" />
<img width="1325" height="327" alt="Screenshot 2026-09-29 092312" src="https://github.com/user-attachments/assets/5ce61c0d-71c4-4e91-bb89-832ac2031bf7" />
<img width="1338" height="331" alt="Screenshot 2026-09-29 092333" src="https://github.com/user-attachments/assets/9d70eff4-2510-4160-ad81-f3f3caa4dd6e" />
<img width="1326" height="588" alt="Screenshot 2026-09-29 092405" src="https://github.com/user-attachments/assets/22481a7c-8403-43b4-93cb-bbb25372dd28" />
<img width="1331" height="482" alt="Screenshot 2026-09-29 092428" src="https://github.com/user-attachments/assets/015c69d8-3f32-48e2-8225-9ab8f12d50b6" />
<img width="1328" height="493" alt="Screenshot 2026-09-29 092451" src="https://github.com/user-attachments/assets/48bd5ac6-8041-43bc-b4b0-e768095048c6" />
<img width="1327" height="562" alt="Screenshot 2026-09-29 092524" src="https://github.com/user-attachments/assets/f5405b23-4ad4-4237-81f4-19a6fb3436c9" />
<img width="1330" height="466" alt="Screenshot 2026-09-29 092612" src="https://github.com/user-attachments/assets/7ebf4b4e-c605-4599-8fcc-ad820393b242" />
<img width="1328" height="432" alt="Screenshot 2026-09-29 092548" src="https://github.com/user-attachments/assets/c3759fe1-9a6b-46bf-b9a2-6d5e17ff5a33" />
<img width="1326" height="483" alt="Screenshot 2026-09-29 092708" src="https://github.com/user-attachments/assets/21bcb5e3-7552-4b8c-aab1-1996f8724975" />
<img width="1530" height="737" alt="Screenshot 2026-09-29 092754" src="https://github.com/user-attachments/assets/62cf22a2-888d-488d-94c7-b06d67afe43d" />


## 8. Conclusion

This project demonstrates basic data understanding, statistical analysis, and feature engineering using Python. It calculates student scores and percentages, summarizes subject performance, and identifies extreme values using the IQR method. The resulting dataset can be used for further data visualization and student performance analysis.

## Author

**S. Naranjana**

  **BCA**


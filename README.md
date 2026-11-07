# Task 1: Data Cleaning and Preprocessing

## 1. Project Overview

**Dataset:** Customer Personality Analysis

**Objective:** Clean and prepare a raw dataset by identifying and handling missing values, checking duplicates, standardizing text values, converting date formats, renaming column headers, and verifying data types.

### Tools Used
- Python
- Pandas
- Google Colab

---

## 2. Dataset Information

The Customer Personality Analysis dataset was loaded into a Pandas DataFrame for cleaning and preprocessing.

| Description | Details |
|---|---|
| Total Rows | 2,240 |
| Total Columns | 29 |
| Missing Values (after cleaning) | 0 |
| Duplicate Rows (after cleaning) | 0 |

---

## 3. Data Cleaning Steps and Commands

### Step 1: Import Pandas and Load the Dataset

```python
import pandas as pd

df = pd.read_csv('/content/sample_data/marketing_campaign_copy.csv')
```

**Explanation:**
- `import pandas as pd` imports the Pandas library.
- `pd.read_csv()` reads the CSV file.
- The dataset is loaded into a DataFrame named `df`.

### Step 2: Inspect the Dataset

```python
df.info()
df.head()
df.shape
```

**Explanation:**
- `df.info()` displays column names, data types, and non-null values.
- `df.head()` displays the first five rows.
- `df.shape` returns the number of rows and columns.

### Step 3: Identify and Handle Missing Values

```python
df.isnull().sum()
```

**Explanation:**
- `isnull()` identifies missing values.
- `sum()` counts the missing values in each column.
- The original dataset contained 24 missing values in the `Income` column.

To handle the missing values:

```python
df['Income'] = df['Income'].fillna(df['Income'].median())
```

**Explanation:**
- `median()` calculates the median value of the Income column.
- `fillna()` replaces missing values with the calculated median.
- The updated values are assigned back to the `Income` column.

### Step 4: Check and Remove Duplicate Rows

```python
df.duplicated().sum()
```

**Explanation:**
- `duplicated()` identifies duplicate rows.
- `sum()` counts the number of duplicate rows.

To remove duplicate rows:

```python
df = df.drop_duplicates()
```

**Explanation:**
- `drop_duplicates()` removes duplicate records.
- The updated DataFrame is assigned back to `df`.
- Final validation confirmed that no duplicate rows remained.

### Step 5: Standardize Column Names

```python
df.columns = (
    df.columns.str.strip()
    .str.lower()
    .str.replace(' ', '_')
)
```

**Explanation:**
- `str.strip()` removes unwanted spaces from column names.
- `str.lower()` converts column names into lowercase.
- `str.replace(' ', '_')` replaces spaces with underscores.

**Examples:**

| Original Column | Updated Column |
|---|---|
| Year_Birth | year_birth |
| Marital_Status | marital_status |
| Dt_Customer | dt_customer |

### Step 6: Standardize Text Values

First, inspect the categorical columns:

```python
df['education'].value_counts(dropna=False)

df['marital_status'].value_counts(dropna=False)
```

**Explanation:**
- `value_counts()` counts the occurrences of each category.
- `dropna=False` includes missing values in the count.

Remove unwanted leading and trailing spaces:

```python
df['education'] = df['education'].str.strip()

df['marital_status'] = df['marital_status'].str.strip()
```

**Explanation:**
- `str.strip()` removes unnecessary spaces from text values.
- Existing category names are preserved.

### Step 7: Convert Date Column to Datetime

```python
df['dt_customer'] = pd.to_datetime(
    df['dt_customer'],
    format='%Y-%m-%d'
)
```

**Explanation:**
- `pd.to_datetime()` converts date values into a Pandas datetime format.
- `format='%Y-%m-%d'` specifies the year-month-day date format.
- The column is converted from `object` to `datetime64[ns]`.

Verify the date data type:

```python
print(df['dt_customer'].dtype)
```

**Output:**

```text
datetime64[ns]
```

### Step 8: Check Data Types

```python
df.dtypes
```

**Explanation:**
- Displays the data type of every column.
- Numeric columns are stored as `int64` or `float64`.
- Text columns are stored as `object`.
- The date column is stored as `datetime64[ns]`.

### Step 9: Final Dataset Validation

```python
print("Dataset Shape:", df.shape)

print("Missing Values:", df.isnull().sum().sum())

print("Duplicate Rows:", df.duplicated().sum())

print("\nColumn Data Types:")

print(df.dtypes)

print("\nDate Column Type:")

print(df['dt_customer'].dtype)
```

**Explanation:**
- `df.shape` checks the final dataset dimensions.
- `df.isnull().sum().sum()` counts all missing values.
- `df.duplicated().sum()` counts remaining duplicate rows.
- `df.dtypes` displays the final column data types.

**Final Output:**

```text
Dataset Shape: (2240, 29)
Missing Values: 0
Duplicate Rows: 0
Date Column Type: datetime64[ns]
```

### Step 10: Export the Cleaned Dataset

```python
df.to_csv('cleaned_customer_data.csv', index=False)
```

**Explanation:**
- `to_csv()` exports the cleaned DataFrame into a CSV file.
- `index=False` prevents Pandas from adding an extra index column.
- The cleaned dataset is saved as `cleaned_customer_data.csv`.

---

## 4. Summary of Changes

The following preprocessing operations were performed:

1. Loaded the raw dataset using Pandas.
2. Identified 24 missing values in the `Income` column and handled them using the median.
3. Checked for duplicate records and applied duplicate removal.
4. Standardized column names by converting them to lowercase and replacing spaces with underscores.
5. Inspected categorical text values and removed unnecessary leading and trailing spaces.
6. Converted the `dt_customer` column into a datetime data type.
7. Checked and verified the data types of all columns.
8. Validated the cleaned dataset to confirm that no missing values or duplicate rows remained.
9. Exported the final cleaned dataset as a CSV file.

---

## 5. Final Dataset Results

| Validation | Final Result |
|---|---:|
| Total Rows | 2,240 |
| Total Columns | 29 |
| Missing Values | 0 |
| Duplicate Rows | 0 |
| Date Data Type | datetime64[ns] |

---

## 6. Conclusion

The Customer Personality Analysis dataset was successfully cleaned and preprocessed using Python and Pandas.

The final dataset contains 2,240 rows and 29 columns, with no missing values or duplicate rows. Column names have been standardized, and the customer date column has been converted into the appropriate datetime data type.

The cleaned dataset is ready for further data analysis and visualization.

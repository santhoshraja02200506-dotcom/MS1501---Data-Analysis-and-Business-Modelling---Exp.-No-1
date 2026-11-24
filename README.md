# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program & Output
# Experiment No. 1: Data Cleaning and Preprocessing

## Code

```python
# Data Cleaning and Preprocessing on the Heart Disease Dataset

# Step 1: Import essential libraries
import pandas as pd
import numpy as np

pd.set_option("display.max_columns", None)
pd.set_option("display.width", 250)

# Step 2: Load the dataset
df = pd.read_csv("heartdisease.csv")
print("Dataset loaded successfully.")

# Step 3: View structure, data types and memory usage
print("\nShape of dataset:", df.shape)
print("\nColumn names:", list(df.columns))
print("\nDataset Info:")
df.info()
print("\nData types:")
print(df.dtypes)
print("\nData type of 'Age':", df["Age"].dtype)

# Step 4: Check for missing values and duplicates
print("\nMissing values per column:")
print(df.isnull().sum())
print("\nDuplicate rows:", df.duplicated().sum())

# Handle missing values and duplicates (no action needed if none are found)
df = df.dropna()
df = df.drop_duplicates()
print("Shape after dropna() and drop_duplicates():", df.shape)

# Step 5: Summary statistics
print("\nSummary statistics:")
print(df.describe())

# Step 6: First and last records
print("\nFirst 5 records:")
print(df.head())
print("\nLast 5 records:")
print(df.tail())

# Step 7: Sort and group the data
print("\nTop 5 patients by Age (descending):")
print(df.sort_values(by="Age", ascending=False).head())

print("\nSorted by Gender (A-Z) and then Age (descending), first 5 rows:")
print(df.sort_values(by=["Gender", "Age"], ascending=[True, False]).head())

group_cols = ["Age", "SysBP", "BMI", "Glucose"]
print("\nGroup by TenYearCHD - mean:")
print(df.groupby("TenYearCHD")[group_cols].mean())
print("\nGroup by TenYearCHD - median:")
print(df.groupby("TenYearCHD")[group_cols].median())
print("\nGroup by Gender - sum of TenYearCHD (number of CHD cases):")
print(df.groupby("Gender")["TenYearCHD"].sum())
print("\nGroup by Gender - max:")
print(df.groupby("Gender")[group_cols].max())
print("\nGroup by Gender - min:")
print(df.groupby("Gender")[group_cols].min())

print("\nMean of all numeric columns:")
print(df.mean(numeric_only=True))

# Step 8: Rename columns for consistency
df = df.rename(columns={
    "S. No": "S_No",
    "currentsmoker": "CurrentSmoker",
    "Cigsperday": "CigsPerDay",
    "Prevalentstroke": "PrevalentStroke",
    "Totalcholestrol": "TotalCholesterol",
    "Heartrate": "HeartRate"
})
print("\nColumns after renaming:")
print(list(df.columns))

# Step 9: Save the cleaned dataset
df.to_csv("heartdisease_cleaned.csv", index=False)
print("\nCleaned dataset saved as 'heartdisease_cleaned.csv'. Final shape:", df.shape)
```
Output:

Dataset loaded successfully.

Shape of dataset: (250, 17)

Column names: ['S. No', 'Gender', 'Age', 'Education', 'currentsmoker', 'Cigsperday', 'BPMeds', 'Prevalentstroke', 'PrevalentHyp', 'Diabetes', 'Totalcholestrol', 'SysBP', 'DiaBP', 'BMI', 'Heartrate', 'Glucose', 'TenYearCHD']

Dataset Info:
<class 'pandas.DataFrame'>
RangeIndex: 250 entries, 0 to 249
Data columns (total 17 columns):
 #   Column           Non-Null Count  Dtype  
---  ------           --------------  -----  
 0   S. No            250 non-null    int64  
 1   Gender           250 non-null    str    
 2   Age              250 non-null    int64  
 3   Education        250 non-null    int64  
 4   currentsmoker    250 non-null    int64  
 5   Cigsperday       250 non-null    int64  
 6   BPMeds           250 non-null    int64  
 7   Prevalentstroke  250 non-null    int64  
 8   PrevalentHyp     250 non-null    int64  
 9   Diabetes         250 non-null    int64  
 10  Totalcholestrol  250 non-null    int64  
 11  SysBP            250 non-null    float64
 12  DiaBP            250 non-null    float64
 13  BMI              250 non-null    float64
 14  Heartrate        250 non-null    int64  
 15  Glucose          250 non-null    int64  
 16  TenYearCHD       250 non-null    int64  
dtypes: float64(3), int64(13), str(1)
memory usage: 33.3 KB

Data types:
S. No                int64
Gender                 str
Age                  int64
Education            int64
currentsmoker        int64
Cigsperday           int64
BPMeds               int64
Prevalentstroke      int64
PrevalentHyp         int64
Diabetes             int64
Totalcholestrol      int64
SysBP              float64
DiaBP              float64
BMI                float64
Heartrate            int64
Glucose              int64
TenYearCHD           int64
dtype: object

Data type of 'Age': int64

Missing values per column:
S. No              0
Gender             0
Age                0
Education          0
currentsmoker      0
Cigsperday         0
BPMeds             0
Prevalentstroke    0
PrevalentHyp       0
Diabetes           0
Totalcholestrol    0
SysBP              0
DiaBP              0
BMI                0
Heartrate          0
Glucose            0
TenYearCHD         0
dtype: int64

Duplicate rows: 0
Shape after dropna() and drop_duplicates(): (250, 17)

Summary statistics:
            S. No         Age  Education  currentsmoker  Cigsperday      BPMeds  Prevalentstroke  PrevalentHyp    Diabetes  Totalcholestrol      SysBP       DiaBP         BMI   Heartrate     Glucose  TenYearCHD
count  250.000000  250.000000  250.00000     250.000000  250.000000  250.000000       250.000000    250.000000  250.000000       250.000000  250.00000  250.000000  250.000000  250.000000  250.000000  250.000000
mean   125.500000   50.088000    2.48000       0.456000    6.688000    0.108000         0.024000      0.256000    0.080000       235.192000  129.42760   83.491200   26.288400   84.220000   88.012000    0.184000
std     72.312977   12.268755    1.08735       0.499059    9.368336    0.311003         0.153356      0.437297    0.271837        37.276498   18.92353   11.649065    4.588731   16.377438   24.685407    0.388261
min      1.000000   30.000000    1.00000       0.000000    0.000000    0.000000         0.000000      0.000000    0.000000       120.000000   85.00000   55.600000   16.000000   55.000000   45.000000    0.000000
25%     63.250000   38.250000    2.00000       0.000000    0.000000    0.000000         0.000000      0.000000    0.000000       207.250000  118.02500   74.425000   23.200000   71.000000   72.000000    0.000000
50%    125.500000   51.500000    2.00000       0.000000    0.000000    0.000000         0.000000      0.000000    0.000000       237.500000  129.10000   84.050000   25.950000   86.000000   89.000000    0.000000
75%    187.750000   61.000000    3.00000       1.000000   12.000000    0.000000         0.000000      1.000000    0.000000       260.750000  141.75000   91.475000   29.375000   99.000000  103.000000    0.000000
max    250.000000   70.000000    4.00000       1.000000   30.000000    1.000000         1.000000      1.000000    1.000000       320.000000  180.90000  114.100000   41.700000  110.000000  163.000000    1.000000

First 5 records:
   S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP   BMI  Heartrate  Glucose  TenYearCHD
0      1  Female   68          1              1           3       0                1             0         0              237  107.8   71.2  30.9         81       70           0
1      2  Female   58          4              1           1       0                0             0         0              268  113.2   94.7  26.8        108       58           0
2      3    Male   44          2              1           6       0                0             0         0              192  132.7   94.8  30.3        104      141           0
3      4    Male   37          4              1          18       0                0             0         0              250  132.3   74.4  25.8         89      120           0
4      5  Female   50          1              1          24       0                1             0         0              202   97.5  102.6  22.2        106       84           1

Last 5 records:
     S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP   BMI  Heartrate  Glucose  TenYearCHD
245    246    Male   32          3              1          11       0                0             0         0              232  133.3   84.2  32.6         64      106           0
246    247  Female   49          3              1          27       1                0             0         0              185  136.5   85.4  22.3         94       58           0
247    248    Male   53          4              0           0       0                0             0         0              195  122.8  100.8  29.1        101       94           0
248    249    Male   62          1              1          27       0                0             0         0              246  142.6   80.0  25.9         96      123           0
249    250    Male   53          3              0           0       0                0             0         0              264  116.9   66.2  35.5         55       82           0

Top 5 patients by Age (descending):
     S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP   BMI  Heartrate  Glucose  TenYearCHD
94      95    Male   70          4              0           0       0                0             0         0              199  144.5   87.1  25.9         69       59           0
75      76  Female   70          3              1          29       0                0             0         0              219  115.7   72.9  24.4         79       68           0
217    218    Male   70          1              1          23       0                0             0         0              256  112.0   62.9  27.6         68      120           0
241    242  Female   70          4              1          27       1                0             0         0              204  131.7   73.4  32.9         87       92           0
156    157    Male   70          4              1           5       0                0             0         0              253  146.2   89.8  36.3         90      120           0

Sorted by Gender (A-Z) and then Age (descending), first 5 rows:
     S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP   BMI  Heartrate  Glucose  TenYearCHD
75      76  Female   70          3              1          29       0                0             0         0              219  115.7   72.9  24.4         79       68           0
170    171  Female   70          3              0           0       0                0             1         0              181  146.0   85.5  27.9         89       89           1
241    242  Female   70          4              1          27       1                0             0         0              204  131.7   73.4  32.9         87       92           0
12      13  Female   69          2              1           8       0                0             1         0              233  168.9   61.7  16.0         63      112           0
219    220  Female   69          3              1           8       0                0             0         0              273  106.4   98.2  23.2        101       63           0

Group by TenYearCHD - mean:
                  Age       SysBP        BMI    Glucose
TenYearCHD                                             
0           49.887255  128.403431  26.230392  88.196078
1           50.978261  133.969565  26.545652  87.195652

Group by TenYearCHD - median:
             Age   SysBP    BMI  Glucose
TenYearCHD                                             
0           51.0  127.85  25.80     89.0
1           52.5  134.40  26.35     89.0

Group by Gender - sum of TenYearCHD (number of CHD cases):
Gender
Female    24
Male      22
Name: TenYearCHD, dtype: int64

Group by Gender - max:
        Age  SysBP   BMI  Glucose
Gender                                
Female   70  177.3  37.0      146
Male     70  180.9  41.7      163

Group by Gender - min:
        Age  SysBP   BMI  Glucose
Gender                                
Female   30   85.0  16.0       45
Male     30   85.0  16.0       45

Mean of all numeric columns:
S. No              125.5000
Age                 50.0880
Education            2.4800
currentsmoker        0.4560
Cigsperday           6.6880
BPMeds               0.1080
Prevalentstroke      0.0240
PrevalentHyp         0.2560
Diabetes             0.0800
Totalcholestrol    235.1920
SysBP              129.4276
DiaBP               83.4912
BMI                 26.2884
Heartrate           84.2200
Glucose             88.0120
TenYearCHD           0.1840
dtype: float64

Columns after renaming:
['S_No', 'Gender', 'Age', 'Education', 'CurrentSmoker', 'CigsPerDay', 'BPMeds', 'PrevalentStroke', 'PrevalentHyp', 'Diabetes', 'TotalCholesterol', 'SysBP', 'DiaBP', 'BMI', 'HeartRate', 'Glucose', 'TenYearCHD']

Cleaned dataset saved as 'heartdisease_cleaned.csv'. Final shape: (250, 17)
```

## Result

Thus, data cleaning and preprocessing on the heart disease dataset (`heartdisease.csv`) was executed successfully, and the cleaned dataset was saved as `heartdisease_cleaned.csv`.

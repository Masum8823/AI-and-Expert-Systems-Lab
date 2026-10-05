# AI Lab 01 Home Work – Diabetes Dataset Analysis

## 1. Lab Homework Overview

এই Lab-এ আমরা **Pima Indians Diabetes Dataset** নিয়ে কাজ করেছি।

এই Lab-এর মূল কাজগুলো হলো:

* Dataset load করা
* Dataset-এর information দেখা
* Statistical summary বের করা
* Missing values check করা
* Invalid `0` values-কে median দিয়ে replace করা
* Duplicate records খুঁজে বের করা
* Duplicate records remove করা
* Numerical features normalize করা
* Categorical variable encode করা
* নির্দিষ্ট condition অনুযায়ী patient filter করা
* বিভিন্ন graph দিয়ে dataset visualize করা

---

# 2. Dataset কী?

Dataset হলো অনেকগুলো related data-এর collection।

এই Lab-এ প্রতিটি row একজন patient-এর information প্রকাশ করে এবং প্রতিটি column একটি feature প্রকাশ করে।

### Dataset-এর Columns

| Column                     | Meaning                                    |
| -------------------------- | ------------------------------------------ |
| `Pregnancies`              | কতবার pregnancy হয়েছে                      |
| `Glucose`                  | Blood glucose level                        |
| `BloodPressure`            | Blood pressure                             |
| `SkinThickness`            | Skin thickness                             |
| `Insulin`                  | Insulin level                              |
| `BMI`                      | Body Mass Index                            |
| `DiabetesPedigreeFunction` | Diabetes-এর genetic/family-related measure |
| `Age`                      | Patient-এর বয়স                             |
| `Outcome`                  | Diabetes আছে কি না                         |

### Outcome

```text
0 → No Diabetes
1 → Diabetes
```

---

# 3. Required Python Libraries

এই Lab-এ কয়েকটি গুরুত্বপূর্ণ Python library ব্যবহার করা হয়েছে।

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.preprocessing import MinMaxScaler, LabelEncoder
```

### Pandas

```python
import pandas as pd
```

Pandas মূলত **data handling এবং data analysis** করার জন্য ব্যবহার করা হয়।

যেমন:

* Dataset load করা
* DataFrame তৈরি করা
* Row/column select করা
* Missing values check করা
* Duplicate remove করা

---

### NumPy

```python
import numpy as np
```

NumPy numerical calculation-এর জন্য ব্যবহৃত হয়।

---

### Matplotlib

```python
import matplotlib.pyplot as plt
```

Matplotlib দিয়ে বিভিন্ন ধরনের graph তৈরি করা যায়।

যেমন:

* Histogram
* Line plot
* Scatter plot

---

### Seaborn

```python
import seaborn as sns
```

Seaborn মূলত সুন্দর এবং সহজে statistical visualization তৈরি করতে ব্যবহৃত হয়।

যেমন:

* Box plot
* Heatmap
* KDE plot
* Scatter plot

---

### MinMaxScaler

```python
from sklearn.preprocessing import MinMaxScaler
```

Numerical data-কে সাধারণত `0` থেকে `1` range-এর মধ্যে আনার জন্য ব্যবহার করা হয়।

---

### LabelEncoder

```python
from sklearn.preprocessing import LabelEncoder
```

Categorical value-কে numerical value-তে convert করার জন্য ব্যবহার করা হয়।

---

# 4. Load Dataset

Dataset একটি URL থেকে load করা হয়েছে।

```python
dataset_url = "https://raw.githubusercontent.com/jbrownlee/Datasets/master/pima-indians-diabetes.data.csv"
```

তারপর column names define করা হয়েছে।

```python
column_names = [
    "Pregnancies", "Glucose", "BloodPressure", "SkinThickness",
    "Insulin", "BMI", "DiabetesPedigreeFunction", "Age", "Outcome"
]
```

Dataset load:

```python
diabetes = pd.read_csv(dataset_url, names=column_names)
```

### এখানে কী হচ্ছে?

`pd.read_csv()` CSV file read করে DataFrame তৈরি করছে।

`names=column_names` ব্যবহার করা হয়েছে কারণ dataset-এর original file-এ column names নেই।

---

# 5. DataFrame কী?

Pandas-এর সবচেয়ে গুরুত্বপূর্ণ data structure হলো **DataFrame**।

সহজভাবে বললে:

> DataFrame হলো table-এর মতো structure যেখানে rows এবং columns থাকে।

Example:

```text
Pregnancies  Glucose  BMI   Age   Outcome
2            120      30    25    0
5            150      35    45    1
```

এখানে প্রতিটি row একটি patient এবং প্রতিটি column একটি feature।

---

# 6. Display First Five Records

প্রথম ৫টি row দেখতে:

```python
print(diabetes.head())
```

### `head()`

```python
df.head()
```

Defaultভাবে প্রথম ৫টি row দেখায়।

নির্দিষ্ট সংখ্যক row চাইলে:

```python
df.head(10)
```

এটি প্রথম ১০টি row দেখাবে।

### মনে রাখবে

```text
head() → প্রথম কয়েকটি row
```

---

# 7. Dataset Information

Dataset সম্পর্কে basic information দেখতে:

```python
print(diabetes.info())
```

`info()` থেকে সাধারণত জানা যায়:

* Number of rows
* Number of columns
* Column names
* Data types
* Non-null values
* Memory usage

### কেন দরকার?

Dataset-এর structure বোঝার জন্য।

---

# 8. Statistical Summary

Dataset-এর numerical columns-এর basic statistics দেখতে:

```python
print(diabetes.describe())
```

`describe()` সাধারণত দেখায়:

* Count
* Mean
* Standard deviation
* Minimum
* 25% value
* 50% value / Median
* 75% value
* Maximum

### গুরুত্বপূর্ণ

```text
describe() → Statistical Summary
```

---

# 9. Missing Values Check

প্রতিটি column-এ কতগুলো actual null/missing value আছে তা দেখতে:

```python
print(diabetes.isnull().sum())
```

### Breakdown

```python
diabetes.isnull()
```

Missing value থাকলে `True` এবং না থাকলে `False` দেয়।

তারপর:

```python
.sum()
```

দিয়ে প্রতিটি column-এর missing value count করা হয়।

### মনে রাখবে

```text
isnull() → Missing value check
sum()    → কতগুলো missing value আছে তা count
```

---

# 10. Important Concept: Zero vs Missing Value

এই dataset-এ কিছু medical feature-এর value `0` দেওয়া আছে।

কিন্তু কিছু ক্ষেত্রে `0` বাস্তব measurement হিসেবে meaningful নয়।

যেমন:

* Glucose = 0
* BloodPressure = 0
* BMI = 0

এগুলো বাস্তব medical measurement হিসেবে invalid হতে পারে।

তাই এই columns-এর `0` values-কে missing/invalid value হিসেবে treat করা হয়েছে।

---

# 11. Pregnancies কেন বাদ দেওয়া হয়েছে?

`Pregnancies` column-এ `0` একটি valid value।

এর অর্থ হতে পারে:

```text
Pregnancies = 0
```

অর্থাৎ patient-এর কোনো pregnancy হয়নি।

তাই `Pregnancies` column-এর `0` পরিবর্তন করা হয়নি।

---

# 12. Replace Zero Values with Median

যে columns-এ `0` invalid হিসেবে ধরা হয়েছে:

```python
zero_missing_columns = [
    "Glucose",
    "BloodPressure",
    "SkinThickness",
    "Insulin",
    "BMI"
]
```

তারপর প্রতিটি column-এর median বের করে `0` replace করা হয়েছে।

```python
for col in zero_missing_columns:
    median = diabetes[col].median()
    diabetes[col] = diabetes[col].replace(0, median)
```

### এখানে কী হচ্ছে?

ধরো:

```text
Glucose:
100
120
0
140
```

এখানে `0` invalid হলে:

```text
median = 120
```

তাহলে:

```text
100
120
120
140
```

হয়ে যাবে।

---

# 13. Median কী?

Median হলো sorted data-এর middle value।

Example:

```text
10, 20, 30, 40, 50
```

এখানে median:

```text
30
```

আর even number of values হলে মাঝের দুইটির average নেওয়া হয়।

### কেন Median ব্যবহার করা হয়েছে?

এই Lab-এ invalid zero values replace করার জন্য median ব্যবহার করা হয়েছে।

---

# 14. Duplicate Records

Duplicate row মানে একই ধরনের record একাধিকবার থাকা।

Duplicate check:

```python
duplicate_count = diabetes.duplicated().sum()
```

এখানে:

```python
duplicated()
```

duplicate row identify করে।

আর:

```python
sum()
```

duplicate row-এর সংখ্যা count করে।

---

# 15. Display Duplicate Records

Duplicate records দেখতে:

```python
print(diabetes[diabetes.duplicated()])
```

এতে duplicate rows display হবে।

---

# 16. Remove Duplicate Records

Duplicate records remove করতে:

```python
diabetes.drop_duplicates(inplace=True)
```

### `drop_duplicates()`

Dataset থেকে duplicate rows remove করে।

### `inplace=True`

এর অর্থ হলো original DataFrame-এই পরিবর্তন করা হবে।

---

# 17. Dataset Shape

Duplicate remove করার পর dataset-এর size দেখতে:

```python
print(diabetes.shape)
```

`shape` সাধারণত:

```text
(rows, columns)
```

format-এ result দেয়।

Example:

```text
(700, 9)
```

মানে:

```text
700 rows
9 columns
```

---

# 18. Normalization

Normalization হলো numerical values-কে একটি নির্দিষ্ট range-এর মধ্যে নিয়ে আসা।

এই Lab-এ:

```text
Glucose
BMI
Age
```

এই তিনটি feature normalize করা হয়েছে।

Target range:

```text
0 to 1
```

---

# 19. কেন Normalization করা হয়?

ধরো:

```text
Glucose → 50–200
BMI     → 15–50
Age     → 20–80
```

তাহলে featureগুলোর range আলাদা।

Normalization করলে:

```text
Glucose → 0–1
BMI     → 0–1
Age     → 0–1
```

হয়ে যায়।

এতে numerical features একই scale-এ আসে।

---

# 20. Min-Max Scaler

Normalization-এর জন্য ব্যবহার করা হয়েছে:

```python
normalizer = MinMaxScaler()
```

Selected features:

```python
features = ["Glucose", "BMI", "Age"]
```

তারপর:

```python
normalized_data = diabetes.copy()
```

Original dataset-এর copy তৈরি করা হয়েছে।

তারপর:

```python
normalized_data[features] = normalizer.fit_transform(
    diabetes[features]
)
```

দিয়ে normalization করা হয়েছে।

---

# 21. `fit_transform()` কী?

```python
fit_transform()
```

দুইটি কাজ একসাথে করে:

```text
fit       → data থেকে প্রয়োজনীয় information শেখে
transform → সেই information ব্যবহার করে data transform করে
```

এই Lab-এ:

```python
normalizer.fit_transform(diabetes[features])
```

ব্যবহার করা হয়েছে।

---

# 22. Encoding

Encoding হলো categorical data-কে numerical form-এ convert করা।

এই Lab-এ `Outcome` column encode করা হয়েছে।

```python
encoded_data = diabetes.copy()
```

তারপর:

```python
label_encoder = LabelEncoder()
```

এবং:

```python
encoded_data["Outcome"] = label_encoder.fit_transform(
    encoded_data["Outcome"]
)
```

---

# 23. LabelEncoder

`LabelEncoder` categorical values-কে numerical values-এ convert করে।

Example:

```text
No Diabetes
Diabetes
```

এর বদলে numerical representation হতে পারে:

```text
0
1
```

এই dataset-এ `Outcome` আগে থেকেই `0` এবং `1`, তাই encoding করার ফলে values একই numerical form-এ থাকে।

### Important

এই Lab-এর code অনুযায়ী `LabelEncoder` ব্যবহার করা হয়েছে।

---

# 24. Filtering Data

Filtering মানে নির্দিষ্ট condition অনুযায়ী dataset থেকে কিছু rows বের করা।

Task:

> Outcome = 1 এবং Age > 40

Code:

```python
selected_patients = diabetes[
    (diabetes["Outcome"] == 1) &
    (diabetes["Age"] > 40)
]
```

---

# 25. Filtering Condition বুঝি

প্রথম condition:

```python
diabetes["Outcome"] == 1
```

মানে:

```text
Patient diabetic কি না
```

দ্বিতীয় condition:

```python
diabetes["Age"] > 40
```

মানে:

```text
Patient-এর বয়স 40-এর বেশি কি না
```

দুই condition-এর মধ্যে:

```python
&
```

ব্যবহার করা হয়েছে।

`&` মানে:

```text
AND
```

অর্থাৎ দুই condition-ই true হতে হবে।

---

# 26. Outcome Labels for Visualization

Graph-এ `0` এবং `1` দেখানোর পরিবর্তে readable name ব্যবহার করা হয়েছে।

```python
visual_data = diabetes.copy()
```

তারপর:

```python
visual_data["Diabetes_Status"] = visual_data["Outcome"].map({
    0: "No Diabetes",
    1: "Diabetes"
})
```

এখন:

```text
0 → No Diabetes
1 → Diabetes
```

হিসেবে graph-এ দেখা যাবে।

---

# 27. Data Visualization

Data visualization হলো graph ব্যবহার করে dataset-এর information বোঝানো।

এই Lab-এ ৫ ধরনের visualization করা হয়েছে:

1. Histogram
2. Box Plot
3. Correlation Heatmap
4. KDE Plot
5. Scatter Plot

---

# 28. Histogram

### Task

**Histogram of Blood Glucose Levels**

Code:

```python
plt.figure(figsize=(9, 5))

plt.hist(
    diabetes["Glucose"],
    bins=15,
    edgecolor="black"
)

plt.title("Blood Glucose Level Distribution")
plt.xlabel("Glucose Level")
plt.ylabel("Frequency")

plt.show()
```

---

# 29. Histogram কী দেখায়?

Histogram কোনো numerical data-এর distribution দেখায়।

এই Lab-এ:

```text
X-axis → Glucose Level
Y-axis → Frequency
```

অর্থাৎ কোন range-এর glucose level কতজন patient-এর আছে তা বোঝা যায়।

### `bins`

```python
bins=15
```

Data-কে 15টি interval/group-এ ভাগ করতে সাহায্য করে।

---

# 30. Box Plot

### Task

**Box Plot of BMI by Diabetes Outcome**

Code:

```python
sns.boxplot(
    data=visual_data,
    x="Diabetes_Status",
    y="BMI"
)
```

---

# 31. Box Plot কী দেখায়?

Box plot ব্যবহার করে কোনো numerical data-এর:

* Median
* Spread
* Distribution
* Possible outliers

সম্পর্কে ধারণা পাওয়া যায়।

এই Lab-এ BMI compare করা হয়েছে:

```text
No Diabetes
vs
Diabetes
```

---

# 32. Correlation

Correlation হলো দুইটি numerical variable-এর মধ্যে relationship-এর strength এবং direction বোঝার একটি measure।

Correlation value সাধারণত:

```text
-1 থেকে +1
```

এর মধ্যে থাকে।

### Positive Correlation

```text
+1 এর কাছাকাছি
```

একটি value বাড়লে অন্যটিও বাড়ার tendency থাকে।

### Negative Correlation

```text
-1 এর কাছাকাছি
```

একটি value বাড়লে অন্যটি কমার tendency থাকে।

### Near Zero

```text
0 এর কাছাকাছি
```

দুই variable-এর মধ্যে strong linear relationship কম।

---

# 33. Correlation Heatmap

Code:

```python
corr_matrix = encoded_data.corr()
```

এটি numerical columns-এর correlation matrix তৈরি করে।

তারপর:

```python
sns.heatmap(
    corr_matrix,
    annot=True,
    fmt=".2f",
    cmap="viridis"
)
```

দিয়ে heatmap তৈরি করা হয়েছে।

---

# 34. Heatmap-এর `annot=True`

```python
annot=True
```

দিলে প্রতিটি cell-এর মধ্যে correlation value দেখা যায়।

Example:

```text
0.45
-0.20
0.78
```

---

# 35. Heatmap-এর `fmt=".2f"`

```python
fmt=".2f"
```

মানে value দুই decimal place পর্যন্ত দেখানো হবে।

Example:

```text
0.4567
```

হয়ে যাবে:

```text
0.46
```

---

# 36. KDE Plot

### Task

**Age Distribution of Diabetic vs Non-Diabetic Patients**

KDE-এর full form:

> Kernel Density Estimate

KDE plot data-এর distribution-এর smooth curve দেখায়।

Code:

```python
sns.kdeplot(
    data=visual_data[visual_data["Outcome"] == 0],
    x="Age",
    label="Non-Diabetic",
    fill=True
)
```

এবং diabetic patients-এর জন্য:

```python
sns.kdeplot(
    data=visual_data[visual_data["Outcome"] == 1],
    x="Age",
    label="Diabetic",
    fill=True
)
```

---

# 37. KDE Plot কেন ব্যবহার করা হয়েছে?

এই graph দিয়ে দেখা যায়:

```text
Diabetic patients-এর age distribution
vs
Non-diabetic patients-এর age distribution
```

অর্থাৎ দুই group-এর age distribution compare করা যায়।

---

# 38. Scatter Plot

### Task

**Scatter Plot of Glucose vs BMI**

Code:

```python
sns.scatterplot(
    data=diabetes,
    x="Glucose",
    y="BMI",
    hue="Outcome"
)
```

---

# 39. Scatter Plot কী দেখায়?

Scatter plot দুইটি numerical variable-এর relationship visualize করে।

এই Lab-এ:

```text
X-axis → Glucose
Y-axis → BMI
```

এবং:

```python
hue="Outcome"
```

ব্যবহার করে diabetes outcome অনুযায়ী points আলাদা করা হয়েছে।

---

# 40. `hue` কী?

Seaborn-এর:

```python
hue="Outcome"
```

এর মাধ্যমে Outcome-এর value অনুযায়ী data points আলাদা করা হয়।

অর্থাৎ:

```text
Outcome = 0
Outcome = 1
```

দুই group আলাদা করে দেখা যায়।

---

# 41. `plt.figure(figsize=...)`

Example:

```python
plt.figure(figsize=(9, 5))
```

Graph-এর size নির্ধারণ করতে ব্যবহার করা হয়।

এখানে:

```text
9 → width
5 → height
```

---

# 42. `plt.xlabel()` এবং `plt.ylabel()`

X-axis-এর নাম:

```python
plt.xlabel("Glucose Level")
```

Y-axis-এর নাম:

```python
plt.ylabel("Frequency")
```

---

# 43. `plt.title()`

Graph-এর title দেওয়ার জন্য:

```python
plt.title("Blood Glucose Level Distribution")
```

ব্যবহার করা হয়।

---

# 44. `plt.show()`

Graph display করার জন্য:

```python
plt.show()
```

ব্যবহার করা হয়।

---

# 45. Complete Workflow

এই Lab-এর পুরো workflow:

```text
Load Dataset
     ↓
Check Dataset Information
     ↓
Check Statistics
     ↓
Check Missing Values
     ↓
Replace Invalid Zero Values
     ↓
Check Duplicate Records
     ↓
Remove Duplicates
     ↓
Normalize Selected Features
     ↓
Encode Outcome
     ↓
Filter Required Patients
     ↓
Prepare Data for Visualization
     ↓
Create Graphs
     ↓
Analyze Dataset
```

---

# 46. Important Functions Used

| Function            | কাজ                          |
| ------------------- | ---------------------------- |
| `pd.read_csv()`     | CSV dataset load করে         |
| `head()`            | প্রথম কয়েকটি row দেখায়       |
| `info()`            | Dataset information দেখায়    |
| `describe()`        | Statistical summary দেখায়    |
| `isnull()`          | Missing values identify করে  |
| `sum()`             | Count করে                    |
| `median()`          | Median বের করে               |
| `replace()`         | Value replace করে            |
| `duplicated()`      | Duplicate row identify করে   |
| `drop_duplicates()` | Duplicate remove করে         |
| `shape`             | Row ও column সংখ্যা দেখায়    |
| `copy()`            | DataFrame-এর copy তৈরি করে   |
| `MinMaxScaler()`    | Data normalize করে           |
| `fit_transform()`   | Data fit এবং transform করে   |
| `LabelEncoder()`    | Categorical value encode করে |
| `map()`             | Value mapping করে            |
| `plt.hist()`        | Histogram তৈরি করে           |
| `sns.boxplot()`     | Box plot তৈরি করে            |
| `sns.heatmap()`     | Heatmap তৈরি করে             |
| `sns.kdeplot()`     | KDE plot তৈরি করে            |
| `sns.scatterplot()` | Scatter plot তৈরি করে        |
| `plt.show()`        | Graph display করে            |

---

# 47. Important Concepts for Exam

### Dataset

Related data-এর collection।

### DataFrame

Rows এবং columns-এর মাধ্যমে data রাখার tabular structure।

### Missing Value

Dataset-এ কোনো value না থাকা।

### Duplicate

একই record একাধিকবার থাকা।

### Median

Sorted data-এর middle value।

### Normalization

Numerical data-কে নির্দিষ্ট range-এর মধ্যে নিয়ে আসা।

### Encoding

Categorical data-কে numerical form-এ convert করা।

### Filtering

Condition ব্যবহার করে নির্দিষ্ট rows বের করা।

### Histogram

Numerical data-এর distribution দেখায়।

### Box Plot

Data-এর median, spread এবং possible outliers দেখায়।

### Correlation

দুইটি variable-এর relationship-এর direction এবং strength বোঝায়।

### Heatmap

Color ব্যবহার করে matrix-এর values visualize করে।

### KDE Plot

Data distribution-এর smooth density curve দেখায়।

### Scatter Plot

দুইটি numerical variable-এর relationship দেখায়।

---

# 48. Quick Revision

```text
Pandas
→ Data handling

NumPy
→ Numerical operations

Matplotlib
→ Visualization

Seaborn
→ Statistical visualization

read_csv()
→ Dataset load

head()
→ First rows

info()
→ Dataset information

describe()
→ Statistics

isnull().sum()
→ Missing values

median()
→ Median

replace()
→ Replace values

duplicated()
→ Find duplicates

drop_duplicates()
→ Remove duplicates

MinMaxScaler
→ Normalize data

LabelEncoder
→ Encode categorical data

&
→ AND condition

Histogram
→ Distribution

Box Plot
→ Median + spread + outliers

Heatmap
→ Correlation visualization

KDE
→ Distribution curve

Scatter Plot
→ Relationship between two variables
```

---

# 49. One-Minute Memory Map

```text
                 AI LAB 01
                     │
          Diabetes Dataset Analysis
                     │
       ┌─────────────┴─────────────┐
       │                           │
   Data Cleaning              Visualization
       │                           │
       ├─ Missing Values           ├─ Histogram
       ├─ Zero Values             ├─ Box Plot
       ├─ Median                  ├─ Heatmap
       └─ Duplicates              ├─ KDE
                                  └─ Scatter
       │
       ├─ Normalization
       │      ↓
       │   MinMaxScaler
       │
       ├─ Encoding
       │      ↓
       │   LabelEncoder
       │
       └─ Filtering
              ↓
       Outcome = 1
       Age > 40
```

---

# 50. Final Understanding

এই Lab-এর মূল উদ্দেশ্য হলো raw dataset নিয়ে basic **data preprocessing এবং data visualization** শেখা।

আমরা প্রথমে dataset load করেছি এবং dataset-এর structure ও statistics দেখেছি।

তারপর invalid zero values median দিয়ে replace করেছি এবং duplicate records remove করেছি।

এরপর `Glucose`, `BMI` এবং `Age` normalize করেছি এবং `Outcome` encode করেছি।

শেষে বিভিন্ন visualization ব্যবহার করে dataset-এর distribution এবং featureগুলোর relationship দেখেছি।

সবচেয়ে গুরুত্বপূর্ণভাবে মনে রাখবে:

```text
Load
→ Inspect
→ Clean
→ Normalize
→ Encode
→ Filter
→ Visualize
→ Analyze
```
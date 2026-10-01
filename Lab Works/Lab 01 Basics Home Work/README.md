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
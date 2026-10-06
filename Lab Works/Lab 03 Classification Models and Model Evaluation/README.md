# AI Lab 03 – Classification Models and Model Evaluation

## 1. Lab Overview

এই Lab-এ আমরা **Classification Problem** এবং বিভিন্ন **Classification Machine Learning Model** সম্পর্কে শিখেছি।

এই Lab-এর প্রধান বিষয়গুলো হলো:

* Classification এবং Regression-এর পার্থক্য
* Breast Cancer Dataset নিয়ে কাজ করা
* Dataset load এবং explore করা
* Missing values check করা
* Class distribution দেখা
* Imbalanced dataset সম্পর্কে ধারণা নেওয়া
* Imbalance Ratio বের করা
* Class Weight বের করা
* Training এবং Testing dataset তৈরি করা
* Feature Scaling / Standardization
* Logistic Regression
* K-Nearest Neighbors (KNN)
* Decision Tree
* Random Forest
* Support Vector Machine (SVM)
* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix
* ROC Curve
* AUC
* Overfitting এবং Underfitting
* বিভিন্ন model-এর performance compare করা

---

# 2. Classification কী?

Classification হলো এমন একটি **Supervised Machine Learning problem**, যেখানে model কোনো input data-কে নির্দিষ্ট class/category-এর মধ্যে classify করে।

সহজভাবে:

> Classification model input data দেখে সেটি কোন class-এর অন্তর্ভুক্ত তা predict করে।

Example:

```text
Email → Spam / Not Spam

Patient → Disease / No Disease

Transaction → Fraud / Not Fraud

Tumor → Benign / Malignant
```

এই Lab-এ:

```text
Patient/Tumor Data
       ↓
Classification Model
       ↓
Benign / Malignant
```

predict করা হয়।

---

# 3. Classification vs Regression

এটি খুব গুরুত্বপূর্ণ exam topic।

| Classification                | Regression                  |
| ----------------------------- | --------------------------- |
| Class/category predict করে    | Numerical value predict করে |
| Output discrete               | Output continuous numerical |
| Example: Disease/No Disease   | Example: House Price        |
| Logistic Regression, KNN, SVM | Linear Regression           |

### Example

Classification:

```text
Age = 50, Glucose = 150
        ↓
Diabetes
```

Regression:

```text
BMI = 30
   ↓
Diabetes Progression = 180.5
```

### সহজে মনে রাখো

```text
Classification → "কোন class?"
Regression     → "কত value?"
```

---

# 4. Dataset Used in This Lab

এই Lab-এ **Breast Cancer Dataset** ব্যবহার করা হয়েছে।

Dataset load করা হয়েছে scikit-learn থেকে:

```python
from sklearn.datasets import load_breast_cancer

cancer = load_breast_cancer()
```

এই dataset-এ breast cancer সম্পর্কিত বিভিন্ন numerical features এবং একটি target variable আছে।

---

# 5. Target Variable

Code:

```python
df["target"] = cancer.target
```

এই Lab-এর target:

```text
0 → Benign
1 → Malignant
```

অর্থাৎ model-এর কাজ হলো:

```text
Input Features
      ↓
Model
      ↓
0 = Benign
1 = Malignant
```

---

# 6. Required Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import (
    accuracy_score,
    classification_report,
    confusion_matrix,
    roc_curve,
    auc
)

from sklearn.datasets import load_breast_cancer
```

---

# 7. Pandas

```python
import pandas as pd
```

Pandas dataset handling এবং analysis-এর জন্য ব্যবহার করা হয়।

যেমন:

* DataFrame তৈরি করা
* Dataset দেখা
* Column select করা
* Missing values check করা
* Statistics বের করা

---

# 8. NumPy

```python
import numpy as np
```

Numerical operations এবং array-related কাজের জন্য ব্যবহার করা হয়।

---

# 9. Matplotlib

```python
import matplotlib.pyplot as plt
```

Graph এবং visualization তৈরি করার জন্য ব্যবহৃত হয়।

---

# 10. Seaborn

```python
import seaborn as sns
```

Statistical visualization-এর জন্য ব্যবহার করা হয়।

এই Lab-এ:

* Count plot
* Heatmap
* Pie chart
* Confusion matrix visualization

ইত্যাদিতে Seaborn/Matplotlib ব্যবহার করা হয়েছে।

---
# 11. Dataset Load করা

```python
cancer = load_breast_cancer()
```

এরপর DataFrame:

```python
df = pd.DataFrame(
    cancer.data,
    columns=cancer.feature_names
)
```

এবং target:

```python
df["target"] = cancer.target
```

---

# 12. `head()`

প্রথম ৫টি row দেখতে:

```python
print(df.head())
```

### মনে রাখবে

```text
head()
→ First 5 rows
```

---

# 13. Entire Dataset দেখা

সব row দেখানোর জন্য:

```python
pd.set_option('display.max_rows', None)
```

সব column দেখানোর জন্য:

```python
pd.set_option('display.max_columns', None)
```

তারপর:

```python
print(df)
```

সব data দেখার পর settings reset করা যায়:

```python
pd.reset_option('display.max_rows')
pd.reset_option('display.max_columns')
```

---

# 14. Exploratory Data Analysis (EDA)

EDA-এর full form:

> Exploratory Data Analysis

EDA হলো model তৈরি করার আগে dataset সম্পর্কে ভালোভাবে বোঝার process।

EDA-এর মাধ্যমে আমরা জানতে পারি:

* Data কেমন?
* Missing values আছে কি না?
* Numerical values-এর distribution কেমন?
* Classes-এর distribution কেমন?
* Dataset balanced নাকি imbalanced?

---

# 15. Summary Statistics

```python
print(df.describe())
```

`describe()` থেকে পাওয়া যায়:

* Count
* Mean
* Standard deviation
* Minimum
* 25%
* 50%
* 75%
* Maximum

---
# 16. Missing Values

Missing value check:

```python
print(df.isnull().sum())
```

### `isnull()`

প্রতিটি value missing কি না check করে।

### `sum()`

প্রতিটি column-এ missing value কতটি আছে তা count করে।

### মনে রাখবে

```text
isnull()
→ Missing values check

isnull().sum()
→ Missing values count
```

---

# 17. Class Distribution

Class distribution দেখতে:

```python
print(df["target"].value_counts())
```

এতে প্রতিটি class-এ কতগুলো data আছে তা জানা যায়।

Example:

```text
0 → কতটি Benign
1 → কতটি Malignant
```

---

# 18. Class Distribution কেন গুরুত্বপূর্ণ?

Classification problem-এ প্রতিটি class-এর data কতটা আছে তা জানা গুরুত্বপূর্ণ।

ধরো:

```text
Benign     → 500
Malignant  → 50
```

এখানে দুই class সমান নয়।

এ ধরনের dataset-কে **imbalanced dataset** বলা হয়।

---
# 19. Balanced Dataset

যদি classes-এর সংখ্যা মোটামুটি কাছাকাছি হয়:

```text
Class 0 → 300
Class 1 → 280
```

তাহলে dataset relatively balanced।

---

# 20. Imbalanced Dataset

যদি একটি class অন্য class-এর তুলনায় অনেক বেশি হয়:

```text
Class 0 → 900
Class 1 → 100
```

তাহলে dataset imbalanced।

---

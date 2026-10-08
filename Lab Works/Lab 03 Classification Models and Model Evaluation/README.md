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
# 21. Imbalance Ratio

Lab-এ imbalance ratio বের করার জন্য:

```python
minority_class = df["target"].value_counts().min()

majority_class = df["target"].value_counts().max()

imbalance_ratio = majority_class / minority_class

print(f"Imbalance Ratio: {imbalance_ratio:.2f}")
```

Formula:

```text
Imbalance Ratio =
Majority Class Count
--------------------
Minority Class Count
```

---

# 22. Imbalance Ratio Example

ধরো:

```text
Majority = 800
Minority = 200
```

তাহলে:

```text
IR = 800 / 200
   = 4
```

অর্থাৎ imbalance ratio = 4।

Lab-এর provided guideline অনুযায়ী:

```text
IR > 2
→ Dataset imbalanced

IR > 10
→ Highly imbalanced
```

### Important

এটি এই Lab-এর guideline হিসেবে মনে রাখবে।

---

# 23. Class Weight

Class imbalance-এর জন্য class weight বের করা হয়েছে:

```python
from sklearn.utils.class_weight import compute_class_weight

class_weights = compute_class_weight(
    class_weight="balanced",
    classes=np.unique(df["target"]),
    y=df["target"]
)

print("Class Weights:", class_weights)
```

---

# 24. Class Weight কী?

Class weight হলো model-কে different classes-এর প্রতি কতটা গুরুত্ব দিতে হবে তার একটি weight।

যে class dataset-এ কম থাকে, তার weight সাধারণত বেশি হতে পারে।

সহজভাবে:

```text
Underrepresented Class
        ↓
Higher Weight
        ↓
Model gives more importance
```

### Lab-এর note

> Higher weight values indicate a class is underrepresented.

---

# 25. TO DO — Dataset Balancing

Lab-এ বলা হয়েছে:

> Learn how to balance dataset if it is imbalanced.

Dataset imbalance handle করার কিছু সাধারণ approach:

* Class weighting
* Oversampling
* Undersampling
* SMOTE

এই Lab-এ এগুলো detailed implementation করা হয়নি; এগুলো **self-study topic** হিসেবে দেওয়া হয়েছে।

---

# 26. Features এবং Target

Machine Learning-এ:

```text
X → Features
Y → Target
```

এই Lab-এ:

```python
X = df.drop(columns=["target"])
Y = df["target"]
```

---

# 27. X কী?

```python
X = df.drop(columns=["target"])
```

Target column বাদ দিয়ে বাকি সব columns হলো input features।

```text
X = Input Features
```

---

# 28. Y কী?

```python
Y = df["target"]
```

Target হলো model-এর output।

```text
Y = Target
```

---

# 29. Train-Test Split

Dataset-কে:

```text
80% → Training
20% → Testing
```

ভাগ করা হয়েছে।

Code:

```python
X_train, X_test, Y_train, Y_test = train_test_split(
    X,
    Y,
    test_size=0.2,
    random_state=42
)
```

---
# 30. Training Data

Training data দিয়ে model শেখে।

```text
Training Features
        +
Training Labels
        ↓
      Model
        ↓
   Learn Pattern
```

---

# 31. Testing Data

Testing data training-এর পরে model evaluate করার জন্য ব্যবহার করা হয়।

```text
Test Features
     ↓
Model
     ↓
Prediction
     ↓
Compare with Actual Test Labels
```

---

# 32. `test_size=0.2`

```python
test_size=0.2
```

মানে:

```text
20% → Testing
80% → Training
```

---

# 33. `random_state=42`

Dataset split-এর randomness fixed রাখার জন্য:

```python
random_state=42
```

ব্যবহার করা হয়েছে।

একই code আবার run করলে একইভাবে split পাওয়ার সম্ভাবনা থাকে।

---
# 34. Feature Scaling

এই Lab-এ:

```python
scaler = StandardScaler()
```

ব্যবহার করা হয়েছে।

Training data:

```python
X_train_scaled = scaler.fit_transform(X_train)
```

Testing data:

```python
X_test_scaled = scaler.transform(X_test)
```

---

# 35. StandardScaler কী?

StandardScaler features-কে standard scale-এ নিয়ে আসে।

সাধারণভাবে standardized data-এর:

```text
Mean ≈ 0
Standard Deviation ≈ 1
```

হয়।

---
# 36. `fit_transform()` vs `transform()`

Training:

```python
X_train_scaled = scaler.fit_transform(X_train)
```

এখানে:

```text
fit + transform
```

দুটো কাজ হয়।

Testing:

```python
X_test_scaled = scaler.transform(X_test)
```

এখানে শুধু transformation apply হয়।

### মনে রাখবে

```text
Training → fit_transform()
Testing  → transform()
```

---
# 37. কেন Feature Scaling দরকার?

সব algorithm-এর জন্য scaling equally important নয়।

এই Lab-এর note অনুযায়ী scaling বিশেষভাবে দরকার:

```text
Logistic Regression
KNN
SVM
```

কারণ এগুলো feature values-এর scale-এর প্রতি sensitive হতে পারে।

---

# 38. Decision Tree-এর ক্ষেত্রে Scaling

Decision Tree সাধারণত feature scaling-এর উপর একইভাবে dependent নয়।

তাই Lab code-এ:

```python
tree_model.fit(X_train, Y_train)
```

ব্যবহার করা হয়েছে।

এখানে scaled data নয়, original data ব্যবহার করা হয়েছে।

---

# 39. Random Forest-এর ক্ষেত্রেও

Random Forest-ও সাধারণত feature scaling-এর জন্য dependent নয়।

Lab code:

```python
rf_model.fit(X_train, Y_train)
```

অর্থাৎ original training features ব্যবহার করা হয়েছে।

---

# Task 1: Logistic Regression

# 40. Logistic Regression কী?

Logistic Regression একটি classification algorithm।

নামতে "Regression" থাকলেও এটি classification problem solve করতে ব্যবহৃত হয়।

এটি সাধারণত class probability estimate করে এবং সেই probability-এর ভিত্তিতে class predict করে।

---

# 41. Logistic Regression Model

```python
from sklearn.linear_model import LogisticRegression

logistic_model = LogisticRegression()
```

Training:

```python
logistic_model.fit(X_train_scaled, Y_train)
```

Prediction:

```python
Y_pred_logistic = logistic_model.predict(X_test_scaled)
```

---

# 42. Logistic Regression-এর কাজ

```text
Input Features
      ↓
Logistic Regression
      ↓
Class Prediction
      ↓
0 or 1
```

এই Lab-এ:

```text
0 → Benign
1 → Malignant
```

---
# 43. Logistic Regression-এর Basic Idea

Linear Regression-এর output যেকোনো numerical value হতে পারে।

কিন্তু classification-এর ক্ষেত্রে আমাদের class probability দরকার।

Logistic Regression-এর ক্ষেত্রে **sigmoid function** ব্যবহার করা হয়।

Formula:

```text
σ(z) = 1 / (1 + e^(-z))
```

এটি output-কে সাধারণত:

```text
0 থেকে 1
```

এর মধ্যে probability হিসেবে map করে।

যেখানে:

```text
z = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
```

---
# 44. Probability থেকে Class

ধরো model probability দিল:

```text
P = 0.85
```

এবং threshold 0.5 হলে:

```text
0.85 ≥ 0.5
→ Class 1
```

আবার:

```text
P = 0.20
```

হলে:

```text
0.20 < 0.5
→ Class 0
```

---

# 45. Logistic Regression Evaluation

```python
print("Accuracy:",
      accuracy_score(Y_test, Y_pred_logistic))

print("Classification Report:\n",
      classification_report(Y_test, Y_pred_logistic))
```

---
# Task 2: K-Nearest Neighbors (KNN)

# 46. KNN কী?

KNN-এর full form:

> K-Nearest Neighbors

KNN একটি **distance-based classification algorithm**।

সহজভাবে:

> নতুন data point-এর সবচেয়ে কাছের Kটি data point দেখে তার class নির্ধারণ করা হয়।

---

# 47. KNN-এর Basic Idea

ধরো:

```text
K = 5
```

নতুন একটি point-এর সবচেয়ে কাছের ৫টি neighbor পাওয়া গেল।

যদি:

```text
3 → Class 1
2 → Class 0
```

তাহলে majority class:

```text
Class 1
```

তাই নতুন point-কে Class 1 হিসেবে classify করা হবে।

---
# 48. KNN Model

```python
from sklearn.neighbors import KNeighborsClassifier

knn_model = KNeighborsClassifier(n_neighbors=5)
```

এখানে:

```text
K = 5
```

তারপর:

```python
knn_model.fit(X_train_scaled, Y_train)
```

Prediction:

```python
Y_pred_knn = knn_model.predict(X_test_scaled)
```

---

# 49. K কেন গুরুত্বপূর্ণ?

`K` খুব ছোট হলে model noise-এর প্রতি sensitive হতে পারে।

`K` অনেক বড় হলে local pattern হারিয়ে যেতে পারে।

তাই appropriate K নির্বাচন গুরুত্বপূর্ণ।

---

# 50. KNN এবং Scaling

KNN distance ব্যবহার করে।

তাই feature-এর scale বড় হলে distance calculation-এ সেই feature বেশি influence করতে পারে।

এই কারণে KNN-এর জন্য feature scaling খুব গুরুত্বপূর্ণ।

---

# 51. Distance-এর Basic Idea

দুইটি point-এর Euclidean distance:

```text
d = √[(x₁-y₁)² + (x₂-y₂)² + ...]
```

KNN-এর মতো distance-based algorithm-এর ক্ষেত্রে scaling গুরুত্বপূর্ণ হওয়ার একটি কারণ হলো distance calculation।

---
# Task 3: Decision Tree

# 52. Decision Tree কী?

Decision Tree হলো tree structure-based classification algorithm।

এটি বিভিন্ন condition-এর মাধ্যমে data-কে split করে শেষ পর্যন্ত একটি class-এর prediction দেয়।

সহজভাবে:

```text
             Feature?
             /      \
           Yes       No
           /          \
       Condition    Condition
          ↓            ↓
        Class 0      Class 1
```

---

# 53. Decision Tree Model

```python
from sklearn.tree import DecisionTreeClassifier

tree_model = DecisionTreeClassifier(
    max_depth=5,
    random_state=42
)
```

Training:

```python
tree_model.fit(X_train, Y_train)
```

Prediction:

```python
Y_pred_tree = tree_model.predict(X_test)
```

---

# 54. `max_depth=5`

Decision Tree কত গভীর পর্যন্ত যেতে পারবে তা control করতে:

```python
max_depth=5
```

ব্যবহার করা হয়েছে।

Depth বেশি হলে tree খুব complex হতে পারে।

Depth limit করা model-এর complexity control করতে সাহায্য করে।

---

# 55. Decision Tree-এর সুবিধা

* বুঝতে সহজ
* Rule-based structure
* Feature scaling সাধারণত প্রয়োজন হয় না
* Non-linear relationship handle করতে পারে

Lab-এর note অনুযায়ী:

> Works well with unscaled data and handles non-linear relationships.

---
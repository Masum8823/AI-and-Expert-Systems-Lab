# Artificial Intelligence Lab — Zero to Basic Bangla Notes

> **Purpose:** এই README এমনভাবে লেখা হয়েছে যেন AI/ML সম্পর্কে আমার basic একদম zero হলেও এখান থেকে ধীরে ধীরে বুঝতে পারি এবং Lab-এর code নিজে লিখতে পারি।

---

# 1. Artificial Intelligence (AI) কী?

সহজ ভাষায়,

**AI = Computer/Machine-কে এমনভাবে তৈরি করা যাতে সে মানুষের মতো কিছু intelligent কাজ করতে পারে।**

যেমন:

* মানুষের কথা বুঝতে পারা
* ছবি চিনতে পারা
* সিদ্ধান্ত নেওয়া
* Prediction করা
* Problem solve করা
* কোনো data দেখে pattern খুঁজে বের করা

### Example

ধরো, আমরা computer-কে অনেক student's data দিলাম:

| Study Hours | Attendance | Result    |
| ----------: | ---------: | --------- |
|           2 |        60% | Fail      |
|           4 |        75% | Pass      |
|           6 |        85% | Pass      |
|           8 |        95% | Excellent |

Computer এই data দেখে pattern শিখতে পারে।

তারপর নতুন একজন student-এর:

```text
Study Hours = 5
Attendance = 80%
```

দিলে computer অনুমান করতে পারে:

```text
Result = Pass
```

এটাই AI-এর একটি simple example।

Source অনুযায়ী AI হলো এমন machine তৈরি করার field যা human intelligence-এর প্রয়োজন হয় এমন কাজ করতে পারে।

---

# 2. AI, ML, Neural Network এবং Deep Learning

এই চারটা বিষয় প্রথমে confusing লাগবে।

সবচেয়ে সহজভাবে hierarchy:

```text
AI
└── ML
    └── Neural Network
        └── Deep Learning
```

অর্থাৎ:

**AI → ML → Neural Network → Deep Learning**

---

## 2.1 AI

AI হলো সবচেয়ে বড় field।

এর মধ্যে এমন সব technique থাকে যার মাধ্যমে computer intelligent কাজ করতে পারে।

Example:

```text
AI
├── Machine Learning
├── Neural Networks
├── Expert Systems
├── Natural Language Processing
└── Computer Vision
```

---

# 3. Machine Learning (ML)

**Machine Learning হলো AI-এর একটি অংশ।**

এখানে computer-কে প্রতিটি rule manually লিখে দিতে হয় না।

বরং তাকে **data দেওয়া হয়**, এবং data থেকে সে pattern শেখে।

### Traditional Programming

আমরা যদি বলি:

```text
যদি marks >= 40
    তাহলে Pass
নাহলে
    Fail
```

এখানে rule আমরা নিজেরাই লিখেছি।

### Machine Learning

ML-এ আমরা অনেক example data দেব:

```text
Marks     Result
30        Fail
35        Fail
45        Pass
60        Pass
80        Pass
```

Machine এই data থেকে pattern শেখার চেষ্টা করবে।

তারপর নতুন marks দিলে prediction করবে।

---

# 4. Neural Network কী?

Neural Network হলো ML-এর একটি technique।

এটি মানুষের brain-এর neuron-এর idea থেকে inspired।

সহজভাবে:

```text
Input
  ↓
Neuron Layer
  ↓
Neuron Layer
  ↓
Output
```

যেমন student result prediction:

```text
Study Hours ─────┐
                 ├──> Neural Network ──> Result
Attendance ──────┤
                 │
Previous Marks ──┘
```

Neural Network input data নিয়ে বিভিন্ন layer-এর মাধ্যমে process করে output দেয়।

---

# 5. Deep Learning (DL)

Deep Learning হলো Neural Network-এর একটি advanced form যেখানে **অনেকগুলো hidden layer** থাকে।

```text
Input
 ↓
Hidden Layer
 ↓
Hidden Layer
 ↓
Hidden Layer
 ↓
Output
```

অনেক layer থাকার কারণে একে **Deep Learning** বলা হয়।

Deep Learning complex কাজের ক্ষেত্রে খুব useful, যেমন:

* Image Recognition
* Speech Recognition
* Natural Language Processing

Source-এও DL-কে multiple hidden layers-যুক্ত neural network হিসেবে ব্যাখ্যা করা হয়েছে।

---

# 6. এই Lab-এ আসলে কী শিখব?

এই lab-এর মূল focus এখনো বড় কোনো AI model বানানো না।

বরং AI-এর আগে যে সবচেয়ে important কাজ করতে হয়:

> **Data নিয়ে কাজ করা।**

Lab-এ মূলত আমরা শিখব:

```text
Dataset
   ↓
Load
   ↓
Understand
   ↓
Clean
   ↓
Transform
   ↓
Scale
   ↓
Filter
   ↓
AI/ML Model-এর জন্য প্রস্তুত
```

এই process-এর সবচেয়ে গুরুত্বপূর্ণ অংশ হলো:

# Data Preprocessing

---
# 7. Data কী?

Data মানে হলো information।

Example:

```text
Name = Alice
Age = 25
Salary = 50000
```

আর অনেকগুলো data একসাথে থাকলে আমরা dataset পাই।

Example:

| Name    | Age | Salary |
| ------- | --: | -----: |
| Alice   |  25 |  50000 |
| Bob     |  30 |  60000 |
| Charlie |  35 |  70000 |

---

# 8. Dataset কী?

অনেকগুলো related data একসাথে থাকলে তাকে dataset বলা হয়।

যেমন student dataset:

| Name | Age | Marks | Result |
| ---- | --: | ----: | ------ |
| A    |  20 |    80 | Pass   |
| B    |  21 |    45 | Pass   |
| C    |  20 |    30 | Fail   |

এখানে:

* প্রতিটি **row** = একটি student's record
* প্রতিটি **column** = একটি feature/information

---

# 9. Data Preprocessing কী?

Raw data সরাসরি AI model-এ দেওয়া সবসময় ভালো হয় না।

কারণ data-এর মধ্যে থাকতে পারে:

* Missing value
* Duplicate data
* Wrong data
* Text/category
* Different numerical scales

তাই model-এর আগে data clean এবং prepare করতে হয়।

এই কাজকে বলা হয়:

# Data Preprocessing

সহজ flow:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Transformation
   ↓
Feature Selection
   ↓
Feature Scaling
   ↓
Ready for ML
```

Source অনুযায়ী preprocessing হলো raw data-কে clean এবং structured format-এ transform করার process।

---

# 10. Data Cleaning

Data Cleaning মানে data-এর সমস্যা ঠিক করা।

যেমন:

```text
Age = 20
Age = 21
Age = NULL
Age = 22
Age = 20
```

এখানে:

* NULL → Missing value
* একই row একাধিকবার থাকলে → Duplicate

এগুলো handle করতে হবে।

---

# 11. Missing Value কী?

যখন কোনো data পাওয়া যায় না তখন সেটি missing value।

Example:

| Name  | Age | Salary |
| ----- | --: | -----: |
| Alice |  25 |  50000 |
| Bob   |  30 |  60000 |
| Emma  |  45 |    NaN |

এখানে Emma-এর salary নেই।

Pandas সাধারণত এটাকে:

```text
NaN
```

দিয়ে দেখায়।

NaN-এর অর্থ এখানে value পাওয়া যাচ্ছে না।

---

# 12. Missing Value কীভাবে handle করব?

মূলত তিনভাবে করা যায়।

## Method 1 — Remove

যে row-তে missing value আছে সেটি delete করে দেওয়া।

```python
df.dropna()
```

Example:

```text
Alice   25   50000
Bob     30   60000
Emma    45   NaN
```

`dropna()` করলে Emma-এর row বাদ যেতে পারে।

---

## Method 2 — Fill

Missing জায়গায় একটি suitable value বসানো।

যেমন mean:

```python
df.fillna(df.mean())
```

ধরো:

```text
Salary:
50000
60000
NaN
80000
```

Mean:

```text
(50000 + 60000 + 80000) / 3
= 63333.33
```

তাহলে NaN-এর জায়গায় প্রায়:

```text
63333.33
```

বসানো যায়।

---

## Method 3 — Interpolation

আগের এবং পরের value দেখে missing value estimate করা।

সহজভাবে:

```text
10
20
?
40
50
```

এখানে মাঝের value অনুমান করে:

```text
30
```

ধরা যেতে পারে।

---

# 13. Categorical Data vs Numerical Data

এটা খুব important।

## Numerical Data

যে data number দিয়ে প্রকাশ করা যায়।

Example:

```text
Age = 25
Salary = 50000
Height = 5.8
Marks = 85
```

এগুলো numerical।

---

## Categorical Data

যে data category বা group বোঝায়।

Example:

```text
Gender = Male
City = Dhaka
Color = Red
Species = Setosa
```

এগুলো categorical।

Source-এ categorical data-কে categories বোঝানো non-numeric data এবং numerical data-কে measurable numbers হিসেবে আলাদা করা হয়েছে।

---

# 14. Encoding কী?

Machine Learning model সাধারণত numerical data নিয়ে কাজ করতে বেশি স্বাচ্ছন্দ্যবোধ করে।

কিন্তু dataset-এ যদি থাকে:

```text
Male
Female
```

তাহলে এগুলোকে number-এ convert করতে হতে পারে।

এই conversion হলো:

# Encoding

---

# 15. Label Encoding

প্রতিটি category-কে একটি number দেওয়া হয়।

Example:

```text
Male   → 0
Female → 1
```

আর species:

```text
setosa     → 0
versicolor → 1
virginica  → 2
```

Python:

```python
from sklearn.preprocessing import LabelEncoder

encoder = LabelEncoder()

df["species"] = encoder.fit_transform(df["species"])
```

এখানে:

### `LabelEncoder()`

একটি encoder তৈরি করছে।

### `fit_transform()`

দুইটি কাজ একসাথে করছে:

```text
fit
+
transform
```

অর্থাৎ category চিনছে এবং তারপর number-এ convert করছে।

Source-এর Iris example-এ `species` column-কে LabelEncoder দিয়ে numeric label-এ convert করা হয়েছে।

---

# 16. One-Hot Encoding

আরেকটি encoding method হলো One-Hot Encoding।

ধরো:

```text
Gender
------
Male
Female
```

এটা এমন হতে পারে:

| Male | Female |
| ---: | -----: |
|    1 |      0 |
|    0 |      1 |

অর্থাৎ প্রতিটি category-এর জন্য আলাদা binary column তৈরি হয়।

Source-এ One-Hot Encoding এবং Label Encoding দুটো method-ই উল্লেখ করা হয়েছে।

---

# 17. Feature কী?

Dataset-এর প্রতিটি useful input column-কে সহজভাবে feature বলা যায়।

Example:

| Study Hours | Attendance | Previous Marks | Result |
| ----------: | ---------: | -------------: | ------ |
|           5 |         80 |             70 | Pass   |

এখানে:

```text
Study Hours
Attendance
Previous Marks
```

হলো input features।

আর:

```text
Result
```

হতে পারে target/output।

---

# 18. Feature Selection

Dataset-এ অনেক column থাকতে পারে।

কিন্তু সব column model-এর জন্য দরকারি নাও হতে পারে।

তাই useful feature select করা হয়।

এটাই:

# Feature Selection

Example:

```text
Name
Age
Study Hours
Attendance
Previous Marks
Random ID
```

Prediction-এর জন্য হয়তো:

```text
Study Hours
Attendance
Previous Marks
```

যথেষ্ট।

তখন প্রয়োজনীয় features select করা হবে।

---

# 19. Feature Scaling

ধরো আমাদের dataset:

```text
Age = 20
Salary = 50000
```

দুটোর scale অনেক different।

একটি:

```text
20
```

আরেকটি:

```text
50000
```

কিছু ML algorithm-এর জন্য এই difference সমস্যা তৈরি করতে পারে।

তাই numerical values-কে comparable scale-এ আনা হয়।

এটাকে বলে:

# Feature Scaling

Source-এ বলা হয়েছে scaling বড় value-এর domination কমাতে এবং model performance/convergence improve করতে সাহায্য করতে পারে।

---

# 20. Normalization

Normalization-এর একটি common method হলো:

# Min-Max Scaling

এতে value সাধারণত:

```text
0 থেকে 1
```

এর মধ্যে নিয়ে আসা হয়।

Formula:

```text
X' = (X - Min) / (Max - Min)
```

ধরো:

```text
Min = 10
Max = 100
X = 55
```

তাহলে:

```text
(55 - 10) / (100 - 10)

= 45 / 90

= 0.5
```

অর্থাৎ:

```text
55 → 0.5
```

Source-এ Min-Max Scaling-এর এই formula দেওয়া আছে।

---

# 21. Standardization

আরেকটি scaling method হলো:

# Standardization / Z-score Scaling

Formula:

```text
Z = (X - Mean) / Standard Deviation
```

এখানে data এমনভাবে transform হয় যাতে:

```text
Mean ≈ 0
Standard Deviation ≈ 1
```

Normalization:

```text
0 → 1 range
```

Standardization:

```text
mean = 0
std = 1
```

দুটো এক জিনিস নয়।

---

# 22. এখন আসি Python Libraries-এ

এই Lab-এর সবচেয়ে important তিনটি library:

```text
NumPy
Pandas
Matplotlib
```

এছাড়া preprocessing-এর জন্য:

```text
Scikit-learn
```

---

# 23. NumPy কী?

NumPy = Numerical Python

এটি mainly numerical calculation এবং array/matrix নিয়ে কাজ করার জন্য ব্যবহার করা হয়।

Import:

```python
import numpy as np
```

এখানে:

```text
numpy
```

library-এর নাম।

আর:

```text
np
```

হলো তার short name।

তাই:

```python
np.array()
```

মানে NumPy-এর array function ব্যবহার করা।

---

# 24. NumPy Array কী?

সাধারণ Python list:

```python
numbers = [1, 2, 3, 4, 5]
```

NumPy:

```python
arr = np.array([1, 2, 3, 4, 5])
```

Array numerical operation-এর জন্য খুব useful।

---

# 25. `np.arange()`

Source code:

```python
arr = np.arange(1, 13)
```

এটা তৈরি করবে:

```text
1 2 3 4 5 6 7 8 9 10 11 12
```

মনে রাখবে:

```python
np.arange(start, stop)
```

এখানে `stop` সাধারণত include হয় না।

তাই:

```python
np.arange(1, 13)
```

মানে:

```text
1 থেকে 12
```

---

# 26. `reshape()`

ধরো array:

```text
1 2 3 4 5 6 7 8 9 10 11 12
```

এতে মোট:

```text
12 elements
```

এখন:

```python
arr.reshape(3, 4)
```

করলে:

```text
1  2  3  4
5  6  7  8
9 10 11 12
```

হবে।

অর্থাৎ:

```text
3 rows
4 columns
```

কারণ:

```text
3 × 4 = 12
```

### Important

Reshape করার সময় total elements একই থাকতে হবে।

যেমন 12 elements-কে:

```text
3 × 4
2 × 6
4 × 3
```

করা যাবে।

কিন্তু:

```text
5 × 3
```

করা যাবে না।

কারণ:

```text
5 × 3 = 15
```

---

# 27. NumPy Matrix

Source:

```python
A = np.array([[1, 2],
              [3, 4]])

B = np.array([[5, 6],
              [7, 8]])
```

এগুলো 2×2 matrix।

A:

```text
1 2
3 4
```

B:

```text
5 6
7 8
```

---

# 28. Element-wise Multiplication

Code:

```python
A * B
```

এখানে একই position-এর value multiply হয়।

```text
1×5 = 5
2×6 = 12
3×7 = 21
4×8 = 32
```

Result:

```text
5   12
21  32
```

অর্থাৎ:

```text
A * B
```

মানে এখানে element-by-element multiplication।

---

# 29. Matrix Multiplication

Code:

```python
np.dot(A, B)
```

এটা সাধারণ element-wise multiplication না।

Matrix multiplication rule অনুযায়ী calculation হয়।

Result:

```text
19  22
43  50
```

যেমন first value:

```text
(1×5) + (2×7)

= 5 + 14

= 19
```

---

# 30. Transpose

Code:

```python
np.transpose(A)
```

অথবা:

```python
A.T
```

Transpose করলে:

Rows ↔ Columns

Original:

```text
1 2
3 4
```

Transpose:

```text
1 3
2 4
```

অর্থাৎ:

```text
Row → Column
Column → Row
```

---

# 31. Mean

Mean মানে সাধারণ average।

Data:

```text
10, 20, 30, 40, 50
```

Mean:

```text
(10+20+30+40+50) / 5

= 150 / 5

= 30
```

Python:

```python
np.mean(data)
```

---

# 32. Median

Median হলো sorted data-এর middle value।

Example:

```text
10, 20, 30, 40, 50
```

Middle:

```text
30
```

তাই:

```python
np.median(data)
```

দিলে:

```text
30
```

---

# 33. Standard Deviation

Standard deviation বলে data values average-এর আশেপাশে কতটা spread করেছে।

সহজভাবে:

```text
Low Standard Deviation
→ values কাছাকাছি

High Standard Deviation
→ values বেশি ছড়ানো
```

Python:

```python
np.std(data)
```

---

# 34. Variance

Variance-ও data কতটা spread করেছে তা measure করে।

Python:

```python
np.var(data)
```

Relationship:

```text
Variance = Standard Deviation²
```

---

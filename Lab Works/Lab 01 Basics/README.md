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


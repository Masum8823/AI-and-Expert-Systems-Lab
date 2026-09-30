# AI Lab 2 — Linear Regression

## Zero to Basic Bangla Notes

> **Purpose:** এই README এমনভাবে লেখা হয়েছে যেন Linear Regression সম্পর্কে আমার basic একদম zero হলেও এখান থেকে concept, formula, Python code এবং output বুঝতে পারি।

---

# 1. এই Lab-এ আমরা কী শিখব?

এই Lab-এর মূল বিষয়:

# Linear Regression

আমরা শিখব:

```text
Linear Regression
      ↓
Mathematical Formula
      ↓
Dataset
      ↓
EDA
      ↓
Train/Test Split
      ↓
Feature Scaling
      ↓
Simple Linear Regression
      ↓
Multiple Linear Regression
      ↓
Prediction
      ↓
Performance Evaluation
      ↓
Feature Selection / Importance
```

---
# 2. Linear Regression কী?

প্রথমে খুব সহজভাবে বুঝি।

ধরো, আমরা house price predict করতে চাই।

আমাদের কাছে কিছু information আছে:

| Income | House Price |
| -----: | ----------: |
|      2 |         1.2 |
|      3 |         1.5 |
|      4 |         1.8 |
|      5 |         2.2 |
|      6 |         2.5 |

এখানে আমরা লক্ষ্য করছি:

> Income বাড়লে House Price-ও সাধারণত বাড়ছে।

Machine Learning model এই relationship শিখে নতুন income-এর জন্য house price predict করতে পারে।

এই ধরনের prediction-এর জন্য Linear Regression ব্যবহার করা যায়।

---

# 3. Linear Regression কোন ধরনের Machine Learning?

Linear Regression হলো:

```text
Machine Learning
      ↓
Supervised Learning
      ↓
Regression
      ↓
Linear Regression
```

## Supervised Learning কী?

যে Machine Learning-এ model-কে input-এর সাথে correct output-ও দেওয়া হয় তাকে supervised learning বলা হয়।

Example:

```text
Input              Output

Income = 3   →     Price = 1.5
Income = 5   →     Price = 2.2
Income = 6   →     Price = 2.5
```

Machine input এবং output-এর relationship শেখে।

তারপর নতুন input দিলে output predict করে।

---

# 4. Regression কী?

Regression-এর মূল কাজ:

> **Continuous numerical value predict করা।**

যেমন:

```text
House Price
Salary
Temperature
Sales
Stock Price
```

এগুলো continuous numerical values হতে পারে।

Example:

```text
House Price = 250000
Salary = 50000
Temperature = 32.5
```

---

# 5. Classification বনাম Regression

এটা খুব important।

## Classification

Output হলো category/class।

Example:

```text
Pass / Fail
Yes / No
Disease / No Disease
Spam / Not Spam
```

## Regression

Output হলো numerical/continuous value।

Example:

```text
House Price = 250000
Salary = 50000
Temperature = 32.5
```

সহজভাবে:

```text
Classification → Category
Regression    → Number
```

---

# 6. Linear Regression-এর মূল Idea

Linear Regression ধরে নেয়:

> Input এবং output-এর মধ্যে একটি approximately linear relationship আছে।

সহজভাবে graph কল্পনা করো:

```text
Price
  |
  |                 *
  |             *
  |          *
  |       *
  |    *
  |________________________ Income
```

যদি points-এর trend মোটামুটি একটি straight line-এর মতো হয়, তাহলে Linear Regression সেই relationship-এর একটি line খুঁজে বের করার চেষ্টা করে।

---

# 7. Simple Linear Regression

যখন মাত্র **একটি input feature** থাকে তখন তাকে:

# Simple Linear Regression

বলা হয়।

Formula:

```text
Y = mX + c
```

এখানে:

```text
Y = Predicted Output
X = Input Feature
m = Slope
c = Intercept
```

---

# 8. Formula-টা বাস্তব Example দিয়ে বুঝি

ধরো:

```text
Y = 2X + 1
```

এখানে:

```text
m = 2
c = 1
```

যদি:

```text
X = 3
```

তাহলে:

```text
Y = 2(3) + 1
  = 6 + 1
  = 7
```

অর্থাৎ prediction:

```text
Y = 7
```

---

# 9. X কী?

```text
X = Input / Feature
```

Example:

```text
Income
Study Hours
House Size
Experience
```

যে information ব্যবহার করে আমরা prediction করব সেটাই feature/input।

---

# 10. Y কী?

```text
Y = Target / Output
```

যে value আমরা predict করতে চাই সেটাই target।

এই Lab-এ:

```text
X → House-related features
Y → House Price
```

---

# 11. m কী?

Formula:

```text
Y = mX + c
```

এখানে:

```text
m = Slope
```

Slope বলে:

> X পরিবর্তন হলে Y কতটা পরিবর্তন করার tendency দেখাচ্ছে।

ধরো:

```text
Y = 2X + 1
```

তাহলে:

```text
m = 2
```

X 1 unit বাড়লে Y-এর predicted value 2 unit বাড়বে।

---

# 12. c কী?

```text
c = Intercept
```

Intercept হলো সেই point যেখানে regression line X-axis-এর সাথে শুরু/ছেদ করার অবস্থান নির্দেশ করে।

Formula:

```text
Y = mX + c
```

যদি:

```text
X = 0
```

তাহলে:

```text
Y = c
```

অর্থাৎ X zero হলে model-এর predicted Y হলো intercept।

---

# 13. Multiple Linear Regression

যখন একটির বেশি feature ব্যবহার করা হয় তখন:

# Multiple Linear Regression

Formula:

```text
Y = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
```

এখানে:

```text
Y  = Predicted Target
β₀ = Intercept
β₁ = X₁-এর coefficient
β₂ = X₂-এর coefficient
...
βₙ = Xₙ-এর coefficient
```

---

# 14. Multiple Regression বাস্তব Example

ধরো House Price predict করতে আমাদের:

```text
X₁ = Income
X₂ = House Age
X₃ = Number of Rooms
X₄ = Population
```

আছে।

তাহলে equation হতে পারে:

```text
Price = β₀
      + β₁(Income)
      + β₂(House Age)
      + β₃(Rooms)
      + β₄(Population)
```

অর্থাৎ model একসাথে অনেক feature ব্যবহার করে price predict করবে।

---

# 15. Simple বনাম Multiple Linear Regression

| বিষয়    | Simple         | Multiple                     |
| ------- | -------------- | ---------------------------- |
| Feature | 1টি            | একাধিক                       |
| Formula | Y = mX + c     | Y = β₀ + β₁X₁ + ...          |
| Example | Income → Price | Income + Rooms + Age → Price |

মনে রাখবে:

```text
1 Feature  → Simple Linear Regression

Many Features → Multiple Linear Regression
```

---

# 16. Coefficient কী?

Multiple Regression-এ প্রতিটি feature-এর সাথে একটি coefficient থাকে।

Example:

```text
Price = 1 + 2(Income) + 0.5(Rooms)
```

এখানে:

```text
Income coefficient = 2
Rooms coefficient  = 0.5
```

Coefficient বলে feature-এর সাথে target-এর relationship-এর direction এবং magnitude সম্পর্কে।

---

# 17. Positive এবং Negative Coefficient

যদি coefficient positive হয়:

```text
Coefficient > 0
```

তাহলে feature বাড়ার সাথে target বাড়ার relationship থাকতে পারে।

যদি coefficient negative হয়:

```text
Coefficient < 0
```

তাহলে feature বাড়ার সাথে target কমার relationship থাকতে পারে।

Example:

```text
Coefficient = +2
```

→ positive relationship

```text
Coefficient = -1.5
```

→ negative relationship

---

# 18. Model কীভাবে Best Line খুঁজে?

এটা Linear Regression-এর important concept।

Model এমন একটি line/equation খুঁজতে চায় যাতে:

```text
Actual Value
      ↓
Predicted Value
```

এর difference যতটা সম্ভব কম হয়।

এই difference-কে error বলা যায়।

Example:

```text
Actual Price      = 300000
Predicted Price   = 280000

Error = 20000
```

Model এমন parameters খুঁজবে যাতে overall error কম হয়।

---

# 19. Mean Squared Error (MSE)

Linear Regression-এর একটি important objective হলো error কমানো।

MSE:

```text
MSE = Average of Squared Errors
```

Conceptually:

```text
Error = Actual - Predicted

Squared Error = (Actual - Predicted)²
```

তারপর সব squared error-এর average নেওয়া হয়।

---

# 20. কেন Error Square করা হয়?

ধরো errors:

```text
+10
-10
```

যদি সরাসরি average করি:

```text
(10 + -10) / 2 = 0
```

দেখে মনে হবে error নেই।

কিন্তু বাস্তবে error আছে।

তাই square করা হয়:

```text
10²  = 100
(-10)² = 100
```

এখন error positive হয়ে যায়।

---

# 21. Least Squares Method

Linear Regression parameters বের করার একটি common method হলো:

# Least Squares

এর basic idea:

> এমন line খুঁজে বের করা যাতে squared errors-এর total যতটা সম্ভব কম হয়।

অর্থাৎ:

```text
Actual points
      ↓
Best fitting line
      ↓
Minimum squared error
```

Source অনুযায়ী Linear Regression-এর coefficients Gradient Descent অথবা Least Squares method দিয়ে learn করা যেতে পারে।

---

# 22. Gradient Descent

আরেকটি method হলো:

# Gradient Descent

এটা সহজভাবে এমন একটি optimization technique যেখানে model-এর parameters ধীরে ধীরে update করা হয় যাতে error কমে।

Concept:

```text
Start
  ↓
Calculate Error
  ↓
Update Parameters
  ↓
Error কমে?
  ↓
Repeat
  ↓
Better Model
```

তবে এই Lab-এর Python code-এ আমরা manually Gradient Descent লিখছি না।

`LinearRegression()` ব্যবহার করছি।

---
# 23. এখন Python Part

এই Lab-এ প্রধান libraries:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

এছাড়াও Scikit-learn থেকে:

```python
train_test_split
LinearRegression
metrics
StandardScaler
fetch_california_housing
```

ব্যবহার করা হয়েছে।

---

# 24. NumPy

```python
import numpy as np
```

NumPy numerical calculation এবং arrays-এর জন্য ব্যবহার হয়।

এই Lab-এ খুব বেশি NumPy operation নেই, কিন্তু Python-এর data science ecosystem-এর গুরুত্বপূর্ণ library।

---

# 25. Pandas

```python
import pandas as pd
```

Pandas dataset/table নিয়ে কাজ করার জন্য ব্যবহার করা হয়।

যেমন:

```python
df = pd.DataFrame(...)
```

এখানে:

```text
df = DataFrame
```

---

# 26. Matplotlib

```python
import matplotlib.pyplot as plt
```

Graph তৈরি করার জন্য ব্যবহার হয়।

যেমন:

```python
plt.scatter()
plt.plot()
plt.show()
```

---

# 27. Seaborn

```python
import seaborn as sns
```

Seaborn মূলত সুন্দর এবং সহজ statistical visualization তৈরির জন্য ব্যবহৃত হয়।

এই Lab-এ:

```python
sns.heatmap()
sns.barplot()
```

ব্যবহার করা হয়েছে।

---

# 28. Scikit-learn

Scikit-learn হলো Python-এর জনপ্রিয় Machine Learning library।

এই Lab-এ এটি ব্যবহার হয়েছে:

```text
Train/Test Split
Linear Regression
Evaluation Metrics
Feature Scaling
Dataset Loading
```

এর জন্য।

---

# 29. Dataset Load করা

Lab-এ:

```python
from sklearn.datasets import fetch_california_housing
```

ব্যবহার করা হয়েছে।

তারপর:

```python
data = fetch_california_housing()
```

দিয়ে dataset load করা হয়েছে।

---

# 30. Important Note: Dataset-এর নাম

Lab instruction-এ dataset-টিকে:

```text
Boston Housing Prices Dataset
```

বলা হয়েছে।

কিন্তু provided code বাস্তবে:

```python
fetch_california_housing()
```

ব্যবহার করছে।

অর্থাৎ code অনুযায়ী dataset হলো:

# California Housing Dataset

README-তে code বুঝতে গেলে **`fetch_california_housing()`-কেই follow করবে**।

---

# 31. Dataset DataFrame-এ নেওয়া

Code:

```python
df = pd.DataFrame(
    data.data,
    columns=data.feature_names
)
```

এখানে dataset-এর feature data দিয়ে Pandas DataFrame তৈরি করা হয়েছে।

সহজভাবে:

```text
Raw Dataset
     ↓
Pandas DataFrame
     ↓
df
```

---

# 32. Target Column তৈরি করা

Code:

```python
df["Price"] = data.target
```

এখানে dataset-এর target values:

```text
data.target
```

কে DataFrame-এর নতুন column:

```text
Price
```

হিসেবে রাখা হয়েছে।

অর্থাৎ:

```text
Features → df-এর অন্যান্য columns

Target → Price
```

---

# 33. Dataset-এর Concept

এই dataset-এ বিভিন্ন housing-related features আছে।

যেমন source code-এর:

```text
MedInc
```

Median Income বোঝায়।

এবং:

```text
Price
```

হলো target।

আমরা বিভিন্ন features ব্যবহার করে:

```text
House Price
```

predict করতে চাই।

---

# 34. `df.head()`

```python
print(df.head())
```

প্রথম 5টি row দেখাবে।

Dataset load হয়েছে কিনা দ্রুত check করার জন্য এটি useful।

---

# 35. পুরো Dataset Print

```python
print(df)
```

দিলে DataFrame-এর content print হবে।

তারপর:

```python
pd.set_option('display.max_rows', None)
```

দিলে Pandas সব rows display করার চেষ্টা করবে।

এবং:

```python
pd.set_option('display.max_columns', None)
```

দিলে সব columns display করা যাবে।

---

# 36. Settings Reset

শেষে:

```python
pd.reset_option('display.max_rows')
pd.reset_option('display.max_columns')
```

দিয়ে Pandas-এর display settings আগের অবস্থায় ফেরত নেওয়া যায়।

---

# 37. EDA কী?

EDA =

# Exploratory Data Analysis

সহজভাবে:

> Dataset-এর ভিতরে কী আছে সেটা explore এবং understand করার process।

Model train করার আগে আমরা জানতে চাই:

```text
Data কেমন?
Missing value আছে?
Values-এর distribution কেমন?
Features-এর relationship কেমন?
```

---

# 38. `df.describe()`

```python
print(df.describe())
```

এটি numerical columns-এর statistical summary দেয়।

যেমন:

```text
count
mean
std
min
25%
50%
75%
max
```

এসব আমরা আগের Lab-এও দেখেছি।

---

# 39. Missing Value Check

```python
df.isnull().sum()
```

প্রতিটি column-এ কতটি missing value আছে সেটা দেখায়।

যদি:

```text
MedInc     0
HouseAge   0
...
```

হয়, তাহলে ওই columns-এ missing value নেই।

---

# 40. Correlation কী?

এটা Lab 2-এর খুব important concept।

Correlation হলো দুইটি variable-এর মধ্যে relationship-এর strength এবং direction বোঝার একটি statistical measure।

সহজভাবে:

```text
X বাড়লে Y-ও বাড়ে?
X বাড়লে Y কমে?
নাকি তেমন relationship নেই?
```

---

# 41. Positive Correlation

যদি:

```text
X ↑
Y ↑
```

তাহলে positive correlation থাকতে পারে।

Example:

```text
Income ↑
House Price ↑
```

---

# 42. Negative Correlation

যদি:

```text
X ↑
Y ↓
```

তাহলে negative correlation হতে পারে।

Example:

```text
একটি variable বাড়লে অন্যটি কমছে।
```

---

# 43. Correlation Heatmap

Code:

```python
plt.figure(figsize=(10, 6))

sns.heatmap(
    df.corr(),
    annot=True,
    cmap="coolwarm",
    linewidths=0.5
)

plt.title("Feature Correlation Heatmap")
plt.show()
```

এখানে সবচেয়ে important:

```python
df.corr()
```

এটি columns-এর correlation calculate করে।

---

# 44. `annot=True`

```python
annot=True
```

দিলে heatmap-এর প্রতিটি cell-এর ভিতরে correlation value দেখা যায়।

Example:

```text
0.85
-0.60
0.12
```

---

# 45. Correlation Value বোঝা

Correlation সাধারণত:

```text
-1 থেকে +1
```

এর মধ্যে থাকে।

সহজভাবে:

```text
+1 → Strong Positive
 0 → Little/No Linear Relationship
-1 → Strong Negative
```

---

# 46. Lab-এর Important Insight

Provided lab material অনুযায়ী:

> **MedInc (Median Income) এবং Price-এর মধ্যে high correlation দেখা যায়।**

অর্থাৎ Median Income এবং house price-এর মধ্যে strong positive relationship লক্ষ্য করা হয়েছে।

---

# 47. Feature এবং Target আলাদা করা

Code:

```python
X = df.drop(columns=["Price"])
Y = df["Price"]
```

এখানে:

```text
X = Features
Y = Target
```

---

# 48. X কেন Price ছাড়া?

আমরা Price predict করতে চাই।

তাই Price নিজে input হতে পারে না।

তাই:

```python
X = df.drop(columns=["Price"])
```

মানে:

> Price column বাদ দিয়ে বাকি columns X হিসেবে নাও।

---

# 49. Y কী?

```python
Y = df["Price"]
```

মানে:

> Price column-কে target হিসেবে Y-তে রাখো।

তাই:

```text
X → Input Features
Y → Output/Target
```

---
# 50. Train এবং Test Data

Machine Learning-এ পুরো dataset দিয়ে model train করে একই data দিয়ে পরীক্ষা করা ভালো practice নয়।

তাই dataset ভাগ করা হয়:

```text
Training Data
Testing Data
```

---

# 51. Training Data কী?

Training data দিয়ে:

> Model relationship শেখে।

Example:

```text
Training Data
     ↓
Model learns
     ↓
Pattern
```

---

# 52. Testing Data কী?

Testing data model training-এর সময় ব্যবহার না করে পরে model-এর performance পরীক্ষা করার জন্য রাখা হয়।

```text
Training
   ↓
Learn

Testing
   ↓
Evaluate
```

---

# 53. 80/20 Split

Lab-এ:

```text
80% → Training
20% → Testing
```

ব্যবহার করা হয়েছে।

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

# 54. `test_size=0.2`

```python
test_size=0.2
```

মানে:

```text
20% → Test
80% → Train
```

---

# 55. `random_state=42`

Dataset split করার সময় random selection হয়।

```python
random_state=42
```

দিলে একই code আবার run করলে একই ধরনের split পাওয়া যায়।

এটাকে reproducibility-এর জন্য ব্যবহার করা হয়।

`42` নিজে কোনো magic mathematical value না।

অন্য fixed integer-ও দেওয়া যায়।

---

# 56. Training এবং Testing Shape

```python
print(X_train.shape)
print(X_test.shape)
```

এগুলো দিয়ে training এবং testing data-তে কত rows/columns আছে সেটা দেখা যায়।

---
# 57. Feature Scaling / Standardization

Lab-এ:

```python
scaler = StandardScaler()
```

ব্যবহার করা হয়েছে।

তারপর:

```python
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

---

# 58. StandardScaler কী করে?

StandardScaler numerical features-কে standardize করে।

Concept:

```text
Mean ≈ 0
Standard Deviation ≈ 1
```

এর মতো scale-এ নিয়ে আসে।

---

# 59. কেন Training Data-তে `fit_transform()`?

```python
X_train = scaler.fit_transform(X_train)
```

এখানে:

```text
fit
↓
Training data-এর mean/std শেখে

transform
↓
Training data scale করে
```

---

# 60. কেন Test Data-তে শুধু `transform()`?

```python
X_test = scaler.transform(X_test)
```

খুব important:

Test data-এর statistics দিয়ে নতুন করে scaler fit করা হয় না।

Training data থেকে শেখা scaling parameters ব্যবহার করেই test data transform করা হয়।

সহজভাবে:

```text
X_train
 ↓
fit
 ↓
transform

X_test
 ↓
শুধু transform
```

---
# 61. Simple Linear Regression

এখন আমরা শুধু একটি feature ব্যবহার করব:

```text
MedInc
```

অর্থাৎ:

```text
Median Income → House Price
```

এটাই:

# Simple Linear Regression

---

# 62. Simple Regression-এর Code

```python
X_simple = df[["MedInc"]]
Y_simple = df["Price"]
```

এখানে:

```text
X_simple → MedInc
Y_simple → Price
```

---

# 63. কেন `df[["MedInc"]]`?

এখানে দুইটি square bracket:

```python
df[["MedInc"]]
```

ব্যবহার করা হয়েছে।

কারণ আমরা DataFrame format-এ একটি column নিতে চাই।

এটি:

```python
df["MedInc"]
```

থেকে কিছুটা আলাদা।

Lab code-এ model input হিসেবে DataFrame shape ধরে রাখার জন্য:

```python
df[["MedInc"]]
```

ব্যবহার করা হয়েছে।

---

# 64. Simple Model তৈরি

```python
simple_model = LinearRegression()
```

এখানে Scikit-learn-এর Linear Regression model তৈরি হলো।

---

# 65. Model Train করা

```python
simple_model.fit(
    X_train_simple,
    Y_train_simple
)
```

`fit()` মানে:

> Training data ব্যবহার করে model-এর parameters শেখানো।

অর্থাৎ:

```text
Training Data
      ↓
fit()
      ↓
Learn relationship
```

---

# 66. Prediction

Training-এর পরে:

```python
Y_pred_simple = simple_model.predict(X_test_simple)
```

এখানে model test features দেখে predicted house prices তৈরি করছে।

```text
X_test
  ↓
Trained Model
  ↓
Y_pred
```

---

# 67. Actual বনাম Predicted

ধরো:

```text
Actual Price     Predicted Price

2.5              2.3
3.0              3.1
1.8              1.9
```

এখানে:

```text
Actual = সত্যিকারের value

Predicted = Model-এর অনুমান
```

দুটোর difference-ই model error-এর অংশ।

---

# 68. Regression Line

Simple Linear Regression-এর সবচেয়ে সুন্দর visual হলো regression line।

Code:

```python
plt.scatter(
    X_test_simple,
    Y_test_simple,
    label="Actual Prices"
)

plt.plot(
    X_test_simple,
    Y_pred_simple,
    label="Regression Line"
)
```

এখানে:

```text
Dots/Points → Actual Prices

Line → Model's predicted relationship
```

---

# 69. Graph কীভাবে বুঝবে?

Graph-এ:

```text
Price
  |
  |       •
  |     •
  |   •
  |  /──────── Regression Line
  | /
  |________________ Income
```

Regression line actual points-এর overall trend represent করার চেষ্টা করে।

---

# 70. Simple Regression-এর Mathematical Connection

এখানে:

```text
X = MedInc
Y = Price
```

তাই model-এর equation conceptually:

```text
Price = m(MedInc) + c
```

Model নিজে:

```text
m
c
```

learn করে।

---

# 71. Multiple Linear Regression

এবার আমরা শুধু MedInc নয়, **সব available features** ব্যবহার করব।

```text
Feature 1
Feature 2
Feature 3
...
Feature n
     ↓
Linear Regression
     ↓
Price
```

এটাই Multiple Linear Regression।

---

# 72. Multiple Model Train

Code:

```python
multi_model = LinearRegression()

multi_model.fit(
    X_train,
    Y_train
)
```

এখানে:

```text
X_train → সব features
Y_train → Price
```

দিয়ে model train হচ্ছে।

---

# 73. Multiple Regression Prediction

```python
Y_pred_multi = multi_model.predict(X_test)
```

এখানে test-এর সব features ব্যবহার করে Price predict করা হচ্ছে।

---

# 74. Model Evaluation কেন দরকার?

শুধু prediction করলেই হবে না।

আমাদের জানতে হবে:

> Model কতটা ভালো prediction করছে?

তাই evaluation metrics ব্যবহার করি।

Lab-এ তিনটি metric:

```text
MAE
MSE
R²
```

---
# 75. MAE

MAE =

# Mean Absolute Error

সহজভাবে:

> Actual এবং predicted value-এর difference-এর absolute average।

Concept:

```text
Error = Actual - Predicted

Absolute Error = |Actual - Predicted|

MAE = সব Absolute Error-এর Average
```

---

# 76. MAE Example

ধরো:

```text
Actual      Predicted

100         90
200         220
300         280
```

Errors:

```text
100 - 90  = 10
200 - 220 = -20
300 - 280 = 20
```

Absolute errors:

```text
10
20
20
```

MAE:

```text
(10 + 20 + 20) / 3

= 16.67
```

---

# 77. MAE কীভাবে বুঝব?

MAE যত কম:

```text
Prediction Error
      ↓
   কম
```

তত prediction সাধারণত actual values-এর কাছাকাছি।

---

# 78. MSE

MSE =

# Mean Squared Error

এখানে error square করা হয়।

```text
MSE = Average[(Actual - Predicted)²]
```

MAE-এর মতোই error measure করে, কিন্তু বড় errors-কে বেশি গুরুত্ব দেয় কারণ error square করা হয়।

---

# 79. MSE Example

Errors:

```text
10
-20
20
```

Square:

```text
100
400
400
```

Average:

```text
(100 + 400 + 400) / 3

= 300
```

তাই:

```text
MSE = 300
```

---

# 80. MAE vs MSE

```text
MAE
→ Absolute Error
→ সহজে interpret করা যায়

MSE
→ Squared Error
→ বড় error-কে বেশি penalize করে
```

দুটোর ক্ষেত্রেই সাধারণভাবে:

```text
Lower → Better
```

তবে metric-এর scale আলাদা হওয়ায় raw MAE আর MSE-এর number সরাসরি compare করা উচিত নয়।

---

# 81. R² Score

R² =

# R-squared

এটা বলে model target-এর variation কতটা explain করতে পারছে।

সহজভাবে:

> Model data-এর relationship কতটা ভালোভাবে capture করছে তার একটি measure।

---

# 82. R²-এর Basic Idea

সাধারণভাবে:

```text
R² closer to 1
→ better fit

R² around 0
→ model খুব কম explanatory power দেখাচ্ছে

R² negative
→ কিছু পরিস্থিতিতে খুব poor fit হতে পারে
```

Lab material-এ মূলত বলা হয়েছে:

> R² value 1-এর কাছাকাছি হলে fit ভালো।

---

# 83. R² Example

ধরো:

```text
R² = 0.90
```

Conceptually model target-এর variation-এর বড় অংশ explain করছে।

আর:

```text
R² = 0.30
```

হলে model তুলনামূলকভাবে কম variation explain করছে।

---

# 84. Metrics-এর Code

Simple regression:

```python
mean_absolute_error(
    Y_test_simple,
    Y_pred_simple
)

mean_squared_error(
    Y_test_simple,
    Y_pred_simple
)

r2_score(
    Y_test_simple,
    Y_pred_simple
)
```

Multiple regression:

```python
mean_absolute_error(
    Y_test,
    Y_pred_multi
)

mean_squared_error(
    Y_test,
    Y_pred_multi
)

r2_score(
    Y_test,
    Y_pred_multi
)
```

---
# 85. খুব Important: Provided Code-এর একটি Label Issue

Source code-এ Simple Linear Regression-এর prediction-এর পর print করা হয়েছে:

```python
print("\nMultiple Linear Regression Performance:")
```

কিন্তু ওই অংশটি আসলে:

```text
Simple Linear Regression
```

এর performance।

অর্থাৎ print text-টা conceptually mismatch করেছে।

**Code-এর মূল calculation বোঝার সময় heading-এর চেয়ে কোন variables ব্যবহার হচ্ছে সেটা follow করবে।**

---

# 86. Feature Importance

Multiple Linear Regression-এ প্রতিটি feature-এর একটি coefficient থাকে।

Code:

```python
coefficients = pd.DataFrame({
    "Feature": X.columns,
    "Coefficient": multi_model.coef_
})
```

এখানে একটি নতুন DataFrame তৈরি হচ্ছে।

দুটি column:

```text
Feature
Coefficient
```

---

# 87. `multi_model.coef_`

এই অংশ:

```python
multi_model.coef_
```

model শেখা coefficients দেয়।

যেমন hypothetical:

```text
Feature       Coefficient

MedInc        0.85
HouseAge      0.10
AveRooms      0.30
Population   -0.20
```

---

# 88. Coefficient কী বোঝায়?

Coefficient-এর:

```text
Sign → Direction
Magnitude → Relationship-এর strength-এর indication
```

যেমন:

```text
+0.8
```

positive relationship।

```text
-0.5
```

negative relationship।

কিন্তু coefficient-এর magnitude compare করার সময় feature scaling এবং feature units-এর বিষয় মাথায় রাখতে হয়।

---

# 89. Coefficients Sort করা

Code:

```python
coefficients = coefficients.sort_values(
    by="Coefficient",
    ascending=False
)
```

মানে coefficient বড় থেকে ছোট সাজানো হচ্ছে।

```text
Largest
 ↓
...
 ↓
Smallest
```

---

# 90. Feature Importance Barplot

Code:

```python
sns.barplot(
    x="Coefficient",
    y="Feature",
    data=coefficients
)
```

এতে প্রতিটি feature-এর coefficient bar আকারে দেখা যায়।

তারপর:

```python
plt.title(
    "Feature Importance in Linear Regression"
)
```

graph-এর title।

---

# 91. Feature Selection কী?

Feature Selection মানে:

> Prediction-এর জন্য relevant features নির্বাচন করা।

ধরো dataset-এ 10টি feature আছে:

```text
X1
X2
X3
...
X10
```

সবগুলো ব্যবহার করার বদলে analysis করে হয়তো কিছু feature বাদ দেওয়া যায়।

---

# 92. Feature Importance এবং Feature Selection এক জিনিস নয়

এটা মনে রাখা ভালো।

```text
Feature Importance
→ কোন feature model-এ কতটা contribution/relationship দেখাচ্ছে তা examine করা।

Feature Selection
→ কোন features model-এর জন্য রাখব/বাদ দেব সেই decision process।
```

এই Lab-এ coefficients ব্যবহার করে feature impact examine করা হচ্ছে।

---
# 93. পুরো Lab-এর Complete Flow

এখন পুরো Lab-টা একসাথে:

```text
                Dataset
                   ↓
             Load Dataset
                   ↓
              DataFrame
                   ↓
                  EDA
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
 Summary Statistics      Correlation
        ↓                     ↓
 Missing Check          Heatmap
        └──────────┬──────────┘
                   ↓
            X and Y Split
                   ↓
          Train/Test Split
                   ↓
          Feature Scaling
                   ↓
       ┌───────────┴───────────┐
       ↓                       ↓
Simple Regression      Multiple Regression
       ↓                       ↓
Prediction              Prediction
       ↓                       ↓
       └───────────┬───────────┘
                   ↓
              Evaluation
                   ↓
             MAE / MSE / R²
                   ↓
          Coefficient Analysis
                   ↓
           Feature Selection
```

---

# 94. Simple Linear Regression-এর Full Concept

```text
One Feature
    ↓
MedInc
    ↓
LinearRegression()
    ↓
Train
    ↓
Predict Price
    ↓
Regression Line
    ↓
Evaluate
```

Mathematics:

```text
Price = m × MedInc + c
```

---

# 95. Multiple Linear Regression-এর Full Concept

```text
Many Features
      ↓
X1, X2, X3, ... Xn
      ↓
LinearRegression()
      ↓
Train
      ↓
Predict Price
      ↓
Evaluate
```

Mathematics:

```text
Price = β₀
      + β₁X₁
      + β₂X₂
      + ...
      + βₙXₙ
```

---

# 96. একটি Real-Life Example

ধরো তুমি একটি house-এর price predict করতে চাও।

Information:

```text
Median Income
House Age
Average Rooms
Population
...
```

এই সব information হলো:

```text
Features
```

Actual house price:

```text
Target
```

Machine Learning flow:

```text
Features
   ↓
Linear Regression
   ↓
Predicted Price
```

তারপর:

```text
Actual Price
     vs
Predicted Price
```

compare করে model-এর performance বের করা হয়।

---
# 97. Lab-এর Important Python Pattern

Dataset load:

```python
data = fetch_california_housing()

df = pd.DataFrame(
    data.data,
    columns=data.feature_names
)

df["Price"] = data.target
```

---

# 98. EDA Pattern

```python
print(df.head())

print(df.describe())

print(df.isnull().sum())

print(df.corr())
```

Visualization:

```python
sns.heatmap(df.corr(), annot=True)
plt.show()
```

---

# 99. Train/Test Pattern

```python
X = df.drop(columns=["Price"])
Y = df["Price"]

X_train, X_test, Y_train, Y_test = train_test_split(
    X,
    Y,
    test_size=0.2,
    random_state=42
)
```

মনে রাখো:

```text
X → Input
Y → Output

Train → Learn
Test → Evaluate
```

---

# 100. Scaling Pattern

```python
scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)

X_test = scaler.transform(X_test)
```

মনে রাখবে:

```text
Train → fit_transform()

Test → transform()
```

---

# 101. Model Training Pattern

Simple:

```python
model = LinearRegression()

model.fit(X_train, Y_train)
```

Prediction:

```python
prediction = model.predict(X_test)
```

---

# 102. Evaluation Pattern

```python
MAE = mean_absolute_error(
    Y_test,
    prediction
)

MSE = mean_squared_error(
    Y_test,
    prediction
)

R2 = r2_score(
    Y_test,
    prediction
)
```

Concept:

```text
MAE → Average absolute error
MSE → Average squared error
R²  → Model fit/explanatory power
```

---

# 103. Coefficient Pattern

```python
coefficients = pd.DataFrame({
    "Feature": X.columns,
    "Coefficient": model.coef_
})
```

তারপর:

```python
coefficients.sort_values(
    by="Coefficient",
    ascending=False
)
```

---

# 104. Exam-এর জন্য Important Definitions

## Linear Regression

> Linear Regression is a supervised machine learning algorithm used to predict continuous numerical values by modeling a linear relationship between input features and a target variable.

---

## Simple Linear Regression

> Simple Linear Regression uses one input feature to predict a continuous target variable.

Formula:

```text
Y = mX + c
```

---

## Multiple Linear Regression

> Multiple Linear Regression uses two or more input features to predict a continuous target variable.

Formula:

```text
Y = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
```

---

## Regression

> Regression is a supervised learning task used to predict continuous numerical values.

---

## MAE

> MAE is the average absolute difference between actual and predicted values.

---

## MSE

> MSE is the average of squared differences between actual and predicted values.

---

## R²

> R² measures how well the regression model explains the variation in the target variable.

---

## Correlation

> Correlation measures the strength and direction of the relationship between two variables.

---

## Feature Scaling

> Feature scaling transforms numerical features to a common or standardized scale.

---

## Feature Selection

> Feature selection is the process of selecting relevant features for model training.

---

# 105. Most Important Differences

## Simple vs Multiple Regression

```text
Simple
→ One feature

Multiple
→ Multiple features
```

---

## MAE vs MSE

```text
MAE
→ Absolute error
→ Easy to interpret
→ Lower generally better

MSE
→ Squared error
→ Large errors receive more penalty
→ Lower generally better
```

---

## Training vs Testing

```text
Training
→ Model learns

Testing
→ Model is evaluated
```

---

## X vs Y

```text
X
→ Features/Input

Y
→ Target/Output
```

---

## Actual vs Predicted

```text
Actual
→ Real value from dataset

Predicted
→ Model-এর estimated value
```

---
# 106. Quick Revision Table

| Term                | সহজ অর্থ                            |
| ------------------- | ----------------------------------- |
| Linear Regression   | Continuous value predict করার model |
| Regression          | Number predict করা                  |
| Simple Regression   | 1 feature                           |
| Multiple Regression | Multiple features                   |
| X                   | Input features                      |
| Y                   | Target                              |
| m                   | Slope                               |
| c                   | Intercept                           |
| β                   | Coefficients                        |
| Training            | Model শেখানো                        |
| Testing             | Model পরীক্ষা                       |
| Prediction          | Model-এর estimated output           |
| MAE                 | Average absolute error              |
| MSE                 | Average squared error               |
| R²                  | Model কতটা variation explain করছে   |
| Correlation         | দুই variable-এর relationship        |
| Scaling             | Feature-এর scale adjust করা         |
| StandardScaler      | Standardization করা                 |
| Coefficient         | Feature-এর learned coefficient      |

---

# 107. One-Minute Memory Map

শেষ মুহূর্তে revision করার সময়:

```text
LINEAR REGRESSION
        ↓
Continuous Value Prediction
        ↓
     ┌──┴──┐
     ↓     ↓
 Simple  Multiple
   ↓        ↓
1 Feature  Many Features
   ↓        ↓
Y=mX+c    Y=β₀+β₁X₁+...
        ↓
      Dataset
        ↓
       EDA
        ↓
     X / Y Split
        ↓
   Train / Test
        ↓
      Scaling
        ↓
     Training
        ↓
    Prediction
        ↓
   MAE / MSE / R²
        ↓
   Coefficients
        ↓
 Feature Analysis
```

---

# 108. সবচেয়ে Important কথা

এই Lab-কে এক লাইনে মনে রাখো:

> **Linear Regression হলো এমন একটি supervised learning method যা input feature(s) এবং continuous target-এর মধ্যে linear relationship শিখে target predict করে।**

আর পুরো practical process:

```text
Dataset
 ↓
Understand Data
 ↓
EDA
 ↓
Separate X and Y
 ↓
Train/Test Split
 ↓
Scale Features
 ↓
Train Linear Regression
 ↓
Predict
 ↓
Evaluate
 ↓
Analyze Coefficients
```
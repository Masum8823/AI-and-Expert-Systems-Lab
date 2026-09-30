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

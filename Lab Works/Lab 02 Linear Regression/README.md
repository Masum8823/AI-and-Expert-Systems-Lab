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
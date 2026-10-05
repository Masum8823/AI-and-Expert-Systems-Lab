# AI Lab 02 – Linear Regression Using Diabetes Dataset

## 1. Lab Overview

এই Lab-এ আমরা **Diabetes Dataset** ব্যবহার করে **Linear Regression** শিখব এবং implement করব।

এই Lab-এর মূল উদ্দেশ্য হলো:

* Dataset load করা
* Dataset explore করা
* Missing values check করা
* Statistical summary দেখা
* Correlation analysis করা
* Features এবং Target আলাদা করা
* Training এবং Testing data তৈরি করা
* Feature standardize করা
* Simple Linear Regression implement করা
* BMI ব্যবহার করে diabetes progression predict করা
* Regression line visualize করা
* Multiple Linear Regression implement করা
* MAE, MSE এবং R² দিয়ে model evaluate করা
* Regression coefficients দেখে feature importance বোঝা

---

# 2. Linear Regression কী?

**Linear Regression** হলো একটি **Supervised Machine Learning algorithm** যা input feature ব্যবহার করে একটি numerical/continuous output predict করতে পারে।

সহজভাবে:

> Input data দেখে একটি numerical value predict করার জন্য Linear Regression ব্যবহার করা হয়।

এই Lab-এ আমরা Diabetes dataset-এর medical features ব্যবহার করে **diabetes progression score** predict করেছি।

---

# 3. Supervised Learning কী?

Linear Regression হলো **Supervised Learning** algorithm।

Supervised Learning-এ আমাদের data-এর সাথে:

```text
Input → Feature
Output → Target
```

দুটিই দেওয়া থাকে।

Model input এবং target-এর relationship শিখে নতুন input-এর জন্য target predict করে।

---

# 4. Regression কী?

Regression এমন একটি machine learning problem যেখানে output সাধারণত একটি **continuous numerical value**।

Example:

```text
House Price
Temperature
Salary
Diabetes Progression Score
```

এই Lab-এ target হলো:

```text
Diabetes Progression Score
```

তাই এটি একটি regression problem।

---

# 5. Classification vs Regression

| Regression                  | Classification                  |
| --------------------------- | ------------------------------- |
| Numerical value predict করে | Category/Class predict করে      |
| Output continuous হতে পারে  | Output class/category           |
| Example: Price = 50000      | Example: Diabetes / No Diabetes |
| Linear Regression           | Logistic Regression             |

এই Lab-এ আমরা **Regression** করছি কারণ target একটি numerical progression score।

---

# 6. Required Libraries

এই Lab-এ নিচের Python libraries ব্যবহার করা হয়েছে:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import load_diabetes
```

---

# 7. NumPy

```python
import numpy as np
```

NumPy numerical calculation এবং array-related কাজের জন্য ব্যবহার করা হয়।

---

# 8. Pandas

```python
import pandas as pd
```

Pandas dataset নিয়ে কাজ করার জন্য ব্যবহার করা হয়।

যেমন:

* DataFrame তৈরি করা
* Data load করা
* Column select করা
* Data inspect করা
* Data preprocessing করা

---

# 9. Matplotlib

```python
import matplotlib.pyplot as plt
```

Graph এবং visualization তৈরি করার জন্য Matplotlib ব্যবহার করা হয়।

---

# 10. Seaborn

```python
import seaborn as sns
```

Statistical visualization তৈরি করার জন্য Seaborn ব্যবহার করা হয়।

এই Lab-এ ব্যবহার হয়েছে:

* Heatmap
* Regression plot
* Bar plot

---

# 11. train_test_split

```python
from sklearn.model_selection import train_test_split
```

Dataset-কে training এবং testing অংশে ভাগ করার জন্য ব্যবহার করা হয়।

---

# 12. LinearRegression

```python
from sklearn.linear_model import LinearRegression
```

Linear Regression model তৈরি করার জন্য ব্যবহার করা হয়।

---

# 13. Evaluation Metrics

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
```

Model-এর performance measure করার জন্য ব্যবহার করা হয়।

এখানে তিনটি metric:

```text
MAE
MSE
R²
```

ব্যবহার করা হয়েছে।

---

# 14. StandardScaler

```python
from sklearn.preprocessing import StandardScaler
```

Features-কে standardize করার জন্য ব্যবহার করা হয়।

---

# 15. load_diabetes()

```python
from sklearn.datasets import load_diabetes
```

Scikit-learn-এর built-in Diabetes dataset load করার জন্য ব্যবহার করা হয়।

---

# 16. Load Diabetes Dataset

Dataset load করার জন্য:

```python
diabetes_data = load_diabetes()
```

এটি scikit-learn-এর built-in Diabetes dataset load করে।

তারপর DataFrame তৈরি করা হয়েছে:

```python
diabetes_df = pd.DataFrame(
    diabetes_data.data,
    columns=diabetes_data.feature_names
)
```

এখানে:

```text
diabetes_data.data
```

থেকে feature data নেওয়া হয়েছে।

আর:

```text
diabetes_data.feature_names
```

থেকে column names নেওয়া হয়েছে।

---

# 17. Target Column Add করা

Dataset-এর target আলাদা করে DataFrame-এ add করা হয়েছে:

```python
diabetes_df["target"] = diabetes_data.target
```

এখন DataFrame-এর মধ্যে features এবং target দুটোই আছে।

---

# 18. First Five Rows দেখা

```python
print(diabetes_df.head())
```

`head()` dataset-এর প্রথম ৫টি row দেখায়।

### মনে রাখবে

```text
head()
→ First 5 rows
```

---
# 19. Dataset-এর Basic Structure

এই dataset-এ বিভিন্ন medical features আছে এবং একটি target value আছে।

Features model-এর input হিসেবে কাজ করবে।

Target হলো model-এর prediction output।

সহজভাবে:

```text
Features
   ↓
Machine Learning Model
   ↓
Target Prediction
```

---

# Task 1: Data Exploration

Data exploration মানে model বানানোর আগে dataset সম্পর্কে basic information জানা।

এই Lab-এ তিনটি প্রধান exploration করা হয়েছে:

1. Missing Values Check
2. Statistical Summary
3. Correlation Heatmap

---

# 20. Missing Values Check

Missing value আছে কি না দেখার জন্য:

```python
missing_values = diabetes_df.isnull().sum()

print(missing_values)
```

---

## `isnull()`

```python
diabetes_df.isnull()
```

প্রতিটি value missing কি না check করে।

Missing হলে:

```text
True
```

না হলে:

```text
False
```

---

## `sum()`

```python
diabetes_df.isnull().sum()
```

প্রতিটি column-এ কতগুলো missing value আছে তা count করে।

### মনে রাখবে

```text
isnull()
→ Missing values identify

sum()
→ Missing values count
```

---

# 21. Summary Statistics

Dataset-এর statistical summary দেখতে:

```python
print(diabetes_df.describe())
```

`describe()` থেকে numerical data-এর বিভিন্ন statistics পাওয়া যায়।

যেমন:

* Count
* Mean
* Standard deviation
* Minimum
* 25%
* 50%
* 75%
* Maximum

---

# 22. Mean

Mean হলো average value।

উদাহরণ:

```text
10, 20, 30
```

Mean:

```text
(10 + 20 + 30) / 3 = 20
```

---

# 23. Standard Deviation

Standard deviation data কতটা spread বা ছড়ানো তা বোঝাতে সাহায্য করে।

সহজভাবে:

> Data values mean-এর আশেপাশে কতটা spread হয়েছে তা বোঝায়।

---

# 24. Correlation

Correlation দুইটি numerical variable-এর মধ্যে relationship বোঝাতে সাহায্য করে।

Correlation সাধারণত:

```text
-1 থেকে +1
```

এর মধ্যে থাকে।

### Positive Correlation

Value `+1`-এর দিকে হলে positive relationship strong।

অর্থাৎ একটি variable বাড়লে অন্যটিও বাড়ার tendency থাকতে পারে।

### Negative Correlation

Value `-1`-এর দিকে হলে negative relationship strong।

অর্থাৎ একটি variable বাড়লে অন্যটি কমার tendency থাকতে পারে।

### Near Zero

Value `0`-এর কাছাকাছি হলে strong linear relationship কম।

---
# 25. Correlation Heatmap

Correlation calculate:

```python
corr = diabetes_df.corr()
```

তারপর heatmap:

```python
plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm"
)

plt.title("Correlation Heatmap")

plt.show()
```

---

# 26. Heatmap-এর কাজ

Heatmap ব্যবহার করে একসাথে অনেকগুলো feature-এর correlation দেখা যায়।

এই Lab-এ আমরা দেখতে পারি:

```text
Feature ↔ Feature
Feature ↔ Target
```

এর relationship।

---

# 27. `annot=True`

```python
annot=True
```

ব্যবহার করলে heatmap-এর প্রতিটি cell-এর মধ্যে numerical correlation value দেখা যায়।

---

# 28. `fmt=".2f"`

```python
fmt=".2f"
```

এর অর্থ value দুই decimal place পর্যন্ত দেখানো হবে।

Example:

```text
0.4567
```

হয়ে যাবে:

```text
0.46
```

---
# Task 2: Data Preprocessing

Model তৈরি করার আগে dataset prepare করতে হয়।

এই Lab-এ preprocessing-এর প্রধান ধাপ:

```text
Features এবং Target আলাদা
        ↓
Train-Test Split
        ↓
Feature Standardization
```

---

# 29. Features এবং Target আলাদা করা

Code:

```python
X = diabetes_df.drop(columns=["target"])
y = diabetes_df["target"]
```

এখানে:

```text
X → Features / Input
y → Target / Output
```

---

# 30. `X` কী?

```python
X = diabetes_df.drop(columns=["target"])
```

এখানে target column বাদ দিয়ে বাকি সব columns নেওয়া হয়েছে।

তাই:

```text
X = Input Features
```

---

# 31. `y` কী?

```python
y = diabetes_df["target"]
```

এখানে শুধু target column নেওয়া হয়েছে।

তাই:

```text
y = Target
```

---

# 32. সহজভাবে X এবং y

```text
X
↓
Input Features
↓
Model-কে দেওয়া হবে

y
↓
Actual Target
↓
Model যেটা predict করবে
```

---

# 33. Train-Test Split

Dataset-কে দুই ভাগে ভাগ করা হয়েছে:

```text
80% → Training
20% → Testing
```

Code:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

---

# 34. Training Data

Training data model শেখানোর জন্য ব্যবহার করা হয়।

```text
Training Data
      ↓
Model learns relationship
```

---

# 35. Testing Data

Testing data model training-এর সময় ব্যবহার করা হয় না।

Training শেষে নতুন/unseen data-এর উপর model কত ভালো predict করতে পারে তা test করার জন্য testing data ব্যবহার করা হয়।

```text
Test Data
   ↓
Model Prediction
   ↓
Actual Value-এর সাথে Compare
```

---

# 36. `test_size=0.2`

```python
test_size=0.2
```

মানে dataset-এর:

```text
20% → Test
80% → Train
```

---

# 37. `random_state=42`

```python
random_state=42
```

Dataset split করার সময় একই random result পাওয়ার জন্য ব্যবহার করা হয়েছে।

সহজভাবে:

> একই code আবার run করলে একইভাবে data split পাওয়ার জন্য `random_state` ব্যবহার করা হয়।

`42` এখানে একটি fixed seed value।

---

# 38. Standardization

Features-এর scale একই নয়।

তাই model training-এর আগে features standardize করা হয়েছে।

এর জন্য:

```python
standardizer = StandardScaler()
```

ব্যবহার করা হয়েছে।

---

# 39. StandardScaler কী?

`StandardScaler` feature values-কে standard scale-এ transform করে।

সাধারণভাবে standardization-এর পরে:

```text
Mean ≈ 0
Standard Deviation ≈ 1
```

হয়।

---

# 40. Training Data Standardize

```python
X_train_scaled = standardizer.fit_transform(X_train)
```

এখানে `fit_transform()` ব্যবহার করা হয়েছে।

এটি training data থেকে scaling information শেখে এবং তারপর training data transform করে।

---

# 41. Test Data Standardize

```python
X_test_scaled = standardizer.transform(X_test)
```

এখানে শুধু:

```text
transform()
```

ব্যবহার করা হয়েছে।

কারণ test data-এর জন্য নতুন করে scaler fit করা উচিত নয়।

একই training-based transformation test data-তে apply করা হয়।

---

# 42. `fit_transform()` vs `transform()`

### Training Data

```python
standardizer.fit_transform(X_train)
```

মানে:

```text
Fit + Transform
```

### Testing Data

```python
standardizer.transform(X_test)
```

মানে:

```text
শুধু Transform
```

### মনে রাখার সহজ নিয়ম

```text
Training → fit_transform()
Testing  → transform()
```

---
# Task 3: Simple Linear Regression

## 43. Simple Linear Regression কী?

Simple Linear Regression-এ মাত্র **একটি input feature** ব্যবহার করা হয়।

সাধারণ equation:

```text
Y = mX + c
```

যেখানে:

```text
Y → Predicted Output
X → Input Feature
m → Slope/Coefficient
c → Intercept
```

---

# 44. এই Lab-এ Simple Regression

এই Lab-এ:

```text
Input  → BMI
Target → Diabetes Progression
```

অর্থাৎ BMI ব্যবহার করে diabetes progression score predict করা হয়েছে।

---

# 45. BMI Select করা

```python
bmi_data = diabetes_df[["bmi"]]
target_data = diabetes_df["target"]
```

এখানে:

```text
bmi_data
→ শুধু BMI feature

target_data
→ Target value
```

---

# 46. কেন Double Bracket?

```python
diabetes_df[["bmi"]]
```

এখানে double bracket ব্যবহার করার কারণে result DataFrame হিসেবে থাকে।

অন্যদিকে:

```python
diabetes_df["bmi"]
```

সাধারণত Series return করে।

Machine Learning-এর জন্য feature input হিসেবে DataFrame format রাখা সুবিধাজনক।

---

# 47. BMI Data Split

BMI এবং target-কে training/testing ভাগে ভাগ করা হয়েছে:

```python
bmi_train, bmi_test, target_train, target_test = train_test_split(
    bmi_data,
    target_data,
    test_size=0.2,
    random_state=42
)
```

এখানেও:

```text
80% → Training
20% → Testing
```

---

# 48. Simple Regression Model তৈরি

```python
simple_regression = LinearRegression()
```

এখানে `LinearRegression()` ব্যবহার করে model তৈরি করা হয়েছে।

---

# 49. Model Training

```python
simple_regression.fit(
    bmi_train,
    target_train
)
```

`fit()` model-কে training data দিয়ে relationship শেখায়।

সহজভাবে:

```text
BMI + Actual Target
       ↓
     fit()
       ↓
Model learns relationship
```

---

# 50. Prediction

Training-এর পর test BMI values ব্যবহার করে prediction করা হয়েছে:

```python
simple_predictions = simple_regression.predict(
    bmi_test
)
```

এখানে:

```text
bmi_test
   ↓
Model
   ↓
Predicted Target
```

---

# 51. `predict()`

```python
model.predict(data)
```

নতুন input data-এর জন্য predicted output তৈরি করে।

---
# 52. Regression Line

Simple Linear Regression-এর relationship graph-এ দেখানো হয়েছে।

```python
sns.regplot(
    x=bmi_test["bmi"],
    y=target_test,
    scatter_kws={"alpha": 0.7},
    line_kws={"linewidth": 2}
)
```

এখানে:

```text
X-axis → BMI
Y-axis → Diabetes Progression
```

এবং regression line estimated relationship দেখায়।

---

# 53. `regplot()`

Seaborn-এর:

```python
sns.regplot()
```

scatter data-এর সাথে একটি regression line দেখাতে পারে।

এই Lab-এ এটি BMI এবং target-এর relationship visualize করতে ব্যবহৃত হয়েছে।

---

# 54. Regression Line কী বোঝায়?

Regression line হলো এমন একটি estimated straight line যা input এবং output-এর relationship represent করে।

সহজভাবে:

```text
BMI
 ↓
Regression Model
 ↓
Estimated Diabetes Progression
```

---
# Task 4: Multiple Linear Regression

# 55. Multiple Linear Regression কী?

Multiple Linear Regression-এ একাধিক input feature ব্যবহার করা হয়।

Simple Linear Regression:

```text
Y = mX + c
```

Multiple Linear Regression:

```text
Y = β₀ + β₁X₁ + β₂X₂ + β₃X₃ + ... + βₙXₙ
```

এখানে একাধিক feature model-এর input হিসেবে কাজ করে।

---

# 56. Simple vs Multiple Linear Regression

| Simple Linear Regression | Multiple Linear Regression |
| ------------------------ | -------------------------- |
| একটি feature             | একাধিক feature             |
| BMI ব্যবহার করা হয়েছে    | সব available features      |
| সহজ model                | তুলনামূলকভাবে complex      |
| `Y = mX + c`             | `Y = β₀ + β₁X₁ + ...`      |

---

# 57. Multiple Regression Model তৈরি

```python
multiple_regression = LinearRegression()
```

তারপর training:

```python
multiple_regression.fit(
    X_train_scaled,
    y_train
)
```

এখানে সব standardized features ব্যবহার করা হয়েছে।

---

# 58. Multiple Regression Prediction

```python
multiple_predictions = multiple_regression.predict(
    X_test_scaled
)
```

এখানে test features ব্যবহার করে target prediction করা হয়েছে।

---

# 59. Model Evaluation

Prediction করার পর দেখতে হবে model কত ভালো কাজ করেছে।

এই Lab-এ তিনটি metric ব্যবহার করা হয়েছে:

```text
1. MAE
2. MSE
3. R²
```

---

# 60. MAE — Mean Absolute Error

Full form:

> Mean Absolute Error

Code:

```python
mae_value = mean_absolute_error(
    y_test,
    multiple_predictions
)
```

MAE actual value এবং predicted value-এর absolute difference-এর average।

সহজভাবে:

> Model-এর prediction গড়ে actual value থেকে কতটা দূরে আছে তা MAE বোঝায়।

### MAE-এর ক্ষেত্রে

```text
Lower MAE → Better
```

সাধারণভাবে error যত কম, model তত ভালো।

---

# 61. MSE — Mean Squared Error

Full form:

> Mean Squared Error

Code:

```python
mse_value = mean_squared_error(
    y_test,
    multiple_predictions
)
```

MSE prediction error-এর square-এর average।

সহজভাবে:

> Actual এবং predicted value-এর difference বের করে সেটাকে square করে average করা হয়।

### MSE-এর ক্ষেত্রে

```text
Lower MSE → Better
```

---

# 62. R² — R-squared

Full form:

> R-squared

Code:

```python
r2_value = r2_score(
    y_test,
    multiple_predictions
)
```

R² model target-এর variation-এর কত অংশ explain করতে পারছে তা বোঝাতে সাহায্য করে।

সহজভাবে:

> Model data-এর pattern কতটা ভালোভাবে explain করতে পারছে তা R² দিয়ে বোঝা যায়।

### সাধারণ ধারণা

```text
R² বেশি → Better fit
```

---

# 63. MAE, MSE এবং R² একসাথে

| Metric | কী বোঝায়               | সাধারণভাবে    |
| ------ | ---------------------- | ------------- |
| MAE    | Average absolute error | Lower better  |
| MSE    | Average squared error  | Lower better  |
| R²     | Explained variation    | Higher better |

---

# 64. Model Evaluation Code

```python
mae_value = mean_absolute_error(
    y_test,
    multiple_predictions
)

mse_value = mean_squared_error(
    y_test,
    multiple_predictions
)

r2_value = r2_score(
    y_test,
    multiple_predictions
)

print("Multiple Linear Regression Results:")
print("Mean Absolute Error (MAE):", mae_value)
print("Mean Squared Error (MSE):", mse_value)
print("R-squared (R²) Score:", r2_value)
```

---

# Task 5: Feature Importance Analysis

# 65. Regression Coefficient কী?

Linear Regression model-এর প্রতিটি feature-এর একটি coefficient থাকে।

এই coefficient feature এবং prediction-এর relationship সম্পর্কে information দেয়।

Multiple Linear Regression-এর equation:

```text
Y = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
```

এখানে:

```text
β₁, β₂, ... βₙ
```

হলো feature coefficients।

---

# 66. Coefficient Positive হলে

Coefficient positive হলে feature এবং target-এর মধ্যে positive relationship-এর indication থাকতে পারে।

সহজভাবে:

```text
Feature ↑
   ↓
Prediction ↑
```

এমন relationship model-এ দেখা যেতে পারে।

---

# 67. Coefficient Negative হলে

Coefficient negative হলে negative relationship-এর indication থাকতে পারে।

সহজভাবে:

```text
Feature ↑
   ↓
Prediction ↓
```

এমন relationship model-এ দেখা যেতে পারে।

---

# 68. Feature Coefficients বের করা

```python
feature_coefficients = pd.DataFrame({
    "Feature": X.columns,
    "Coefficient": multiple_regression.coef_
})
```

এখানে একটি DataFrame তৈরি করা হয়েছে যেখানে:

```text
Feature
Coefficient
```

দুটি column আছে।

---

# 69. Coefficients Sort করা

```python
feature_coefficients = feature_coefficients.sort_values(
    by="Coefficient",
    ascending=False
)
```

এতে coefficient অনুযায়ী features সাজানো হয়।

`ascending=False` অর্থ বড় value আগে থাকবে।

---
# 70. Feature Importance Bar Chart

Coefficients visualise করতে:

```python
plt.figure(figsize=(9, 6))

sns.barplot(
    data=feature_coefficients,
    x="Coefficient",
    y="Feature"
)

plt.title("Feature Importance Based on Regression Coefficients")
plt.xlabel("Coefficient Value")
plt.ylabel("Feature")

plt.show()
```

এই bar chart feature coefficients-এর comparison দেখায়।

---

# 71. Coefficient দিয়ে Feature Comparison

Coefficient-এর sign এবং magnitude দুটোই গুরুত্বপূর্ণ।

### Positive coefficient

```text
Positive relationship-এর indication
```

### Negative coefficient

```text
Negative relationship-এর indication
```

### Larger absolute coefficient

```text
Model-এর prediction-এ তুলনামূলকভাবে stronger contribution-এর indication
```

তবে coefficient-এর magnitude তুলনা করার সময় feature scaling/standardization-এর বিষয়টি গুরুত্বপূর্ণ।

---
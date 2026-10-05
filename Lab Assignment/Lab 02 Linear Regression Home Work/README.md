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

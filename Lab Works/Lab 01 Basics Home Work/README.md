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
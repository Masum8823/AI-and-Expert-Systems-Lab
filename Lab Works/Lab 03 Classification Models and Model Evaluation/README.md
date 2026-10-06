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
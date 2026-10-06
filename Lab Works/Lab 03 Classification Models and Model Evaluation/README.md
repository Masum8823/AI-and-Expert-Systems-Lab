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
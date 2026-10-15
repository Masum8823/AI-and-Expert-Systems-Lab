## 1. Lab Overview

এই Lab-এ **Artificial Neural Network (ANN)** এবং **Convolutional Neural Network (CNN)**-এর প্রাথমিক ধারণা শেখানো হয়েছে। দেওয়া practical code-এ Breast Cancer Dataset ব্যবহার করে একটি **Feedforward Neural Network** তৈরি, train এবং evaluate করা হয়েছে।

এই Lab-এর প্রধান বিষয়গুলো:

- Artificial Neural Network (ANN)
- Feedforward Neural Network
- Neuron, weights এবং bias
- Input layer, hidden layer এবং output layer
- Activation functions: ReLU এবং Sigmoid
- Breast Cancer Dataset
- Features এবং target
- Data visualization ও Exploratory Data Analysis (EDA)
- Feature scaling using StandardScaler
- Train-test split
- TensorFlow ও Keras
- Sequential model
- Dense layer
- Loss function: Binary Cross-Entropy
- Optimizer: Adam
- Accuracy metric
- Epoch এবং validation data
- Training ও validation accuracy graph
- Prediction probability এবং classification threshold
- Classification report
- Confusion matrix
- Single sample prediction
- CNN-এর architecture ও image classification-এর ধারণা

**গুরুত্বপূর্ণ:** Learning Objectives-এ CNN থাকলেও সরবরাহ করা code-এ CNN model তৈরি করা হয়নি। এই code-এ ANN ব্যবহার করে tabular Breast Cancer data classify করা হয়েছে। CNN অংশে তাই architecture ও প্রয়োজনীয় ধারণা আলাদাভাবে ব্যাখ্যা করা হয়েছে।

---
## 2. Artificial Intelligence, Machine Learning এবং Deep Learning

এই তিনটি বিষয় পরস্পরের সঙ্গে সম্পর্কিত।

```text
Artificial Intelligence (AI)
        │
        └── Machine Learning (ML)
                  │
                  └── Deep Learning (DL)
                            │
                            ├── ANN
                            └── CNN
```

- **Artificial Intelligence (AI):** Computer-কে এমন কাজ করানোর বিস্তৃত ক্ষেত্র, যেগুলোতে সাধারণত মানুষের বুদ্ধিমত্তার প্রয়োজন হয়।
- **Machine Learning (ML):** Data থেকে pattern শিখে prediction বা decision করার পদ্ধতি।
- **Deep Learning (DL):** একাধিক layer-যুক্ত neural network ব্যবহার করে data থেকে জটিল pattern শেখার পদ্ধতি।

সহজে মনে রাখো:

```text
AI → বুদ্ধিমান কাজ করানো
ML → Data থেকে শেখা
DL → Multiple neural-network layers দিয়ে শেখা
```

---

## 3. Artificial Neural Network (ANN) কী?

**Artificial Neural Network (ANN)** হলো একটি Machine Learning model, যা মানুষের মস্তিষ্কের neuron-এর কাজ থেকে অনুপ্রাণিত হয়ে তৈরি। এটি input data থেকে pattern শিখে prediction করতে পারে।

সহজভাবে, ANN input নেয়, বিভিন্ন calculation করে এবং output দেয়। Training-এর সময় model তার weights ও biases পরিবর্তন করে prediction উন্নত করার চেষ্টা করে।

উদাহরণ:

```text
Tumor Measurements
        ↓
       ANN
        ↓
Benign / Malignant
```

ANN ব্যবহার করা যায়:

- Classification
- Regression
- Image recognition
- Speech recognition
- Pattern recognition

---
## 4. Biological Neuron এবং Artificial Neuron

মানুষের মস্তিষ্কে neuron signal গ্রহণ ও প্রক্রিয়াকরণ করে। Artificial neuron এই ধারণার একটি mathematical model।

Artificial neuron-এর প্রধান অংশ:

- **Inputs:** Model-এর কাছে আসা data values।
- **Weights:** প্রতিটি input কতটা গুরুত্বপূর্ণ, তা নির্ধারণে সাহায্য করে।
- **Bias:** Weighted sum-কে adjust করে।
- **Activation Function:** Neuron-এর output নির্ধারণ করে।

সাধারণ ধারণা:

```text
Inputs
  ↓
Weights × Inputs
  ↓
Add Bias
  ↓
Activation Function
  ↓
Output
```


একটি neuron-এর basic formula:

\[
z = w_1x_1 + w_2x_2 + \cdots + w_nx_n + b
\]

\[
a = f(z)
\]

যেখানে:

- \(x_i\) = input features
- \(w_i\) = weights
- \(b\) = bias
- \(z\) = weighted sum plus bias
- \(f\) = activation function
- \(a\) = neuron-এর output

---

## 5. Weight এবং Bias কী?

### Weight

Weight নির্ধারণ করে কোনো input feature final calculation-এ কতটা প্রভাব ফেলবে।

যে feature-এর weight বেশি, সেটি model-এর calculation-এ তুলনামূলকভাবে বেশি প্রভাব ফেলতে পারে। তবে weight-এর অর্থ model ও অন্য weights-এর সঙ্গে মিলিয়ে বুঝতে হয়।

### Bias

Bias হলো একটি অতিরিক্ত trainable value, যা weighted sum-কে adjust করে। এটি model-কে আরও flexible হতে সাহায্য করে।

```text
Weighted Sum = (Input × Weight-এর যোগফল) + Bias
```

Training-এর সময় model data অনুযায়ী weights ও biases update করে।

---
## 6. Neural Network-এর Layers

একটি সাধারণ ANN-এ তিন ধরনের layer দেখা যায়।

### 6.1 Input Layer

Input layer feature values গ্রহণ করে। এই Lab-এ প্রতিটি breast cancer sample-এর 30টি numerical feature input হিসেবে ব্যবহৃত হয়।

### 6.2 Hidden Layer

Hidden layer input থেকে pattern শেখে। একটি network-এ এক বা একাধিক hidden layer থাকতে পারে।

এই Lab-এ দুটি hidden Dense layer রয়েছে:

```text
First Hidden Layer  → 32 neurons
Second Hidden Layer → 16 neurons
```

### 6.3 Output Layer

Output layer final prediction দেয়। এই Lab-এ binary classification হওয়ায় output layer-এ একটি neuron আছে।

```text
Input: 30 Features
       ↓
Hidden Layer: 32 Neurons
       ↓
Hidden Layer: 16 Neurons
       ↓
Output Layer: 1 Neuron
       ↓
Probability between 0 and 1
```

---

## 7. Feedforward Neural Network কী?

Feedforward Neural Network হলো এমন neural network যেখানে information input থেকে hidden layer হয়ে output layer-এর দিকে যায়। সাধারণ feedforward pass-এ information সামনের দিকে প্রবাহিত হয়; recurrent loop থাকে না।

এই Lab-এর flow:

```text
Input Features
      ↓
Dense(32, ReLU)
      ↓
Dense(16, ReLU)
      ↓
Dense(1, Sigmoid)
      ↓
Prediction Probability
```

এখানে model input data গ্রহণ করে এবং layer-by-layer calculation করে final probability তৈরি করে।

---

## 8. Dataset Used in This Lab

এই Lab-এ scikit-learn-এর built-in **Breast Cancer Dataset** ব্যবহার করা হয়েছে।

Code:

```python
from sklearn.datasets import load_breast_cancer

data = load_breast_cancer()
```

Dataset-এ breast tumor-এর বিভিন্ন numerical measurement রয়েছে। এই features থেকে model tumor-এর class predict করার চেষ্টা করে।

Dataset-এর feature-এর উদাহরণ:

- mean radius
- mean texture
- mean perimeter
- mean area

এগুলো tumor measurement-সংক্রান্ত numerical features।

---

## 9. Target Variable এবং Class Label

Code:

```python
y = pd.Series(data.target, name='target')
```

scikit-learn-এর এই dataset-এ label mapping হলো:

```text
0 → Malignant
1 → Benign
```

অর্থাৎ model-এর output label 0 হলে Malignant এবং 1 হলে Benign বোঝানো হয়েছে।

**সতর্কতা:** Dataset-এর label mapping অন্য dataset-এ একই হবে—এমন নয়। তাই সবসময় dataset-এর documentation বা target names check করতে হবে।

---

## 10. Required Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import classification_report, confusion_matrix

import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
```

### Library-গুলোর কাজ

| Library / Function | কাজ |
|---|---|
| NumPy | Numerical calculation ও array operations |
| Pandas | DataFrame এবং tabular data handling |
| Matplotlib | Graph আঁকা |
| Seaborn | Statistical visualization |
| `load_breast_cancer()` | Breast Cancer Dataset load করা |
| `train_test_split()` | Data-কে training ও testing ভাগে ভাগ করা |
| `StandardScaler()` | Feature standardization |
| `classification_report()` | Precision, recall, F1-score ইত্যাদি দেখানো |
| `confusion_matrix()` | Actual ও predicted class-এর তুলনা |
| TensorFlow | Machine Learning ও Deep Learning framework |
| Keras `Sequential` | Layer-ভিত্তিক model তৈরি |
| Keras `Dense` | Fully connected neural-network layer তৈরি |

---

## 11. Dataset Load এবং DataFrame তৈরি

Code:

```python
data = load_breast_cancer()

X = pd.DataFrame(
    data.data,
    columns=data.feature_names
)

y = pd.Series(data.target, name='target')
```

ব্যাখ্যা:

- `load_breast_cancer()` dataset load করে।
- `data.data` input feature values দেয়।
- `data.feature_names` feature-গুলোর নাম দেয়।
- `pd.DataFrame()` feature-গুলোকে row ও column-সহ DataFrame-এ রাখে।
- `data.target` target labels দেয়।
- `pd.Series()` target-কে একটি Series হিসেবে রাখে।

এখানে:

```text
X → Input Features
y → Target Labels
```

Machine Learning-এ সাধারণ convention হিসেবে `X` features এবং `y` target বোঝায়।

---
## 12. Dataset-এর Shape দেখা

Code:

```python
print("Shape of dataset:", X.shape)
```

`shape` DataFrame-এর row এবং column-এর সংখ্যা জানায়।

এই Breast Cancer Dataset-এ সাধারণত:

```text
569 rows × 30 features
```

অর্থাৎ:

- 569টি sample বা record
- 30টি input feature

`X.shape` শুধু feature DataFrame-এর shape দেখায়; target column এতে অন্তর্ভুক্ত নয়।

মনে রাখো:

```text
X.shape → (Rows, Columns)
```

---

## 13. X এবং y একসঙ্গে রাখা

Code:

```python
df = X.copy()
df['target'] = y
```

ব্যাখ্যা:

- `X.copy()` দিয়ে X-এর একটি copy তৈরি হয়।
- `df['target'] = y` দিয়ে target column যোগ করা হয়।

এখন `df`-এ feature columns এবং target—দুটোই আছে। এটি মূলত plotting ও exploratory analysis সহজ করার জন্য করা হয়েছে।

```text
df = 30 Feature Columns + 1 Target Column
```

এই dataset-এর ক্ষেত্রে `df`-এর shape হবে 569 rows ও 31 columns।

---

## 14. Exploratory Data Analysis (EDA)

EDA-এর full form **Exploratory Data Analysis**।

Model train করার আগে dataset-এর গঠন, distribution এবং feature-গুলোর সম্পর্ক বোঝার প্রক্রিয়াকে EDA বলে।

এই Lab-এ EDA-এর জন্য ব্যবহার করা হয়েছে:

1. Dataset shape
2. Class distribution count plot
3. Feature correlation heatmap
4. Selected features-এর pair plot

EDA সাহায্য করে data সম্পর্কে ধারণা পেতে; তবে শুধু graph দেখে কোনো model ভালো হবে কি না নিশ্চিত বলা যায় না।

---
## 15. Class Distribution এবং Count Plot

Code:

```python
sns.countplot(x='target', data=df)
plt.title("Class Distribution (0 = Malignant, 1 = Benign)")
plt.show()
```

### `countplot()` কী করে?

`countplot()` প্রতিটি category-তে কতটি sample আছে, তা bar-এর মাধ্যমে দেখায়।

এই Lab-এ:

```text
0 → Malignant
1 → Benign
```

X-axis-এ class label এবং Y-axis-এ sample count দেখানো হয়।

### কেন দরকার?

- দুই class-এ sample-এর সংখ্যা তুলনা করতে।
- Dataset balanced নাকি imbalanced, সে সম্পর্কে ধারণা পেতে।
- কোনো class খুব কম sample নিয়ে আছে কি না দেখতে।

Count plot নিজে class imbalance সমাধান করে না; শুধু distribution দেখায়।

---

## 16. Feature Correlation Heatmap

Code:

```python
plt.figure(figsize=(12, 10))
sns.heatmap(df.corr(), cmap='coolwarm', square=True)
plt.title("Feature Correlation Heatmap")
plt.show()
```

### Correlation কী?

Correlation দুটি numerical variable-এর মধ্যে linear relationship-এর দিক ও শক্তি সম্পর্কে ধারণা দেয়।

Correlation coefficient সাধারণত −1 থেকে +1-এর মধ্যে থাকে:

| মান | সাধারণ ব্যাখ্যা |
|---|---|
| +1-এর কাছাকাছি | Strong positive linear relationship |
| 0-এর কাছাকাছি | দুর্বল বা কোনো linear relationship নেই |
| −1-এর কাছাকাছি | Strong negative linear relationship |

### Heatmap কী দেখায়?

- প্রতিটি cell দুটি column-এর correlation দেখায়।
- Color-এর মাধ্যমে correlation-এর মান বোঝা সহজ হয়।
- `df.corr()` numerical columns-এর pairwise correlation হিসাব করে।
- `figsize=(12, 10)` figure-এর size নির্ধারণ করে।
- `cmap='coolwarm'` color palette নির্বাচন করে।
- `square=True` cell-গুলোকে square আকারে দেখায়।

**মনে রাখবে:** Correlation মানেই causation নয়। দুটি feature correlated হলেই একটিই অন্যটির কারণ—এ কথা বলা যায় না।

---
## 17. Pair Plot

Code:

```python
sns.pairplot(
    df[['mean radius', 'mean texture',
        'mean perimeter', 'mean area', 'target']],
    hue='target'
)
plt.show()
```

`pairplot()` নির্বাচিত numerical features-এর pairwise relationship graph-এ দেখায়।

এই Lab-এ চারটি feature ব্যবহার করা হয়েছে:

- `mean radius`
- `mean texture`
- `mean perimeter`
- `mean area`

`hue='target'` দিয়ে class অনুযায়ী point-গুলোর রং আলাদা করা হয়।

### কেন দরকার?

- Feature-গুলোর মধ্যে relationship দেখা।
- Class 0 ও Class 1-এর data distribution তুলনা করা।
- কোনো feature combination-এ class-গুলো কতটা আলাদা দেখা যায়, তা বোঝা।

Pair plot visualization-এর জন্য; এটি model train করে না।

---

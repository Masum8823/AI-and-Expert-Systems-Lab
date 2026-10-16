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
## 18. Feature Scaling কী?

Dataset-এর বিভিন্ন feature-এর numerical range অনেক আলাদা হতে পারে। Feature scaling তাদের values-কে একটি comparable scale-এ নিয়ে আসে।

উদাহরণ:

```text
Feature A: 1–10
Feature B: 1000–50000
```

বড় numerical range থাকা feature training-কে প্রভাবিত করতে পারে। Neural network-এর ক্ষেত্রে scaling অনেক সময় training-কে আরও stable ও efficient করতে সাহায্য করে।

এই Lab-এ ব্যবহার করা হয়েছে:

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

---
## 19. StandardScaler কী?

`StandardScaler` প্রতিটি feature-কে training data-এর mean ও standard deviation ব্যবহার করে standardize করে।

Formula:

\[
z = \frac{x-\mu}{\sigma}
\]

যেখানে:

- \(x\) = original value
- \(\mu\) = feature-এর mean
- \(\sigma\) = feature-এর standard deviation
- \(z\) = standardized value

Standardized data-এর mean সাধারণত 0-এর কাছাকাছি এবং standard deviation 1-এর কাছাকাছি হয়।

### Code-এর ব্যাখ্যা

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

- `StandardScaler()` scaler object তৈরি করে।
- `fit()` data থেকে mean ও standard deviation শেখে।
- `transform()` সেই statistics ব্যবহার করে data standardize করে।
- `fit_transform()` একই সঙ্গে fitting ও transformation করে।

### গুরুত্বপূর্ণ সতর্কতা: Data Leakage

প্রদত্ত code-এ split করার আগে পুরো `X`-এ `fit_transform()` করা হয়েছে। এটি test data-এর statistics preprocessing-এর মধ্যে ঢুকিয়ে দিতে পারে, যাকে **data leakage** বলা হয়।

সঠিক workflow হলো আগে split করা, তারপর শুধু training data-তে `fit` করা এবং training-এর শেখা scaler দিয়ে test data transform করা। নিচে সংশোধিত pattern দেওয়া হয়েছে:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

এই সংশোধিত workflow-তে test data-এর statistics scaler শেখার সময় ব্যবহার করা হয় না।

---

## 20. Train-Test Split

Code:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)
```

Dataset-কে দুই ভাগে ভাগ করা হয়:

- **Training data:** Model শেখানোর জন্য।
- **Testing data:** Training শেষে model-এর performance পরীক্ষা করার জন্য।

### `test_size=0.2`

এর অর্থ মোট data-এর 20% test data হিসেবে রাখা হবে এবং বাকি 80% training data হবে।

```text
100% Dataset
    ├── 80% Training
    └── 20% Testing
```

569টি sample-এর ক্ষেত্রে exact সংখ্যা ভাগ করার rounding-এর কারণে আনুমানিক 455টি training sample এবং 114টি test sample হয়।

### `random_state=42`

Data split-এর randomness নির্দিষ্ট করে, যাতে একই data ও একই settings ব্যবহার করলে সাধারণত একই split পাওয়া যায়। `42` বিশেষ কোনো mathematical rule নয়; অন্য integer-ও ব্যবহার করা যায়।

### গুরুত্বপূর্ণ নোট

Code-এ test set-কে `validation_data` হিসেবেও `model.fit()`-এ দেওয়া হয়েছে। শেখার সময় বারবার test-set performance দেখা হলে সেটি কার্যত validation set-এর মতো ব্যবহৃত হয়। নিরপেক্ষ final evaluation-এর জন্য আলাদা validation set এবং untouched test set রাখা উত্তম।

---

## 21. TensorFlow এবং Keras

### TensorFlow কী?

TensorFlow হলো একটি open-source framework, যা neural network-সহ Machine Learning ও Deep Learning model তৈরি এবং train করতে ব্যবহৃত হয়।

### Keras কী?

Keras হলো neural network তৈরির high-level API। এটি layer যোগ করে model তৈরি ও train করা সহজ করে।

এই Lab-এ:

```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
```

- `tf` হলো TensorFlow-এর সংক্ষিপ্ত alias।
- `Sequential` layer-গুলোকে ধারাবাহিকভাবে সাজিয়ে model তৈরি করে।
- `Dense` fully connected layer তৈরি করে।

---

## 22. Sequential Model কী?

`Sequential` model-এ layer-গুলো একটির পর একটি সাজানো হয়। একটি সাধারণ feedforward network তৈরির জন্য এটি সহজ পদ্ধতি।

Code:

```python
model = Sequential([
    Dense(32, activation='relu', input_shape=(X_train.shape[1],)),
    Dense(16, activation='relu'),
    Dense(1, activation='sigmoid')
])
```

এখানে তিনটি Dense layer আছে।

```text
Input
  ↓
Dense: 32 neurons, ReLU
  ↓
Dense: 16 neurons, ReLU
  ↓
Dense: 1 neuron, Sigmoid
  ↓
Output
```

---

## 23. Dense Layer কী?

`Dense` হলো fully connected neural-network layer। এর প্রতিটি neuron আগের layer-এর সব output-এর সঙ্গে connected থাকে।

Syntax:

```python
Dense(number_of_neurons, activation='function')
```

উদাহরণ:

```python
Dense(32, activation='relu')
```

অর্থ:

- `32` = এই layer-এ 32টি neuron।
- `activation='relu'` = ReLU activation function ব্যবহার করা হবে।

---
## 24. Input Shape

Code:

```python
input_shape=(X_train.shape[1],)
```

`X_train.shape[1]` training data-তে feature column-এর সংখ্যা দেয়।

এই dataset-এ 30টি feature আছে। তাই input shape:

```text
(30,)
```

অর্থাৎ প্রতিটি sample-এ 30টি numerical input value আছে।

শেষের comma-সহ `(30,)` Python-এর one-dimensional tuple বোঝায়।

**নোট:** `input_shape` প্রথম Dense layer-কে input-এর dimensions জানায়। আধুনিক Keras-এ চাইলে আলাদা `Input(shape=(30,))` layer দিয়েও একই বিষয় স্পষ্টভাবে লেখা যায়।

---

## 25. Hidden Layer 1 — 32 Neurons

Code:

```python
Dense(32, activation='relu', input_shape=(X_train.shape[1],))
```

এই layer-এ 32টি neuron আছে। প্রতিটি neuron input feature-এর combination থেকে pattern শিখতে পারে।

`activation='relu'` এই layer-এর output-এ ReLU function প্রয়োগ করে।

এটি hidden layer-এর প্রথম অংশ।

---

## 26. Hidden Layer 2 — 16 Neurons

Code:

```python
Dense(16, activation='relu')
```

এই layer-এ 16টি neuron আছে। এটি আগের layer-এর output থেকে আরও pattern শিখতে পারে।

এখানে আবার ReLU activation function ব্যবহার করা হয়েছে।

---

## 27. Output Layer — 1 Neuron

Code:

```python
Dense(1, activation='sigmoid')
```

এখানে একটি output neuron আছে।

কারণ task-টি **binary classification**—অর্থাৎ দুটি class-এর মধ্যে একটি নির্বাচন করতে হবে।

Sigmoid activation output-কে 0 ও 1-এর মধ্যে probability-সদৃশ মানে রূপান্তর করে।

```text
Output = 0.85
```

এটি model-এর positive class (এই dataset-এ label 1 = Benign) সম্পর্কে উচ্চ probability নির্দেশ করে। নির্দিষ্ট class নির্ধারণের জন্য threshold ব্যবহার করা হয়।

---

## 28. Activation Function কী?

Activation function neuron-এর weighted sum-কে output-এ রূপান্তর করে। এটি neural network-কে non-linear pattern শেখার ক্ষমতা দেয়।

এই Lab-এ দুটি activation function আছে:

1. ReLU
2. Sigmoid

| Function | কোথায় ব্যবহৃত | কাজ |
|---|---|---|
| ReLU | Hidden layers | Negative input-কে 0 করে; positive input অপরিবর্তিত রাখে |
| Sigmoid | Binary output layer | Output-কে 0 থেকে 1-এর মধ্যে আনে |

---
## 29. ReLU Activation Function

ReLU-এর full form **Rectified Linear Unit**।

Formula:

\[
f(x)=\max(0,x)
\]

অর্থাৎ:

```text
Input = -3 → Output = 0
Input =  0 → Output = 0
Input =  5 → Output = 5
```

Code:

```python
Dense(32, activation='relu')
Dense(16, activation='relu')
```

### ReLU কেন ব্যবহার করা হয়?

- Negative input-এর জন্য output 0 দেয়।
- Positive input-কে  রাখে।
- Deep learning-এর hidden layer-এ বহুল ব্যবহৃত।
- Non-linear relationship শেখাতে সাহায্য করে।

---

## 30. Sigmoid Activation Function

Sigmoid function-এর formula:

\[
\sigma(x)=\frac{1}{1+e^{-x}}
\]

এর output 0 থেকে 1-এর মধ্যে থাকে।

উদাহরণ:

```text
Large negative input → Output near 0
Input = 0            → Output = 0.5
Large positive input → Output near 1
```

Code:

```python
Dense(1, activation='sigmoid')
```

### Sigmoid কেন ব্যবহার করা হয়?

Binary classification-এ একটি probability-like output প্রয়োজন হতে পারে। Sigmoid output সেই কাজের উপযোগী।

এই Lab-এর threshold 0.5:

```text
Probability > 0.5 → Predicted label 1 (Benign)
Probability ≤ 0.5 → Predicted label 0 (Malignant)
```

এটি এই code-এর ব্যবহৃত decision rule। বাস্তব application-এ threshold problem-এর requirement অনুযায়ী বদলাতে পারে।

---

## 31. Model Architecture Summary

| Layer | Neurons | Activation | উদ্দেশ্য |
|---|---:|---|---|
| Input / First Dense | 32 | ReLU | 30টি feature থেকে pattern শেখা শুরু |
| Second Dense | 16 | ReLU | Learned representation আরও process করা |
| Output Dense | 1 | Sigmoid | Binary class-এর probability দেওয়া |

Model-এর সংক্ষিপ্ত structure:

```text
30 Input Features
       ↓
32 Neurons + ReLU
       ↓
16 Neurons + ReLU
       ↓
1 Neuron + Sigmoid
       ↓
Probability
```

---
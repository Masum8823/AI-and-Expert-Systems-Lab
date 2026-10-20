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

## 32. Model Compile করা

Code:

```python
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)
```

`compile()` training শুরু করার আগে model-এর training configuration নির্ধারণ করে।

এখানে তিনটি বিষয় নির্ধারণ করা হয়েছে:

- Optimizer
- Loss function
- Evaluation metric

---

## 33. Optimizer কী?

Optimizer training-এর সময় model-এর weights ও biases কীভাবে update হবে তা নির্ধারণ করে।

এই Lab-এ:

```python
optimizer='adam'
```

ব্যবহার করা হয়েছে।

### Adam-এর ধারণা

Adam-এর full form **Adaptive Moment Estimation**।

এটি gradient-এর information ব্যবহার করে weights update করে এবং deep learning-এ বহুল ব্যবহৃত optimizer।

সহজভাবে:

```text
Prediction
   ↓
Calculate Loss
   ↓
Calculate Gradients
   ↓
Adam Updates Weights
   ↓
Better Prediction-এর চেষ্টা
```

Adam ব্যবহার করলেই সব dataset-এ সর্বোত্তম result নিশ্চিত হয় না; এটি একটি সাধারণ ও কার্যকর starting choice।

---
## 34. Loss Function কী?

Loss function model-এর prediction actual label থেকে কতটা আলাদা, তা measure করে।

Training-এর সময় model loss কমানোর চেষ্টা করে।

এই Lab-এ:

```python
loss='binary_crossentropy'
```

ব্যবহার করা হয়েছে।

Binary Cross-Entropy binary classification-এর জন্য বহুল ব্যবহৃত loss function।

Formula:

\[
L=-\left[y\log(p)+(1-y)\log(1-p)\right]
\]

যেখানে:

- \(y\) = actual label (0 অথবা 1)
- \(p\) = model-এর predicted probability

সহজভাবে, model সঠিক class-কে বেশি probability দিলে loss সাধারণত কম হয়; ভুল class-কে অত্যন্ত বেশি probability দিলে loss বেশি হয়।

---

## 35. Accuracy Metric

Code:

```python
metrics=['accuracy']
```

Accuracy দিয়ে মোট sample-এর মধ্যে কতগুলো sample সঠিক class হিসেবে predict হয়েছে তা দেখা হয়।

Formula:

\[
Accuracy=\frac{\text{Correct Predictions}}{\text{Total Predictions}}
\]

উদাহরণ:

```text
100টি sample-এর মধ্যে 95টি সঠিক
Accuracy = 95 / 100 = 95%
```

`accuracy` training ও validation-এর performance monitor করতে সাহায্য করে। তবে শুধু accuracy দেখে model-এর সব দিক বোঝা যায় না; classification report এবং confusion matrix-ও দেখা উচিত।

---

## 36. `model.summary()`

Code:

```python
model.summary()
```

এটি model-এর architecture-এর summary দেখায়।

সাধারণত দেখা যায়:

- Layer-এর নাম
- Output shape
- Trainable parameters
- Non-trainable parameters
- মোট parameter-এর সংখ্যা

### Parameter কী?

Dense layer-এর trainable parameters হলো weights ও biases, যেগুলো training-এর সময় update হতে পারে।

এই architecture-এ parameter count:

- First Dense: \(30 \times 32 + 32 = 992\)
- Second Dense: \(32 \times 16 + 16 = 528\)
- Output Dense: \(16 \times 1 + 1 = 17\)

মোট:

\[
992+528+17=1537
\]

অর্থাৎ এই architecture-এ **1,537টি trainable parameter** আছে।

---
## 37. Model Training — `model.fit()`

Code:

```python
history = model.fit(
    X_train,
    y_train,
    epochs=30,
    validation_data=(X_test, y_test),
    verbose=1
)
```

`fit()` method training data ব্যবহার করে model-কে train করে।

### প্রতিটি argument-এর কাজ

| Argument | কাজ |
|---|---|
| `X_train` | Training input features |
| `y_train` | Training-এর actual labels |
| `epochs=30` | Training data-এর উপর সর্বোচ্চ 30টি training cycle |
| `validation_data` | প্রতিটি epoch শেষে validation performance হিসাব |
| `verbose=1` | Training progress দেখানো |
| `history` | প্রতিটি epoch-এর recorded metrics সংরক্ষণ |

### গুরুত্বপূর্ণ সতর্কতা

এই code-এ `X_test, y_test` validation data হিসেবে ব্যবহার করা হয়েছে। তাই এটি সম্পূর্ণ untouched final test set নয়। আরও নির্ভরযোগ্য evaluation-এর জন্য training, validation ও final test—তিনটি আলাদা অংশ রাখা ভালো।

---
## 38. Epoch কী?

একটি epoch হলো model-এর training dataset-এর সব sample-এর উপর একবার training সম্পন্ন হওয়া।

Code:

```python
epochs=30
```

অর্থাৎ model training data-এর উপর সর্বোচ্চ 30টি epoch চালাবে।

সহজভাবে:

```text
Epoch 1 → Training data একবার ব্যবহার
Epoch 2 → Training data দ্বিতীয়বার ব্যবহার
...
Epoch 30 → Training data ত্রিশতমবার ব্যবহার
```

Epoch বেশি হলেই model সবসময় ভালো হবে—এমন নয়। খুব বেশি epoch হলে overfitting হতে পারে।

---
## 39. Batch কী?

Training-এর সময় সব sample একসঙ্গে process না করে ছোট ছোট group-এ process করা যেতে পারে। প্রতিটি group-কে batch বলা হয়।

Keras-এর default batch size নির্দিষ্ট না করলে সাধারণত 32 ব্যবহৃত হয়। তাই এই code-এ batch size আলাদা করে দেওয়া হয়নি বলে Keras default ব্যবহার করবে।

উদাহরণ:

```text
Training Samples
      ↓
Batch 1
      ↓
Batch 2
      ↓
Batch 3
```

একটি epoch-এ একাধিক batch process হতে পারে।

---

## 40. `history` Object

Code:

```python
history = model.fit(...)
```

`history` object training চলাকালীন প্রতিটি epoch-এর metrics সংরক্ষণ করে।

এই Lab-এ ব্যবহার করা হয়েছে:

```python
history.history['accuracy']
history.history['val_accuracy']
```

- `accuracy` = প্রতিটি epoch-এর training accuracy
- `val_accuracy` = প্রতিটি epoch-এর validation accuracy

এই values দিয়ে training performance-এর graph তৈরি করা হয়।

---

## 41. Training ও Validation Accuracy Graph

Code:

```python
plt.plot(history.history['accuracy'], label='Train Accuracy')
plt.plot(history.history['val_accuracy'], label='Val Accuracy')
plt.xlabel("Epochs")
plt.ylabel("Accuracy")
plt.legend()
plt.title("Training and Validation Accuracy")
plt.show()
```

### Graph-এর অংশ

- X-axis: Epochs
- Y-axis: Accuracy
- `Train Accuracy`: Training data-তে accuracy
- `Val Accuracy`: Validation data-তে accuracy
- `legend()`: কোন line কোনটি তা দেখায়
- `title()`: Graph-এর title নির্ধারণ করে

### Graph কীভাবে বুঝবে?

**Case 1: দুই accuracy বাড়ছে এবং কাছাকাছি আছে**

Model শেখার উন্নতি হতে পারে এবং generalization মোটামুটি ভালো হতে পারে।

**Case 2: Training accuracy বাড়ছে, validation accuracy কমছে বা পিছিয়ে যাচ্ছে**

এটি overfitting-এর সম্ভাব্য indication।

**Case 3: দুই accuracy-ই কম**

Model যথেষ্ট pattern শিখতে পারছে না—underfitting বা অন্য training সমস্যা হতে পারে।

**মনে রাখবে:** Graph দেখে ধারণা পাওয়া যায়; final conclusion-এর জন্য loss, data quality এবং আলাদা test performance-ও বিবেচনা করতে হয়।

---
## 42. Prediction কী?

Training শেষে model নতুন input-এর class predict করতে পারে।

Code:

```python
y_pred_prob = model.predict(X_test)
```

এই line test data-এর প্রতিটি sample-এর জন্য output probability তৈরি করে।

যেহেতু output layer-এ একটি Sigmoid neuron আছে, প্রতিটি sample-এর জন্য একটি probability-like value পাওয়া যায়।

উদাহরণ:

```text
Sample 1 → 0.92
Sample 2 → 0.18
Sample 3 → 0.67
```

এগুলো সরাসরি class label নয়; এগুলো threshold দিয়ে class-এ রূপান্তর করা হবে।

---

## 43. Probability থেকে Class Label

Code:

```python
y_pred = (y_pred_prob > 0.5).astype("int32")
```

ব্যাখ্যা:

1. `y_pred_prob > 0.5` প্রতিটি probability 0.5-এর চেয়ে বড় কি না পরীক্ষা করে।
2. শর্ত সত্য হলে `True`, অন্যথায় `False` তৈরি হয়।
3. `.astype("int32")` Boolean result-কে integer label-এ রূপান্তর করে:
   - `True` → 1
   - `False` → 0

এখানে `>` ব্যবহার করা হয়েছে, `>=` নয়। তাই probability ঠিক 0.5 হলে label 0 হবে।

এই dataset-এ:

```text
Predicted 0 → Malignant
Predicted 1 → Benign
```

---

## 44. `predict()` বনাম Predicted Probability

| বিষয় | `model.predict()` |
|---|---|
| এই Lab-এ output | Sigmoid output probability |
| Output shape | সাধারণত `(number_of_samples, 1)` |
| Final class | Threshold দিয়ে নির্ধারণ করা হয় |
| Example | 0.82 → threshold 0.5 অনুযায়ী class 1 |

এখানে একটি গুরুত্বপূর্ণ পার্থক্য আছে: Keras model-এর `predict()` এই architecture-এ সরাসরি probability দেয়। Scikit-learn-এর অনেক classifier-এর `predict()` সাধারণত class label দেয়, আর `predict_proba()` probability দেয়।

---

## 45. Classification Report

Code:

```python
print(
    "Classification Report:\n",
    classification_report(y_test, y_pred)
)
```

`classification_report()` classification model-এর evaluation metrics দেখায়।

সাধারণত এতে থাকে:

- Precision
- Recall
- F1-score
- Support

### Precision

Model যে sample-গুলোকে একটি class হিসেবে predict করেছে, সেগুলোর মধ্যে কতগুলো সত্যিই সেই class—তা measure করে।

### Recall

Actual কোনো class-এর sample-এর মধ্যে কতগুলো model সঠিকভাবে identify করেছে, তা measure করে।

### F1-score

Precision ও Recall-এর harmonic mean।

\[
F1=\frac{2PR}{P+R}
\]

যেখানে \(P\) = Precision এবং \(R\) = Recall।

### Support

Test data-তে প্রতিটি class-এর actual sample সংখ্যা।

**গুরুত্বপূর্ণ:** Classification report-এ class 0 ও class 1-এর label এই dataset-এর mapping অনুযায়ী পড়তে হবে।

---

## 46. Confusion Matrix

Code:

```python
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
```

Confusion matrix actual class এবং predicted class-এর count দেখায়।

Binary classification-এ scikit-learn-এর default label order `[0, 1]` হলে matrix-এর layout:

```text
                  Predicted
                 0       1
Actual 0        TN      FP
Actual 1        FN      TP
```

এখানে row হলো actual label এবং column হলো predicted label।

| Term | অর্থ |
|---|---|
| TN — True Negative | Actual 0, predicted 0 |
| FP — False Positive | Actual 0, predicted 1 |
| FN — False Negative | Actual 1, predicted 0 |
| TP — True Positive | Actual 1, predicted 1 |

এই Lab-এ class 0 হলো Malignant এবং class 1 হলো Benign। তাই confusion matrix পড়ার সময় positive/negative শব্দের পাশাপাশি actual class mapping-ও খেয়াল রাখতে হবে।

---
## 47. Single Test Sample নির্বাচন

Code:

```python
sample_index = 0
single_input = X_test[sample_index].reshape(1, -1)
```

ব্যাখ্যা:

- `sample_index = 0` test set-এর প্রথম sample নির্বাচন করে।
- `X_test[sample_index]` ওই sample-এর feature values বের করে।
- `.reshape(1, -1)` input-কে একটি row-যুক্ত 2D array-তে রূপান্তর করে।

Model সাধারণত input-এর shape চায়:

```text
(number_of_samples, number_of_features)
```

একটি sample ও 30টি feature-এর জন্য shape হবে:

```text
(1, 30)
```

---

## 48. Single Sample Prediction

Code:

```python
pred_prob = model.predict(single_input)[0][0]
pred_label = int(pred_prob > 0.5)
true_label = y_test.iloc[sample_index]
```

### `model.predict(single_input)`

একটি sample-এর probability তৈরি করে।

### `[0][0]`

প্রথম sample-এর প্রথম output neuron-এর value নেয়।

### `pred_label`

Probability 0.5-এর বেশি হলে 1, অন্যথায় 0 নির্ধারণ করে।

### `y_test.iloc[sample_index]`

নির্বাচিত sample-এর actual label নেয়। `.iloc[]` position অনুযায়ী Series থেকে value নির্বাচন করে।

---
## 49. Prediction Result Print করা

Code:

```python
print(f"\nSample {sample_index}:")
print(f"Predicted Probability: {pred_prob:.4f}")
print(
    f"Predicted Label: {pred_label} "
    f"({'Benign' if pred_label == 1 else 'Malignant'})"
)
print(
    f"True Label: {true_label} "
    f"({'Benign' if true_label == 1 else 'Malignant'})"
)
```

এখানে f-string ব্যবহার করে text-এর সঙ্গে variable-এর value দেখানো হয়েছে।

- `{pred_prob:.4f}` probability-কে decimal-এর পরে 4 ঘর পর্যন্ত দেখায়।
- `pred_label == 1` হলে `Benign` দেখায়।
- অন্যথায় `Malignant` দেখায়।
- `true_label` দিয়ে actual class দেখানো হয়।

উদাহরণ output-এর format:

```text
Sample 0:
Predicted Probability: 0.9234
Predicted Label: 1 (Benign)
True Label: 1 (Benign)
```

এটি শুধু format বোঝানোর example; actual output training-এর result অনুযায়ী আলাদা হতে পারে।

---

## 50. সম্পূর্ণ ANN Workflow

```text
Load Breast Cancer Dataset
          ↓
Create X and y
          ↓
Create DataFrame
          ↓
EDA and Visualization
          ↓
Feature Scaling
          ↓
Train-Test Split
          ↓
Build Sequential ANN
          ↓
Compile Model
          ↓
Train with model.fit()
          ↓
Plot Train / Validation Accuracy
          ↓
Predict Test Samples
          ↓
Convert Probability to Class
          ↓
Classification Report
          ↓
Confusion Matrix
          ↓
Predict One Sample
```

**Workflow-এর গুরুত্বপূর্ণ correction:** বাস্তব evaluation-এ আগে train/validation/test split করা, তারপর training data দিয়ে scaler fit করা উত্তম। Final test set-কে model selection-এর সময় বারবার ব্যবহার করা উচিত নয়।

---

# Part 2: Convolutional Neural Network (CNN)

## 51. CNN কী?

CNN-এর full form **Convolutional Neural Network**।

CNN হলো Deep Learning model-এর একটি ধরন, যা বিশেষ করে image-এর মতো grid-structured data থেকে features শেখার জন্য কার্যকর।

CNN image-এর ছোট ছোট অংশ পরীক্ষা করে edge, texture, shape এবং আরও জটিল visual pattern শিখতে পারে।

ব্যবহারের উদাহরণ:

- Handwritten digit recognition
- Image classification
- Face recognition
- Object detection
- Medical image analysis

---

## 52. ANN এবং CNN-এর পার্থক্য

| ANN / সাধারণ Dense Network | CNN |
|---|---|
| Dense layer-এ input-এর সব feature সংযুক্ত থাকে | Convolution filter দিয়ে local patterns শেখে |
| Tabular data-তে কার্যকর হতে পারে | Image data-তে বিশেষভাবে কার্যকর |
| Flattened image দিলে spatial structure সহজে হারিয়ে যেতে পারে | Image-এর spatial relationship কাজে লাগাতে পারে |
| সাধারণত Dense layer-নির্ভর architecture হতে পারে | Convolution ও pooling layer ব্যবহার করে |

ANN এবং CNN সম্পূর্ণ আলাদা জগৎ নয়। CNN-এর architecture-এও Dense layer থাকতে পারে।

---

## 53. CNN-এর Basic Architecture

একটি সাধারণ image classification CNN-এর flow:

```text
Input Image
    ↓
Convolution Layer
    ↓
Activation Function (ReLU)
    ↓
Pooling Layer
    ↓
More Convolution / Pooling Layers
    ↓
Flatten or Global Pooling
    ↓
Dense Layer
    ↓
Output Layer
    ↓
Predicted Class
```

Architecture dataset ও task অনুযায়ী পরিবর্তিত হতে পারে।

---
## 54. Convolution Layer

Convolution layer image-এর উপর ছোট filter বা kernel প্রয়োগ করে feature map তৈরি করে।

প্রাথমিক layer শিখতে পারে:

- Edge
- Line
- Simple texture

পরের layer শিখতে পারে:

- Shape
- Object-এর অংশ
- আরও জটিল visual pattern

সহজভাবে:

```text
Input Image
    ↓
Small Filter / Kernel
    ↓
Feature Map
```

CNN filter-এর values training-এর সময় শেখে।

---

## 55. Filter / Kernel কী?

Filter বা kernel হলো ছোট matrix, যা image-এর বিভিন্ন local region-এর উপর slide করে calculation করে।

উদাহরণ হিসেবে 3×3 kernel:

```text
[ 1  0 -1 ]
[ 1  0 -1 ]
[ 1  0 -1 ]
```

এটি শুধু বোঝানোর example; বাস্তব CNN-এ filter-এর weights training-এর মাধ্যমে শেখা হয়।

Filter image-এর pattern detect করতে সাহায্য করে। একটি convolution layer-এ একাধিক filter থাকতে পারে, ফলে একাধিক feature map তৈরি হয়।

---
## 56. Feature Map কী?

Convolution operation-এর output-কে feature map বলা হয়।

Feature map দেখায় image-এর কোন অঞ্চলে কোনো learned feature-এর response বেশি হয়েছে।

```text
Image + Learned Filter
          ↓
      Feature Map
```

CNN-এর পরবর্তী layer-গুলো এই feature map ব্যবহার করে আরও জটিল pattern শেখে।

---
## 57. Padding এবং Stride

### Padding

Convolution-এর আগে image-এর border-এর চারপাশে অতিরিক্ত value—সাধারণত zero—যোগ করাকে padding বলে।

- `valid`: সাধারণত padding ছাড়া convolution।
- `same`: উপযুক্ত padding ব্যবহার করে stride 1-এর ক্ষেত্রে spatial size সাধারণত একই রাখে।

### Stride

Filter প্রতিবার কত ঘর করে এগোবে, তা stride নির্ধারণ করে।

- Stride 1: এক ঘর করে এগোয়।
- Stride 2: দুই ঘর করে এগোয়; output spatial size সাধারণত আরও ছোট হয়।

Padding ও stride output feature map-এর dimensions-এ প্রভাব ফেলে।

---
## 58. Pooling Layer

Pooling layer feature map-এর spatial dimensions ছোট করে। এতে computation কমতে পারে এবং গুরুত্বপূর্ণ feature সংক্ষিপ্তভাবে ধরে রাখা যায়।

দুটি পরিচিত ধরন:

- **Max Pooling:** একটি window-এর সর্বোচ্চ value নেয়।
- **Average Pooling:** একটি window-এর average নেয়।

উদাহরণ:

```text
Feature Map
    ↓
Max Pooling
    ↓
Smaller Feature Map
```

Pooling layer সাধারণত trainable weights ব্যবহার করে না।

---
## 59. Flatten Layer

Convolution ও pooling-এর পরে feature maps-কে Dense layer-এ পাঠাতে একমাত্রিক vector-এ রূপান্তর করা যেতে পারে। এই কাজের জন্য `Flatten` layer ব্যবহার করা হয়।

```text
2D / 3D Feature Maps
          ↓
        Flatten
          ↓
      1D Vector
          ↓
      Dense Layer
```

Flatten নিজে feature শেখে না; এটি data-এর shape পরিবর্তন করে।

কিছু CNN architecture-এ Flatten-এর বদলে Global Average Pooling-ও ব্যবহার করা হয়।

---

## 60. CNN-এ Dense এবং Output Layer

CNN-এর শেষের দিকে Dense layer ব্যবহার করে learned features-এর ভিত্তিতে class prediction করা হতে পারে।

Binary classification-এ একটি সাধারণ option:

```python
Dense(1, activation='sigmoid')
```

Multi-class classification-এ একটি সাধারণ option:

```python
Dense(number_of_classes, activation='softmax')
```

তবে output layer ও loss function নির্বাচন নির্ভর করে task-এর ধরন এবং label format-এর উপর।

---
## 61. MNIST এবং CIFAR-10

Learning Objectives-এ MNIST ও CIFAR-10-এর মতো image dataset-এর কথা বলা হয়েছে।

### MNIST

- Handwritten digit-এর grayscale image।
- Image size: 28×28 pixels।
- সাধারণত 10টি class: digit 0 থেকে 9।
- Beginner CNN practice-এর জন্য বহুল ব্যবহৃত।
### CIFAR-10

- ছোট color image dataset।
- Image size: 32×32 pixels, 3 color channels।
- 10টি object category।
- MNIST-এর তুলনায় image pattern আরও জটিল।

### তুলনা

| বিষয় | MNIST | CIFAR-10 |
|---|---|---|
| Image type | Grayscale | RGB color |
| Image size | 28×28 | 32×32 |
| Class সংখ্যা | 10 | 10 |
| Example | Handwritten digits | Animals ও vehicles-এর মতো object |

---

## 62. CNN কেন Image Classification-এ উপযোগী?

CNN-এর গুরুত্বপূর্ণ সুবিধা:

- Image-এর local spatial pattern শেখে।
- একই filter image-এর বিভিন্ন জায়গায় ব্যবহার করতে পারে।
- Edge থেকে শুরু করে complex visual feature শেখার সুযোগ দেয়।
- সাধারণ Dense network-এর তুলনায় image structure বেশি কার্যকরভাবে ব্যবহার করতে পারে।

তবে ভালো performance পেতে পর্যাপ্ত data, উপযুক্ত architecture, preprocessing এবং training গুরুত্বপূর্ণ।

---
## 63. Lab Code-এ CNN Implement করা হয়েছে কি?

না। প্রদত্ত code-এ:

```python
from tensorflow.keras.layers import Dense
```

ব্যবহার করা হয়েছে এবং model-এ শুধু Dense layer যোগ করা হয়েছে।

এখানে `Conv2D`, `MaxPooling2D` বা CNN-এর অন্য convolution layer নেই। তাই এই practical code-টি ANN implementation; CNN হলো learning objective-এর পরবর্তী ধারণাগত অংশ।

একটি সাধারণ CNN-এ layer import-এর উদাহরণ:

```python
from tensorflow.keras.layers import (
    Conv2D,
    MaxPooling2D,
    Flatten,
    Dense
)
```

এই import pattern CNN তৈরির জন্য প্রয়োজন হতে পারে, কিন্তু শুধু import করলেই CNN তৈরি হয় না—model-এ convolution ও সংশ্লিষ্ট layer ব্যবহার করে architecture বানাতে হবে।

---
# Part 3: Important Differences and Revision

## 64. ANN বনাম CNN — Quick Table

| বিষয় | ANN | CNN |
|---|---|---|
| Full form | Artificial Neural Network | Convolutional Neural Network |
| Basic component | Neurons ও Dense layers | Convolution filters, feature maps, pooling; Dense layers-ও থাকতে পারে |
| Common data | Tabular বা general numerical data | Image ও spatial data |
| Feature learning | Dense connections-এর মাধ্যমে | Local convolution filters-এর মাধ্যমে |
| Example | Breast cancer tabular classification | MNIST digit image classification |

---
## 65. Important Python Code Patterns

### Dataset load

```python
data = load_breast_cancer()
```

### Features ও target

```python
X = pd.DataFrame(data.data, columns=data.feature_names)
y = pd.Series(data.target, name='target')
```

### DataFrame-এ target যোগ করা

```python
df = X.copy()
df['target'] = y
```

### Scaling

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

শিক্ষামূলক code-এ এটি দেখানো হয়েছে। বাস্তব workflow-তে আগে split করে training data-তে scaler fit করবে।

### Train-test split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)
```
### ANN model

```python
model = Sequential([
    Dense(32, activation='relu', input_shape=(X_train.shape[1],)),
    Dense(16, activation='relu'),
    Dense(1, activation='sigmoid')
])
```

### Compile

```python
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)
```

### Train

```python
history = model.fit(
    X_train,
    y_train,
    epochs=30,
    validation_data=(X_test, y_test),
    verbose=1
)
```
### Predict probability

```python
y_pred_prob = model.predict(X_test)
```

### Probability থেকে class

```python
y_pred = (y_pred_prob > 0.5).astype("int32")
```

### Evaluation

```python
print(classification_report(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))
```

---

## 66. Important Terms — এক নজরে

| Term | সহজ অর্থ |
|---|---|
| ANN | Neuron-অনুপ্রাণিত learning model |
| Neuron | Input process করে output তৈরি করে |
| Weight | Input-এর প্রভাব নির্ধারণে সাহায্য করে |
| Bias | Weighted sum adjust করে |
| Input Layer | Input feature গ্রহণ করে |
| Hidden Layer | Data থেকে pattern শেখে |
| Output Layer | Final output দেয় |
| Dense Layer | Fully connected layer |
| Activation Function | Neuron-এর output transform করে |
| ReLU | Negative value-কে 0 করে |
| Sigmoid | Output 0–1-এর মধ্যে আনে |
| Loss Function | Prediction error measure করে |
| Optimizer | Weights update করে |
| Epoch | Training data-এর উপর একবার training pass |
| Batch | Training sample-এর ছোট group |
| StandardScaler | Feature standardize করে |
| Overfitting | Training ভালো, unseen data-তে performance খারাপ হতে পারে |
| CNN | Convolution ব্যবহার করে feature শেখে |
| Kernel / Filter | Local pattern detect করার learned matrix |
| Feature Map | Convolution-এর output |
| Pooling | Spatial dimensions কমায় |
| Flatten | Feature maps-কে vector-এ রূপান্তর করে |

---

## 67. Important Formulas — One Place

### Artificial Neuron

\[
z=\sum_{i=1}^{n} w_i x_i+b
\]

\[
a=f(z)
\]

### ReLU

\[
f(x)=\max(0,x)
\]

### Sigmoid

\[
\sigma(x)=\frac{1}{1+e^{-x}}
\]

### Standardization

\[
z=\frac{x-\mu}{\sigma}
\]

### Binary Cross-Entropy

\[
L=-[y\log(p)+(1-y)\log(1-p)]
\]

### Accuracy

\[
Accuracy=\frac{\text{Correct Predictions}}{\text{Total Predictions}}
\]

### F1-score

\[
F1=\frac{2PR}{P+R}
\]

যেখানে \(P\) হলো Precision এবং \(R\) হলো Recall।

---
## 68. Important Exam Questions and Answers

### Q1. What is an Artificial Neural Network (ANN)?

ANN হলো একটি Machine Learning model, যা biological neuron-এর ধারণা থেকে অনুপ্রাণিত। এটি input data থেকে pattern শিখে classification বা regression-এর মতো কাজ করে।

### Q2. What is a Feedforward Neural Network?

Feedforward Neural Network হলো এমন neural network যেখানে information input layer থেকে hidden layer হয়ে output layer-এর দিকে প্রবাহিত হয়।

### Q3. What is a neuron?

Neuron হলো neural network-এর একটি computational unit, যা input, weights ও bias ব্যবহার করে calculation করে এবং activation function-এর মাধ্যমে output তৈরি করে।

### Q4. What are weights and biases?

Weights input-এর প্রভাব নিয়ন্ত্রণে সাহায্য করে, আর bias weighted sum-কে adjust করে। Training-এর সময় দুটিই update হতে পারে।

### Q5. What is a Dense layer?

Dense layer হলো fully connected layer, যেখানে প্রতিটি neuron আগের layer-এর সব output-এর সঙ্গে connected থাকে।

### Q6. What is an activation function?

Activation function neuron-এর calculated value-কে transform করে। এটি neural network-কে non-linear pattern শেখার ক্ষমতা দেয়।

### Q7. Why is ReLU used in hidden layers?

ReLU negative input-এর জন্য 0 এবং positive input-এর জন্য input value দেয়। এটি hidden layer-এ বহুল ব্যবহৃত এবং non-linear pattern শেখায় সাহায্য করে।

### Q8. Why is Sigmoid used in the output layer?

Binary classification-এ Sigmoid output-কে 0 থেকে 1-এর মধ্যে আনে, যা probability হিসেবে ব্যাখ্যা করা যায়।

### Q9. What is Binary Cross-Entropy?

Binary Cross-Entropy হলো binary classification-এর loss function, যা actual label এবং predicted probability-এর পার্থক্য measure করে।

### Q10. What is an optimizer? Why is Adam used?

Optimizer training-এর সময় weights ও biases update করে। Adam gradient-based update ব্যবহার করে এবং neural network training-এর একটি বহুল ব্যবহৃত optimizer।
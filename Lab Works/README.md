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

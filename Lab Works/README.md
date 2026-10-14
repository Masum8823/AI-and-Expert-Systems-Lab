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
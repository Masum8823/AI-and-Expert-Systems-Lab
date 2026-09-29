# Artificial Intelligence Lab — Zero to Basic Bangla Notes

> **Purpose:** এই README এমনভাবে লেখা হয়েছে যেন AI/ML সম্পর্কে আমার basic একদম zero হলেও এখান থেকে ধীরে ধীরে বুঝতে পারি এবং Lab-এর code নিজে লিখতে পারি।

---

# 1. Artificial Intelligence (AI) কী?

সহজ ভাষায়,

**AI = Computer/Machine-কে এমনভাবে তৈরি করা যাতে সে মানুষের মতো কিছু intelligent কাজ করতে পারে।**

যেমন:

* মানুষের কথা বুঝতে পারা
* ছবি চিনতে পারা
* সিদ্ধান্ত নেওয়া
* Prediction করা
* Problem solve করা
* কোনো data দেখে pattern খুঁজে বের করা

### Example

ধরো, আমরা computer-কে অনেক student's data দিলাম:

| Study Hours | Attendance | Result    |
| ----------: | ---------: | --------- |
|           2 |        60% | Fail      |
|           4 |        75% | Pass      |
|           6 |        85% | Pass      |
|           8 |        95% | Excellent |

Computer এই data দেখে pattern শিখতে পারে।

তারপর নতুন একজন student-এর:

```text
Study Hours = 5
Attendance = 80%
```

দিলে computer অনুমান করতে পারে:

```text
Result = Pass
```

এটাই AI-এর একটি simple example।

Source অনুযায়ী AI হলো এমন machine তৈরি করার field যা human intelligence-এর প্রয়োজন হয় এমন কাজ করতে পারে।

---

# 2. AI, ML, Neural Network এবং Deep Learning

এই চারটা বিষয় প্রথমে confusing লাগবে।

সবচেয়ে সহজভাবে hierarchy:

```text
AI
└── ML
    └── Neural Network
        └── Deep Learning
```

অর্থাৎ:

**AI → ML → Neural Network → Deep Learning**

---

## 2.1 AI

AI হলো সবচেয়ে বড় field।

এর মধ্যে এমন সব technique থাকে যার মাধ্যমে computer intelligent কাজ করতে পারে।

Example:

```text
AI
├── Machine Learning
├── Neural Networks
├── Expert Systems
├── Natural Language Processing
└── Computer Vision
```

---

# 3. Machine Learning (ML)

**Machine Learning হলো AI-এর একটি অংশ।**

এখানে computer-কে প্রতিটি rule manually লিখে দিতে হয় না।

বরং তাকে **data দেওয়া হয়**, এবং data থেকে সে pattern শেখে।

### Traditional Programming

আমরা যদি বলি:

```text
যদি marks >= 40
    তাহলে Pass
নাহলে
    Fail
```

এখানে rule আমরা নিজেরাই লিখেছি।

### Machine Learning

ML-এ আমরা অনেক example data দেব:

```text
Marks     Result
30        Fail
35        Fail
45        Pass
60        Pass
80        Pass
```

Machine এই data থেকে pattern শেখার চেষ্টা করবে।

তারপর নতুন marks দিলে prediction করবে।

---

# 4. Neural Network কী?

Neural Network হলো ML-এর একটি technique।

এটি মানুষের brain-এর neuron-এর idea থেকে inspired।

সহজভাবে:

```text
Input
  ↓
Neuron Layer
  ↓
Neuron Layer
  ↓
Output
```

যেমন student result prediction:

```text
Study Hours ─────┐
                 ├──> Neural Network ──> Result
Attendance ──────┤
                 │
Previous Marks ──┘
```

Neural Network input data নিয়ে বিভিন্ন layer-এর মাধ্যমে process করে output দেয়।

---

# 5. Deep Learning (DL)

Deep Learning হলো Neural Network-এর একটি advanced form যেখানে **অনেকগুলো hidden layer** থাকে।

```text
Input
 ↓
Hidden Layer
 ↓
Hidden Layer
 ↓
Hidden Layer
 ↓
Output
```

অনেক layer থাকার কারণে একে **Deep Learning** বলা হয়।

Deep Learning complex কাজের ক্ষেত্রে খুব useful, যেমন:

* Image Recognition
* Speech Recognition
* Natural Language Processing

Source-এও DL-কে multiple hidden layers-যুক্ত neural network হিসেবে ব্যাখ্যা করা হয়েছে।

---

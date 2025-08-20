# Predicting Student Performance with Machine Learning

This project applies various machine learning techniques to predict whether a student will correctly answer diagnostic questions. It was completed as part of the final project for **CSC311 - Introduction to Machine Learning** at the University of Toronto.

Team: Aryamann Rao, Paridhi Goel  
Date: March 2023

---

## 📚 Project Overview

We used data from Eedi, an online learning platform, to train models that can predict student answers to diagnostic questions. These predictions help assess student ability and inform personalized education strategies.

The project consisted of two parts:

- **Part A**: Implementing baseline ML models (kNN, IRT, Neural Networks) and an ensemble method.
- **Part B**: Extending the neural network model by adding layers and incorporating student metadata.

---

## 🧪 Dataset

- **Students**: 542
- **Questions**: 1774
- **Format**: Sparse matrix (NaNs for unanswered questions)

Metadata included:
- Student age, gender, economic status
- Question subject and ID

---

## 🧩 Models Implemented

### 🔹 k-Nearest Neighbours (kNN)

- **User-based CF**: Accuracy peaked at 68.4% with `k=11`.
- **Item-based CF**: Accuracy peaked at 68.2% with `k=21`.
- **Limitations**:
  - Ignores individual topic mastery.
  - Poor scalability.
  - Assumes similarity transfers across topics.

### 🔹 Item Response Theory (IRT)

- Probabilistic model: \( P(c_{ij} = 1 | \theta_i, \beta_j) = \sigma(\theta_i - \beta_j) \)
- **Accuracy**:
  - Validation: 70.69%
  - Test: 70.17%
- **Analysis**:
  - Plotted sigmoid probability curves for questions with varying difficulty.

### 🔹 Autoencoder Neural Network

- **Base Model**:
  - Latent dimension \(k=50\)
  - Validation accuracy: 66.6%
- **With Regularization**:
  - Best \( \lambda = 0.01 \)
  - Accuracy improved to 66.9%
- **Hyperparameters**:
  - Learning rate = 0.1
  - Epochs = 10

### 🔹 Ensemble (Bagging)

- Used 3 bootstrapped neural networks.
- Averaged predictions for final output.
- **Performance**:
  - Validation Accuracy: 67.1%
  - Test Accuracy: 67.2%

---

## 🚀 Part B: Extending the Neural Network

### 🔧 Extension 1: Additional Layers

- Added two hidden layers with intermediate sizes \(k_1 = 50\), \(k_2 = 2\)
- Improved learning and late-epoch accuracy

### 🧬 Extension 2: Student Metadata

- Appended age, gender, and economic status to the input vector
- Resulted in reduced accuracy due to:
  - Unnormalized values (e.g., gender = 2)
  - Sigmoid activation outputs limited to [0, 1]

---

## 📊 Results

| Model                      | Validation Accuracy | Test Accuracy |
|---------------------------|---------------------|---------------|
| kNN (User)                | 68.9%               | 68.4%         |
| kNN (Item)                | 69.2%               | 68.2%         |
| IRT                       | 70.69%              | 70.17%        |
| Neural Net (Base)         | ~66.6%              | 66.6%         |
| Neural Net + Regularizer  | ~67.0%              | 66.9%         |
| Ensemble                  | 67.1%               | 67.2%         |
| Extension 1 (Deep NN)     | ↑ over base         | Not reported  |
| Extension 2 (Metadata)    | ↓ from Extension 1  | Not reported  |

---

## ⚠️ Limitations

- Sigmoid activations restrict range of output — problematic for non-binary features.
- Student metadata caused decreased accuracy due to poor scaling.
- Limited training data (524 students, 1774 questions)
- Weight initialization randomness caused minor accuracy variation per run

---

## 👥 Contributions

- **Aryamann Rao**: Implemented kNN, Neural Networks (Part A)
- **Paridhi Goel**: Implemented Ensemble Model (Part A)
- **Both**: Collaborated on Item Response Theory and Part B model design

---

## 📌 Acknowledgments

- [Eedi](https://eedi.com/) for providing real-world student diagnostic data
- CSC311 Course Staff for project guidance and support

---

## 🧠 Future Work

- Normalize metadata features (e.g., scale age/gender)
- Explore different activations (e.g., ReLU)
- Increase dataset size
- Use more sophisticated ensembling techniques

---

## 📜 License

This project is part of a university course submission and is intended for educational purposes only.

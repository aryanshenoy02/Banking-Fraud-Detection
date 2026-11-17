# Banking Fraud Detection – Transaction Anomaly Detection

An unsupervised machine learning project that analyses personal banking transactions to identify unusual financial activities based on historical transaction behaviour.

The project explores how anomaly detection techniques can be applied to banking transactions when labelled fraud data is unavailable.

## Project Overview

Traditional fraud detection systems often rely on labelled datasets containing examples of both legitimate and fraudulent transactions.

However, real-world banking data frequently lacks reliable fraud labels.

This project approaches the problem differently: instead of explicitly learning what fraud looks like, it attempts to learn patterns associated with normal transaction behaviour and identify transactions that deviate from those patterns.

The system uses historical transaction data exported from PhonePe as a starting point for developing a personalized transaction anomaly detection pipeline.

## Objectives

- Develop an unsupervised approach to transaction anomaly detection.
- Understand individual spending patterns using historical transaction data.
- Engineer behavioural and time-based transaction features.
- Analyse transaction frequency and spending velocity.
- Identify potentially suspicious transactions without requiring fraud labels.
- Develop a system capable of evaluating new transactions against historical behaviour.

## Machine Learning Approach

### 1. Data Collection

The initial dataset consists of exported PhonePe transaction history.

The transaction records are processed locally and used to establish a baseline of historical financial behaviour.

### 2. Data Preprocessing

The preprocessing pipeline involves:

- Parsing transaction dates and timestamps.
- Handling missing and invalid records.
- Extracting transaction counterparties.
- Separating debit and credit transactions.
- Sorting transactions chronologically.
- Preparing numerical and categorical features.

### 3. Feature Engineering

Behavioural features are developed to capture different aspects of transaction activity.

| Feature                        | Purpose                                               |
| ------------------------------ | ----------------------------------------------------- |
| Log_Amount                     | Represents transaction amounts on a logarithmic scale |
| Time_Diff_Hours                | Measures the time elapsed between transactions        |
| Counterparty_Transaction_Count | Captures transaction frequency with counterparties    |
| Hour_Sin / Hour_Cos            | Encodes time of day cyclically                        |
| DayOfWeek                      | Captures weekly transaction patterns                  |
| is_debit                       | Distinguishes outgoing from incoming transactions     |

Additional temporal and transaction-velocity features are explored to improve anomaly detection.

### 4. Anomaly Detection

The project explores unsupervised learning techniques, including autoencoder-based anomaly detection.

An autoencoder learns to reconstruct patterns from historical transaction data.

Transactions that significantly deviate from learned patterns may produce higher reconstruction errors, making them potential anomalies.

The objective is to use reconstruction behaviour as an indicator of unusual transaction activity rather than relying on predefined fraud labels.

### 5. Historical Behaviour Analysis

Transaction behaviour is also evaluated using historical lookback windows.

Instead of relying on future transactions, the system considers previously observed activity when evaluating a new transaction.

This allows the project to explore transaction velocity, spending frequency and unusual activity within a defined historical period.

## Technology Stack

| Technology           | Purpose                                    |
| -------------------- | ------------------------------------------ |
| Python               | Core programming language                  |
| Pandas               | Data preprocessing and manipulation        |
| NumPy                | Numerical computation                      |
| Scikit-learn         | Feature preprocessing and ML utilities     |
| TensorFlow / Keras   | Neural network and autoencoder development |
| Matplotlib / Seaborn | Data visualization                         |
| Jupyter Notebook     | Experimentation and development            |

## Repository Structure

```text
Banking-Fraud-Detection/
│
├── notebooks/
│   └── isolation-forest.ipynb
│
├── README.md
└── requirements.txt
```

## Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/aryanshenoy02/Banking-Fraud-Detection.git

cd Banking-Fraud-Detection
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the notebook inside the `notebooks/` directory and execute the cells sequentially.

### 4. Provide transaction data

The notebook requires a compatible PhonePe transaction export.

For privacy reasons, personal transaction records are not included in the public repository.

## Limitations

- The initial dataset represents one individual's transaction history and may not generalize to other customers.
- The absence of verified fraud labels makes conventional supervised evaluation difficult.
- An anomaly does not necessarily indicate fraud.
- New spending patterns may initially be identified as unusual.
- Detection quality depends on the quantity and diversity of historical transaction data.

## Future Improvements

- Experiment with different unsupervised anomaly detection algorithms.
- Improve autoencoder architecture and reconstruction-based scoring.
- Develop adaptive transaction risk scoring.
- Incorporate more sophisticated transaction velocity features.
- Build a reusable prediction interface for evaluating incoming transactions.
- Develop an API for real-time transaction analysis.
- Explore deployment using FastAPI and Docker.

---

**Author:** [Aryan Shenoy](https://github.com/aryanshenoy02)

**GitHub Repository:** [Banking-Fraud-Detection](https://github.com/aryanshenoy02/Banking-Fraud-Detection)

# Banking Fraud Detection – Anomaly Detection

An anomaly detection system that analyses personal PhonePe transaction history using **Isolation Forest** to identify unusual transaction patterns.

## Input Data

- Upload a PhonePe transaction history CSV exported from PhonePe.
- The notebook expects the CSV to contain the following columns:
  - `Transaction ID`
  - `UTR`
  - `Date`
  - `Time`
  - `Transaction Details`
  - `Transaction Type`
  - `Amount`
  - `Credit/debit instrument`
- The CSV should retain the original PhonePe export structure, including the first three metadata rows, which are skipped during loading.

**Privacy:** The notebook processes transaction history containing potentially sensitive financial information. Do not upload personal transaction data to a public repository.

## How It Works

1. **Data preprocessing:** Cleans transaction details, parses timestamps, removes invalid rows and sorts transactions chronologically.
2. **Feature engineering:** Creates behavioural features such as:
   - Log-transformed transaction amount
   - Time difference between consecutive transactions
   - Previous transaction count for each counterparty
   - Cyclical hour encoding
   - New counterparty indicator
   - Debit/credit indicator
3. **Training:** Trains an Isolation Forest on the first 75% of chronologically sorted transactions.
4. **Anomaly detection:** Scores the remaining 25% using the trained model.
5. **Thresholding:** Uses the 99th percentile of training anomaly scores (after familiarity adjustment) to flag unusual transactions.

## Running the Notebook

1. Open `notebooks/isolation-forest.ipynb` in Google Colab.
2. Upload your PhonePe transaction CSV when prompted.
3. Run all notebook cells.
4. Inspect the flagged transactions and their anomaly scores.

## Important Notes

- This is an **unsupervised anomaly detection** system. It learns patterns from historical transactions assumed to be legitimate.
- A flagged transaction is unusual relative to the training data; it is not necessarily fraudulent.
- The system currently uses personal transaction history and is intended as an experimental, customer-specific anomaly detection approach.
- No verified fraud labels are available, so actual fraud detection accuracy cannot currently be measured.

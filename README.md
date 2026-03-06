# Financial Fraud Risk Analytics 

This project performs an in-depth Exploratory Data Analysis (EDA) on financial transaction data to identify patterns and risk factors associated with fraudulent activity. The analysis culminates in an interactive web dashboard that visualizes key performance indicators (KPIs) and risk profiles.

##  Overview

The script automates the retrieval of a financial fraud dataset from Kaggle, systematically handles missing data through targeted imputation strategies, and explores the behavioral characteristics of fraudulent transactions. Finally, it uses `Streamlit` and `pyngrok` to deploy a live, interactive dashboard summarizing the findings.

##  Tech Stack & Libraries

* **Python 3**
* **Kagglehub**: For programmatic downloading of the dataset.
* **Pandas & NumPy**: For data manipulation, aggregations, and mathematical transformations (e.g., log scaling).
* **Matplotlib & Seaborn**: For static data visualization, including histograms, line charts, and heatmaps.
* **Streamlit**: For building the interactive web application/dashboard.
* **Pyngrok**: For creating a secure public URL to host the Streamlit app directly from a notebook environment.

## Dataset

The data is sourced from Kaggle using the `kagglehub` library:
* **Dataset Name**: `fraud-detection-dataset-csv`
* **Author**: `ranjitmandal`
* **File**: `Fraud Detection Dataset.csv`

##  Data Cleaning & Imputation Strategy

The dataset contained several missing values, which were handled thoughtfully to avoid skewing the analysis:
* **`Transaction_Amount`**: Imputed using the **mean** to maintain the average transaction value.
* **`Time_of_Transaction` & `Device_Used`**: Imputed using the **mode** (most frequent occurrence) to represent typical user behavior.
* **`Location` & `Payment_Method`**: Imputed with the string **"Unknown"**. Filling these with the mode would heavily skew categorical analysis, so isolating them as "Unknown" preserves the integrity of the data.

---

## Key Insights & Exploratory Data Analysis

The EDA addresses several critical questions about fraudulent behavior:

### 1. Are frauds associated with higher transaction amounts?
* **Insight:** Fraudsters tend to hide in plain sight. Using a log-transformed distribution, the data reveals that fraudulent transactions rarely occur at extreme high values. Instead, they cluster in the mid-range to mimic normal spending behavior and evade threshold-based detection. 
### 2. Is fraud dependent on time, account age, or transaction velocity?
* **Insight:** Surprisingly, no. Fraud rates remain relatively stable across all 24 hours of the day. Furthermore, neither high transaction velocity (number of transactions in 24 hours) nor account age are strong standalone indicators of fraud, suggesting that account takeovers are just as common as fraudulent new accounts.

### 3. Does previous fraud history matter?
* **Insight:** Yes. Accounts with a history of fraudulent transactions have a noticeably higher probability of committing fraud again, indicating that risk persists over time for specific profiles.

### 4. What is the ultimate "High-Risk" Profile?
* **Insight:** Heatmap analysis combining devices, payment methods, and transaction types reveals the most dangerous combinations:   * Transactions originating from **Unknown devices**.
  * **Online purchases** and **Bill payments**.
  * Digital payment channels (Net banking/UPI).
  * Conversely, traditional methods like ATM withdrawals and POS payments show significantly lower risk.

---

##  How to Run

1. Clone or download the repository.
2. Install the required dependencies:
   ```bash
   pip install kagglehub pandas numpy matplotlib seaborn streamlit pyngrok
   ```
3. Important: To run the Streamlit dashboard via Ngrok, you must add your personal Ngrok Auth Token inside the script:
    ```python
    ngrok.set_auth_token('YOUR_AUTH_TOKEN_HERE')
    ```
4.Execute the script. The EDA will run, and the terminal will output a public Ngrok URL `(e.g., https://<random-id>.ngrok-free.app)` where you can view the live Streamlit dashboard.



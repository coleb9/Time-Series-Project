# Time Series Project — Electricity Load & Renewable Forecasting (Germany)

This project uses deep learning models to forecast hourly electricity load in Germany using data from the Open Power System Data (OPSD) initiative. We compare **LSTM**, **GRU**, and **TCN** architectures to determine which model provides the most accurate next-hour load predictions.

The repository contains a single consolidated notebook (`TimeSeriesProject.ipynb`) with the full workflow: dataset loading, preprocessing, feature engineering, model training, and evaluation.

---

## 📊 Dataset

We use the **OPSD Hourly Time Series** dataset:
[https://data.open-power-system-data.org/time_series/](https://data.open-power-system-data.org/time_series/)

Columns used (Germany):

* `DE_load_actual_entsoe_transparency` — Actual electrical load
* `DE_wind_onshore_generation_actual` — Onshore wind generation
* `DE_solar_generation_actual` — Solar PV generation
* `utc_timestamp` — Timestamp (UTC)

Engineered features:

* Hour of day
* Day of week
* Month of year

---

## 🔧 Preprocessing Pipeline

The notebook applies the following **leakage-free** preprocessing steps:

### **1. Load the dataset**

Read the hourly German electricity dataset "time_series_60min_singleindex.csv" into a pandas DataFrame.

### **2. Select Germany features**

Keep the required columns (load, wind, solar, and engineered time features).

### **3. Fix the timestamp**

Convert the timestamp column to `datetime`, set it as the index, and sort chronologically.

### **4. Handle missing values**

Convert columns to numeric → time-interpolate missing values → forward/backward fill remaining gaps.

### **5. Add time features**

Extract hour, day of week, and month (optionally using cyclical encodings).

### **6. Split into Train / Validation / Test (70 / 15 / 15)**

Perform a chronological split on the **raw, unscaled** data to prevent future information leaking into training.

### **7. Scale all features (WITHOUT leakage)**

Fit the scaler **only on the training split**, then transform the validation and test splits using that scaler.

### **8. Create sliding windows** (past 24h → next-hour load)

Windowing is applied **separately** to the scaled train/val/test data to generate input sequences (`X`) and targets (`y`).

---

## 🤖 Models

Three deep learning architectures were built and evaluated:

* **LSTM** (Long Short-Term Memory)
* **GRU** (Gated Recurrent Unit)
* **TCN** (Temporal Convolutional Network)

Each model uses the past **24 hours** of features to predict the **next hour’s load**.

---

## 📈 Evaluation

Metrics used:

* **MAE** — Mean Absolute Error
* **RMSE** — Root Mean Squared Error
* **Execution Time** 

Visualizations:

* Predicted vs. actual load curves
* Training and validation loss/MAE curves
* Model comparison charts based of calculated metrics

---

## ▶️ Running the Notebook

1. Open the notebook in Google Colab.
2. Upload `time_series_60min_singleindex.csv`.
3. Run all preprocessing cells.
4. Train the LSTM, GRU, and TCN models.
5. Review the evaluation metrics and plots.

---

## 🧑‍🤝‍🧑 Group 11

* Cole Book
* Adam Dunn
* Bryce Nielsen
* Jaemin Cho

---



---



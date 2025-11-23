# Time Series Project — Electricity Load & Renewable Forecasting (Germany)

This project uses deep learning models to forecast hourly electricity load in Germany, using the Open Power System Data (OPSD) dataset. We compare LSTM, GRU, and Transformer architectures to evaluate which model provides the most accurate predictions.

This repository contains a single main notebook (`TimeSeriesProject.ipynb`) that includes the full workflow: dataset loading, preprocessing, feature engineering, model training, and evaluation.

---

## 📊 Dataset

We use the **OPSD Hourly Time Series** dataset:
https://data.open-power-system-data.org/time_series/

Columns used for Germany:
- `DE_load_actual_entsoe_transparency` — Actual electrical load  
- `DE_wind_onshore_generation_actual` — Onshore wind generation  
- `DE_solar_generation_actual` — Solar PV generation  
- `utc_timestamp` — Timestamp (in UTC)

Additional engineered features:
- Hour of day  
- Day of week  
- Month of year  

---

## 🔧 Preprocessing Pipeline

The notebook applies the following preprocessing steps:

### **1. Load the dataset**
### **2. Select Germany features**
### **3. Fix the timestamp**
### **4. Handle missing values**
### **5. Add time features**
### **6. Scale all features**  
### **7. Create sliding windows** (past 24h → next-hour load)
### **8. Train/Validation/Test split** (70 / 15 / 15)

---

## 🤖 Models

We train and compare three deep learning models:

- **LSTM**
- **GRU**
- **Transformer**

Each model uses the past **24 hours** of all features to predict the next hour’s load.

---

## 📈 Evaluation

Metrics:
- **MAE** (Mean Absolute Error)  
- **RMSE** (Root Mean Squared Error)

Plots:
- Predicted vs. actual  
- Loss curves  
- Model comparison bar charts  

---

## ▶️ Running the Notebook

1. Open the notebook in Google Colab.
2. Upload the `time_series_60min_singleindex.csv` file.
3. Run preprocessing.
4. Train each model.
5. View evaluation results.

---

## 🧑‍🤝‍🧑 Group 11

- Cole Book  
- Adam Dunn  
- Bryce Nielsen  
- Jaemin Cho  

---



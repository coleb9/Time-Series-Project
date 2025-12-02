# Time Series Project — Electricity Load & Renewable Forecasting (Germany)

## Project Overview
This project implements and benchmarks advanced deep learning architectures to forecast the hourly electricity load in Germany. Using data from the Open Power System Data (OPSD) initiative, we compare LSTM, GRU, and TCN models to determine the most effective approach for grid demand prediction.

A key focus of this project is feature ablation (Univariate vs. Multivariate analysis) to quantify the predictive value of including renewable energy generation data (Wind and Solar).

The repository contains a single consolidated notebook (`Group-11_Time_Series_Project_Final.ipynb`) with the full workflow: dataset loading, preprocessing, feature engineering, model training, and evaluation.


## Dataset

We use the **OPSD Hourly Time Series** dataset:
[https://data.open-power-system-data.org/time_series/](https://data.open-power-system-data.org/time_series/)

### Input Features (Germany):

* `DE_load_actual_entsoe_transparency` — Actual electrical load
* `DE_wind_onshore_generation_actual` — Onshore wind generation
* `DE_solar_generation_actual` — Solar PV generation
* `utc_timestamp` — Timestamp (UTC)
* Engineered features: Hour of day, Day of week, Month of year


## Methodology & Pipeline
The notebook (`Group-11_Time_Series_Project_Final.ipynb`) follows a strict leakage-free preprocessing pipeline:

1. Data Ingestion: Loading specific German energy columns.

2. Imputation: Time-based interpolation to handle missing values without altering trends.

3. Chronological Split: * Train: 70% | Validation: 15% | Test: 15%

      - _Note_: Data is NOT shuffled to preserve temporal order.

4. Feature Scaling: Standard Scaling fitted only on the Training set to prevent data leakage.

5. Windowing: Sliding window approach (Lookback: 24 hours → Prediction: Next Hour).


## Model Architectures
We implemented three distinct architectures to handle the time-series data:

1. LSTM (Long Short-Term Memory): * Stacked architecture with Dropout.

      - Optimized via Grid Search for units and learning rate.

2. GRU (Gated Recurrent Unit): * Evaluated in both Univariate and Multivariate configurations.

      - Proved more efficient than LSTM due to streamlined gating (3 gates vs 4).

3. TCN (Temporal Convolutional Network): * Uses Dilated Causal Convolutions to capture long-term dependencies.

      - Optimized using Bayesian Optimization (Keras Tuner) to select the best kernel size, filter count, and dilation depth.


## Evaluation

Metrics used:

* **MAE** — Mean Absolute Error
* **RMSE** — Root Mean Squared Error
* **Execution Time** 

Visualizations:

* Predicted vs. actual load curves
* Training and validation loss/MAE curves
* Model comparison charts based of calculated metrics


## Running the Notebook

1. Open the notebook in Google Colab.
2. Upload `time_series_60min_singleindex.csv`.
3. Run all preprocessing cells.
4. Train the LSTM, GRU, and TCN models.
5. Review the evaluation metrics and plots.


## Group 11 Members

* Cole Book
* Adam Dunn
* Bryce Nielsen
* Jaemin Cho


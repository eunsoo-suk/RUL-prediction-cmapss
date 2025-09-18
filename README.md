## Turbofan Engine RUL Prediction
### 📌 Project Overview

This project aims to predict the Remaining Useful Life (RUL) of turbofan engines using NASA’s CMAPSS dataset.
Multivariate sensor time series data are preprocessed and fed into sequence models (LSTM / GRU) to estimate how many cycles remain before failure.
The workflow includes data preparation, sliding-window sequence generation, model training/validation, and evaluation on the official test set.

### 📂 Dataset Composition

[Download RUL Dataset](https://drive.google.com/file/d/1smfbeqOaf4UEEY5ulXlOZMMB3TXwNtqp/view?usp=drive_link)

- Source: NASA CMAPSS Turbofan Engine Degradation Dataset

- Train set: Full run-to-failure sensor sequences for multiple engine units

- Test set: Partial sequences (censored before failure)

- RUL labels: Provided separately for test units

- Features: 21 sensor readings + operational settings per time step
Target: Remaining Useful Life (RUL) in cycles

### ⚙️ Workflow

**Data Preparation**

- Load CMAPSS dataset (FD001 subset)

- Handle missing values, normalize features

- Compute RUL for each cycle (max time − current time)

**Sequence Generation**

- Sliding-window approach to create time series sequences

- Unit-aware splitting for train/validation/test

**Model Training**

- Implemented LSTM and GRU models

- Loss: MAE, Optimizer: Adam

- Early stopping + ReduceLROnPlateau

**Evaluation**

- Metrics: MAE, RMSE, R²

- Test set evaluated on last window per unit

### 📊 Results (Example)

- LSTM: MAE = 16.8, RMSE = 22.5, R² = 0.72

- GRU: MAE = 15.9, RMSE = 21.3, R² = 0.75

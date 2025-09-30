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

- LSTM: MAE = 16.428, RMSE = 24.454, R² = 0.824
  
- GRU: MAE = 16.904, RMSE = 24.453, R² = 0.824

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/78a01b0e-bb9c-484b-a4ef-5fc471aa4142" width="400"><br>
      <sub>LSTM Parity Plot</sub>
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/1cc555ab-1178-4697-b7b5-802252a49594" width="400"><br>
      <sub>GRU Parity Plot</sub>
    </td>
  </tr>
</table>


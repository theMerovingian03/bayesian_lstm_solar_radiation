# Bayesian Solar Irradiance Forecasting

This project demonstrates **uncertainty-aware forecasting of solar irradiance** using a **Bayesian Long Short-Term Memory (LSTM) neural network**. The model predicts daily **Global Horizontal Irradiance (GHI)** and provides **confidence intervals** for predictions, allowing us to understand both the forecast and its associated uncertainty.

The project is part of the research work titled:

**“Uncertainty Quantification in Solar Irradiance Forecasting Using Bayesian Deep Learning.”**

---

## Installation
Recommended Python version: **Python 3.13.3** to avoid Pytorch compatibility issues.

1. Create virtual environment: ```py -3.13 -m venv myenv```
2. Activate ```myenv\Scripts\activate```
3. Install dependencies ```pip install -r requirements.txt```

## Dataset

The dataset used in this project comes from **NASA POWER (Prediction Of Worldwide Energy Resources)**.

**Location:** Kothrud, Pune, India  
**Time Range:** 1 January 2003 – 31 December 2023  
**Frequency:** Daily observations

### Key Variable Used

| Variable | Description |
|--------|-------------|
| `ALLSKY_SFC_SW_DWN` | Global Horizontal Irradiance (GHI) in kWh/m²/day |

Other dataset fields include:

- `YEAR`
- `MO` (Month)
- `DY` (Day)

These are combined to create a **datetime index** for time-series modeling.

---

## Project Objective

The goal of this project is to:

- Forecast **daily solar irradiance**
- Quantify **prediction uncertainty**
- Demonstrate the use of **Bayesian deep learning for renewable energy forecasting**

Unlike traditional models that provide only a **single predicted value**, this model produces:

- A **predicted mean**
- A **95% confidence interval**

This helps assess the **reliability of predictions**.

---

## Method Overview

The forecasting pipeline follows these steps:

1. **Load and preprocess NASA POWER data**
2. **Normalize the irradiance values**
3. **Create sliding-window time series sequences**
4. **Train a Bayesian LSTM model**
5. **Use Monte Carlo Dropout to estimate uncertainty**
6. **Generate predictions and confidence intervals**
7. **Evaluate model performance**

---

## Model Architecture

The model uses a simple **Bayesian LSTM structure**:

- **Input:** 7 previous days of GHI
- **LSTM Layer:** 32 hidden units
- **Dropout Layer:** 0.3 dropout rate
- **Output Layers:**
  - Mean prediction
  - Standard deviation estimate

Dropout remains active during inference, enabling **Monte Carlo sampling**.

---

## Uncertainty Estimation

The model uses **Monte Carlo Dropout**:

1. The same input is passed through the network **100 times**.
2. Each pass produces a slightly different prediction due to dropout.
3. These predictions form a **distribution**.

From this distribution we compute:

- **Mean prediction**
- **95% confidence interval**

This provides an estimate of **prediction uncertainty**.

---

## Model Performance

The model was evaluated using standard regression metrics:

| Metric | Value |
|------|------|
| Mean Squared Error (MSE) | 0.4898 |
| Root Mean Squared Error (RMSE) | 0.6999 |
| Mean Absolute Error (MAE) | 0.4916 |
| R² Score | 0.7639 |

These results show that the model captures the **temporal patterns of solar irradiance effectively** while also providing **useful uncertainty estimates**.

---

## Output

The script generates:

### 1. Forecast Visualization
A plot showing:

- Actual GHI values
- Predicted mean values
- 95% confidence interval

### 2. Prediction Results File

`prediction_results.csv`

Contains:

| Column | Description |
|------|-------------|
| Date | Observation date |
| Actual | True GHI value |
| Predicted_Mean | Model prediction |
| Lower_CI | Lower bound of 95% confidence interval |
| Upper_CI | Upper bound of 95% confidence interval |

---

## Key Highlights

- Uses **21 years of real solar irradiance data**
- Implements **Bayesian Deep Learning**
- Provides **uncertainty-aware forecasts**
- Demonstrates practical application for **solar energy forecasting**

### Improvements:
- Use of a GPU (if available)
- Feel free to contribute for any other improvements

## Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Scikit-learn
- Matplotlib

---

## Research Context

This implementation supports the research study:

**"Uncertainty Quantification in Solar Irradiance Forecasting Using Bayesian Deep Learning."** (dated: April 2025)

The project demonstrates how **probabilistic deep learning models** can improve decision-making in **renewable energy systems** by incorporating **prediction uncertainty**.

---
# 📈 Stacked LSTM Stock Price Prediction & Mock Trading

> **Deep learning for stock prediction** — stacked LSTM model trained on historical price data, evaluated against a mock trading simulation with buy/sell signal generation and profit tracking.

---

## ✨ What It Does

1. **Fetches** historical stock price data from Yahoo Finance (`yfinance`)
2. **Preprocesses** — resamples to daily frequency, interpolates gaps, scales with MinMaxScaler
3. **Trains** a stacked LSTM (multiple layers + Dense output) to predict next-day closing price
4. **Evaluates** with MSE, early stopping, and learning rate reduction on plateau
5. **Simulates** a mock trading environment — buy/sell decisions based on predicted vs actual price
6. **Visualises** actual vs predicted prices and trading P&L

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat-square&logo=keras&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square&logoColor=white)

---

## 🧠 Model Architecture

```
Input (sequence of N days)
        │
        ▼
┌───────────────────┐
│  LSTM Layer 1     │  return_sequences=True
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  LSTM Layer 2     │  return_sequences=True
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  LSTM Layer 3     │  return_sequences=False
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  Dense (1)        │  Predicted next-day closing price
└───────────────────┘

Training: Adam optimizer · MSE loss
Callbacks: EarlyStopping · ReduceLROnPlateau
```

---

## 💰 Mock Trading Strategy

| Signal | Condition | Action |
|--------|-----------|--------|
| **Buy** | Predicted price > previous actual price | Purchase stock |
| **Sell** | Predicted price < previous actual price | Sell holdings |
| **Hold** | No signal | Do nothing |

Tracks capital, owned shares, and final portfolio value to calculate total return.

---

## 🏗️ Project Structure

```
stock-price-analysis-and-algorithmic-trading-model/
├── SCRIPTS/
│   ├── StackedLSTM.ipynb   # Full workflow: data → model → trading sim
│   ├── SMA.ipynb           # Simple Moving Average baseline
│   └── AAPL_daily.csv      # Example dataset (Apple, daily OHLCV)
├── requirements.txt
└── README.md
```

---

## 🚀 Running Locally

### Prerequisites
- Python 3.10+
- Jupyter Notebook or JupyterLab

### Install & run

```bash
git clone https://github.com/iKatiyar/stock-price-analysis-and-algorithmic-trading-model.git
cd stock-price-analysis-and-algorithmic-trading-model

pip install -r requirements.txt
jupyter notebook SCRIPTS/StackedLSTM.ipynb
```

### Fetch data for any stock

```python
from datetime import datetime
stock_data = prepare_ticker_data("TSLA", start_date="2015-01-01")
```

Replace `"TSLA"` with any valid ticker symbol.

---

## 📊 Key Functions

| Function | Description |
|----------|-------------|
| `get_ticker_data()` | Fetch OHLCV data from Yahoo Finance |
| `clean_ticker_data()` | Rename columns, parse dates |
| `resample()` | Resample to daily frequency, fill gaps |
| `basic_preprocess()` | Interpolate missing values, cast to float |
| `prepare_ticker_data()` | Full pipeline: fetch → clean → resample → preprocess |

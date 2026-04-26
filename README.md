# CS3 Case Study
# Forecasting Amazon Stock Price: ARIMA vs. LSTM

**Course:** DS 4002 
**Date:** Spring 2026  
**Contributor:** Victoria Markakis  
**Instructor:** Professor Siller

---

## Contents of the Repository

```
CS3-Amazon-Forecasting/
├── README.md
├── Hook Document.pdf
├── Rubric.pdf
├── DATA/
│   ├── amazon_data.csv               # Raw MacroTrends daily closing prices (1997–2026)
│   └── Dataset_Details.md            # Variable descriptions and source info
├── SCRIPTS/
│   └── amazon_forecasting.ipynb      # Full forecasting pipeline (ARIMA + LSTM)
└── SUPPLEMENTAL MATERIALS/
    ├── explainer_arima_to_lstm.pdf    # Beginner-friendly time series tutorial
    └── amazon_stock_analysis.pdf     # Domain context article
```

---

## Section 1: Software and Platform

### Software Used
- Python 3.10
- Jupyter Notebook / Google Colab

### Required Packages
```
pip install darts pytorch-lightning torch statsforecast "numpy<2"
```

Additional standard libraries: `pandas`, `numpy`, `matplotlib`, `scipy`, `statsmodels`

> **Note:** The `darts` library provides unified wrappers for both AutoARIMA and LSTM (RNNModel).
> Install `numpy<2` to avoid version conflicts with darts.

---

## Section 2: Dataset

- **Source:** MacroTrends — https://macrotrends.net/stocks/charts/AMZN/amazon/stock-price-history
- **Coverage:** May 15, 1997 to February 24, 2026
- **Observations:** 7,239 trading days
- **Target variable:** Daily closing price (split-adjusted, USD)
- **Columns:** date, open, high, low, close, volume

Holiday gaps (non-trading days) are filled using `fill_missing_dates=True` with business-day frequency (`freq='B'`).

---

## Section 3: Instructions for Reproducing the Workflow

1. Clone the repository
```bash
git clone https://github.com/[your-username]/CS3-Amazon-Forecasting.git
cd CS3-Amazon-Forecasting
```

2. Install dependencies
```bash
pip install darts pytorch-lightning torch statsforecast "numpy<2"
```

3. Open the notebook
```
SCRIPTS/amazon_forecasting.ipynb
```

4. Run cells in order:
   - Data loading and preprocessing
   - EDA (price history, distributions, volume)
   - Stationarity testing (ADF test, ACF/PACF)
   - Train/val/test split (80/10/10 chronological)
   - AutoARIMA model: fit, validate, test
   - LSTM model: normalize, fit, validate, test
   - Model comparison (MAE, RMSE, MAPE)
   - 2026 forecast (both models on full dataset)

---

## Section 4: Key Results

| Metric   | ARIMA   | LSTM    |
|----------|---------|---------|
| MAE ($)  | 77.52   | 30.36   |
| RMSE ($) | 85.24   | 36.21   |
| MAPE (%) | 39.39   | 16.10   |

**Winner: LSTM** — roughly 59% lower MAPE than ARIMA on the test set (2023–2026).

Both models projected an end-of-2026 Amazon price near **$217–218**.

---

## Section 5: Purpose of the Project

This project explores whether deep learning (LSTM) outperforms classical statistical forecasting (ARIMA) on a long-horizon, real-world financial time series. The workflow covers data acquisition, preprocessing, stationarity analysis, model building with the Darts library, rigorous train/val/test evaluation, and future forecasting.

---

## Section 6: References

- MacroTrends. Amazon Stock Price History. https://macrotrends.net
- Darts Documentation. Unit8. https://unit8co.github.io/darts/
- Machine Learning Mastery. Mastering Time Series Forecasting: From ARIMA to LSTM.
- Hochreiter, S. & Schmidhuber, J. (1997). Long Short-Term Memory. *Neural Computation*, 9(8).

---

## License

MIT License — authored by Victoria Markakis, DS 4002, Spring 2026.

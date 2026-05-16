# Stock Price Prediction (Short-Term Forecasting    )

Predicting the next day’s closing price using historical stock data from Yahoo Finance.

## Overview

This project explores a beginner-to-intermediate machine learning workflow for time series-style stock prediction. The goal is to use historical market features to predict the **next day’s closing price** and compare model predictions against real values.

It was built as a hands-on practice project to strengthen skills in:

- data fetching with APIs
- pandas-based data cleaning and feature engineering
- descriptive statistics and time-based exploration
- regression modeling
- model evaluation
- visualization of actual vs predicted values

## Objective

Use historical stock data to predict the **next day’s closing price**.

## Data Source

- **Yahoo Finance**
- Retrieved using the **`yfinance`** Python library

## Features Used

The following features were used for modeling:

- `Open`
- `High`
- `Low`
- `Volume`

Engineered features:

- `MA5` — 5-day moving average
- `MA10` — 10-day moving average
- `Daily Range` — `High - Low`
- `Volatility` — rolling price variation
- `Prev Close` — previous day's closing price

## Target Variable

The target is the **next day’s closing price**:

```python
df["Target"] = df["Close"].shift(-1)
```

## Train/Test Split

The dataset was split using a **chronological 80/20 split**.

This means:

- earlier dates were used for training
- later dates were used for testing

No shuffle was used, because the data follows time order and should not be randomized.

## Models Used

Two regression models were trained and compared:

- **Linear Regression**
- **Random Forest Regressor**

## Evaluation Metrics

The following metrics were used to evaluate the models:

- **MAE** — Mean Absolute Error
- **RMSE** — Root Mean Squared Error
- **R²** — Coefficient of Determination
- **MAPE** — Mean Absolute Percentage Error

In addition, **residual plots** were used to inspect prediction errors.

## Results Summary

| Aspect | What I Did |
|---|---|
| **Data Source** | Yahoo Finance via `yfinance` API |
| **Features** | Open, High, Low, Volume + engineered: MA5, MA10, Daily Range, Volatility, Prev Close |
| **Target** | Next day's closing price (`Close.shift(-1)`) |
| **Split** | Chronological 80/20 — no shuffle (respects time order) |
| **Models** | Linear Regression & Random Forest Regressor |
| **Evaluation** | MAE, RMSE, R², MAPE + residual plots |

## Project Workflow

1. Fetch historical stock data from Yahoo Finance.
2. Inspect the dataset using pandas.
3. Clean the data and handle missing values created by feature engineering.
4. Create the target column for next-day prediction.
5. Engineer additional features to improve model input.
6. Split data chronologically into train and test sets.
7. Train regression models.
8. Evaluate model performance.
9. Plot actual vs predicted closing prices.

## Visualizations Included

- historical price trends
- feature distribution plots
- actual vs predicted closing price comparison
- residual plots

## Key Takeaways

- Time order matters in stock prediction, so random shuffling should be avoided.
- Feature engineering can help capture short-term market behavior better than raw OHLC data alone.
- Linear Regression is a useful baseline.
- Random Forest can capture nonlinear patterns better, but stock data remains noisy and difficult to predict accurately.
- Prediction performance should be interpreted carefully, since stock prices are influenced by many external factors not included in the dataset.

## Tech Stack

- **Python**
- **pandas**
- **numpy**
- **matplotlib**
- **seaborn**
- **yfinance**
- **scikit-learn**

## Setup Instructions

### 1. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn yfinance scikit-learn
```

### 2. Run the notebook

Open the notebook in:

- Kaggle Notebook
- Google Colab
- Jupyter Notebook

### 3. Fetch data

Use `yfinance` to download stock history:

```python
import yfinance as yf

df = yf.download("AAPL", period="5y", interval="1d")
```

## Folder Structure

```text
stock-price-prediction/
├── notebook.ipynb
├── README.md
└── images/
    ├── actual_vs_predicted.png
    └── residual_plot.png
```

## Limitations

- Stock prices are highly volatile and influenced by many external events.
- This project uses a short-term regression setup, so results should not be treated as financial advice.
- Performance may vary depending on the selected stock and time range.
- Internet access may be required for `yfinance` to fetch live data.

## Future Improvements

- Add more technical indicators
- Try LSTM / GRU / XGBoost models
- Use walk-forward validation
- Add model tracking with MLflow
- Deploy the model using Streamlit or FastAPI
- Build an interactive dashboard for predictions

## License

For learning and portfolio use.

## Author

Built as a hands-on machine learning practice project.

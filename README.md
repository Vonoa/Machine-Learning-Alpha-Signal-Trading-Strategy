# Alpha Signal Engineering & Monte Carlo Validation

A machine learning-driven trading strategy using Random Forest regression trained on technical alpha signals, with robust validation through walk-forward analysis and Monte Carlo resampling.

## 📊 Project Overview

This project implements a quantitative trading strategy that:
- Engineers multiple alpha signals from price momentum, trend, and volatility
- Trains a Random Forest Regressor to predict future returns
- Uses walk-forward validation to simulate realistic model retraining
- Employs Monte Carlo resampling with antithetic variates to assess robustness
- Compares performance against buy-and-hold and naive benchmarks

**Goal**: Evaluate whether learned predictive signals outperform basic benchmarks on risk-adjusted returns (Sharpe ratio).

## 🎯 Key Results

- **Walk-Forward Validation Sharpe Ratio**: 1.78
- **Monte Carlo Mean Sharpe Ratio**: 1.54 (Median: 1.62)
- **Success Rate**: 61.6% of simulations achieved Sharpe > 1.5
- **Excess Returns vs Buy & Hold**: +1,579.88%
- **Maximum Drawdown**: -87.06%
- **Calmar Ratio**: 29.95

## 🔧 Features

### Alpha Signal Engineering

The strategy generates five categories of technical indicators:

1. **Simple Moving Averages (SMA)**: Periods of 10, 30, 60, 120, 240 days
2. **Momentum Signals**: SMA crossovers (10-30, 30-60, 60-120, 120-240)
3. **Trend Signals**: Rate of Change (ROC) over 20, 60, 120 days
4. **Ratio Signals**: Short-term to long-term SMA ratios
5. **Volatility Signal**: 14-day Average True Range (ATR)

### Trading Logic

- **Position Sizing**: Long (+1), Short (-1), or Neutral (0) based on predicted returns
- **Trend Filter**: SMA-100 filter prevents shorting in uptrending markets
- **Prediction Threshold**: ±0.15% return threshold for signal generation
- **Target**: 10-day forward returns

### Validation Methods

#### Walk-Forward Validation
- 70/30 train-validation split
- Chronological ordering preserved (no look-ahead bias)
- Single realistic out-of-sample test

#### Monte Carlo Resampling
- 500 simulation pairs with antithetic variates
- Random training proportions between 60-85%
- Variance reduction through complementary splits
- Robustness assessment across different market regimes

## 📈 Performance Metrics

| Metric | ML Strategy | Benchmark (Always Long) | Buy & Hold |
|--------|-------------|-------------------------|------------|
| Total Return | 2,607% | 10,317% | 61% |
| Sharpe Ratio | 1.78 | 2.37 | 0.70 |
| Max Drawdown | -87.06% | -93.09% | -25.36% |
| Calmar Ratio | 29.95 | 110.83 | 2.41 |

## 📦 Dependencies

- Python 3.7+
- numpy
- pandas
- yfinance
- matplotlib
- scikit-learn

## 📊 Mathematical Foundations

### Alpha Signals

**Simple Moving Average**:
```
SMA(n) = (1/n) × Σ(P[t-i]) for i=0 to n-1
```

**Rate of Change**:
```
ROC(n) = (P[t] / P[t-n]) - 1
```

**Average True Range**:
```
TR[t] = max(High[t] - Low[t], |High[t] - Close[t-1]|, |Low[t] - Close[t-1]|)
ATR(n) = (1/n) × Σ(TR[t-i])
```

### Performance Metrics

**Sharpe Ratio**:
```
Sharpe = √252 × E[R] / σ(R)
```

**Drawdown**:
```
DD[t] = (P[t] - max(P[0:t])) / max(P[0:t]) × 100%
```

**Calmar Ratio**:
```
Calmar = Total Return / |Max Drawdown|
```

## 🎨 Visualizations

The project generates three key plots:

1. **Cumulative Returns**: Log-scale comparison of strategy vs benchmarks
2. **Strategy Drawdown**: Peak-to-trough decline visualization
3. **Benchmark Drawdown**: Comparative risk assessment
4. **Monte Carlo Distribution**: Histogram of Sharpe ratios across simulations

## ⚠️ Risk Disclaimer

This project is for **educational and research purposes only**. It is not financial advice. Key risks include:

- **High Drawdown Risk**: Maximum drawdown of -87% observed
- **Overfitting**: ML models may overfit historical patterns
- **Transaction Costs**: Real-world costs not included in simulations
- **Market Regime Changes**: Past performance doesn't guarantee future results
- **Execution Risk**: Slippage and market impact not modeled

**Do not use this strategy for live trading without extensive additional testing and risk management.**

## 📚 References

- **Random Forests**: Breiman, L. (2001). "Random Forests." Machine Learning, 45(1), 5-32.
- **Sharpe Ratio**: Sharpe, W.F. (1966). "Mutual Fund Performance." Journal of Business, 39(1), 119-138.
- **Monte Carlo Methods**: Glasserman, P. (2003). "Monte Carlo Methods in Financial Engineering."
- **Technical Analysis**: Murphy, J.J. (1999). "Technical Analysis of the Financial Markets."

## 👤 Author
- GitHub: https://github.com/Vonoa
- LinkedIn: https://www.linkedin.com/in/aled-von-oppell-40b315289/

## ⭐ Show Your Support

If you find this project helpful, please give it a ⭐️!

---

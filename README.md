# Quant Project 2 — Pairs Trading Strategy

## Overview

This project develops and backtests a **statistical arbitrage pairs trading strategy** using two historically related stocks: **Coca-Cola (KO)** and **PepsiCo (PEP)**.

The strategy is based on the idea that two assets with a stable long-term relationship may temporarily diverge in price. When the spread between them moves sufficiently far from its historical mean, the strategy takes a position expecting the spread to converge again.

The project covers the complete process from identifying a suitable pair to evaluating the strategy on unseen data.

---

## Objectives

The main objectives of this project are to:

* Investigate the relationship between two financial assets
* Estimate a hedge ratio using linear regression
* Test for cointegration using the **Engle-Granger test**
* Construct a mean-reverting spread
* Generate trading signals using **z-scores**
* Backtest a pairs trading strategy
* Incorporate transaction costs
* Evaluate risk-adjusted performance
* Compare training and out-of-sample test performance
* Compare the strategy against simple buy-and-hold benchmarks

---

## Methodology

### 1. Pair Selection

KO and PEP were selected as the trading pair due to their similar business exposure and historical relationship.

The relationship between their prices is modelled as:

$$
KO_t = \\alpha + \\beta PEP_t + \\epsilon_t
$$

where:

* $\alpha$ is the regression intercept
* $\beta$ is the hedge ratio
* $\epsilon_t$ represents the residual spread

---

### 2. Cointegration Testing

Correlation alone does not imply that two assets have a stable long-term relationship.

The **Engle-Granger cointegration test** is therefore applied to the price series.

The null hypothesis is that the two series are **not cointegrated**.

A sufficiently small p-value provides evidence against the null hypothesis and supports the use of a pairs trading strategy.

---

### 3. Spread Construction

The spread is constructed using the estimated regression parameters:

$$
Spread_t = KO_t - \\beta PEP_t
$$

The historical mean and standard deviation of the spread are then used to calculate its z-score:

$$
z_t = \\frac{Spread_t - \\mu_{Spread}}{\\sigma_{Spread}}
$$

This standardises the spread and allows deviations from its historical level to be interpreted consistently.

---

### 4. Trading Strategy

The strategy trades when the z-score moves sufficiently far from zero.

* **Large positive z-score:** spread considered unusually high → short the spread
* **Large negative z-score:** spread considered unusually low → long the spread
* **Z-score returns towards zero:** close the position

This creates a market-neutral framework where the strategy attempts to profit from relative mispricing rather than the overall direction of the market.

---

## Backtesting

The dataset is divided into **training and test periods**.

The training period is used to estimate the relationship between KO and PEP and determine the parameters of the strategy.

The test period is then used to evaluate how the strategy performs on previously unseen data.

This separation helps reduce the risk of evaluating the strategy using information that would not have been available at the time of trading.

---

## Performance

### Training Period

| Metric           | Result |
| ---------------- | -----: |
| Total Return     | 23.70% |
| Sharpe Ratio     |  0.661 |
| Maximum Drawdown | -7.36% |

### Test Period

| Metric           | Result |
| ---------------- | -----: |
| Total Return     |  8.59% |
| Sharpe Ratio     |  0.620 |
| Maximum Drawdown | -8.08% |

### Benchmark Comparison

| Strategy               | Total Return |
| ---------------------- | -----------: |
| KO Buy & Hold          |       14.91% |
| PEP Buy & Hold         |       -4.18% |
| 50/50 KO–PEP           |        5.48% |
| Pairs Trading Strategy |    **8.59%** |

The strategy produced a positive return during the out-of-sample test period and outperformed the 50/50 KO–PEP benchmark.

However, the lower test-period performance relative to the training period highlights the importance of evaluating quantitative strategies out of sample.

---

## Risk Analysis

Several performance metrics are used to evaluate the strategy:

### Sharpe Ratio

The annualised Sharpe ratio measures risk-adjusted returns:

$$
Sharpe = \\frac{E[R_p - R_f]}{\\sigma_p}\\sqrt{252}
$$

where $R_p$ is the portfolio return, $R_f$ is the risk-free rate, and $\sigma_p$ is portfolio volatility.

### Maximum Drawdown

Maximum drawdown measures the largest decline from a previous portfolio peak:

$$
MDD = \\min_t \\left(\\frac{V_t}{\\max_{s\\leq t}V_s}-1\\right)
$$

It provides an indication of the strategy's worst historical loss from peak to trough.

### Profit Factor

Profit factor is calculated as:

$$
Profit\\ Factor =
\\frac{Gross\\ Profits}{Gross\\ Losses}
$$

A value greater than 1 indicates that total profits from winning trades exceeded total losses from losing trades.

---

## Key Results

The backtest demonstrates several important characteristics of quantitative trading:

1. A statistically related pair can be identified using cointegration rather than simple correlation.
2. Z-scores provide a systematic method for generating entry and exit signals.
3. Transaction costs can reduce strategy performance and should be incorporated into realistic backtests.
4. Training performance does not necessarily translate directly into future performance.
5. Out-of-sample testing is therefore essential when evaluating a trading strategy.

---

## Limitations

This project is a simplified research backtest and does not represent a production trading system.

Important limitations include:

* Only one stock pair is considered
* Historical relationships may break down
* Model parameters are estimated from historical data
* The strategy does not model market impact
* Transaction costs are simplified
* Execution delays and liquidity constraints are not fully modelled
* The backtest does not guarantee future profitability

A more robust strategy would test many candidate pairs, use rolling parameter estimation, perform sensitivity analysis, and incorporate more realistic execution assumptions.

---

## Technologies

* **Python**
* **NumPy**
* **Pandas**
* **Matplotlib**
* **SciPy**
* **Statsmodels**
* **Jupyter Notebook**

---

## Project Structure

```text
quant-project-2-pairs-trading/
│
├── pairs_trading.ipynb
├── README.md
└── requirements.txt
```

---

## What I Learned

This project developed my understanding of:

* Statistical arbitrage
* Linear regression
* Cointegration
* Mean reversion
* Time-series analysis
* Z-score based trading signals
* Backtesting methodology
* Transaction costs
* Sharpe ratio and drawdown analysis
* Out-of-sample testing
* Benchmark comparison

The project also reinforced the importance of distinguishing between **a strategy that performs well historically and a strategy that is genuinely robust**.

*To be completed after the project is finished.*

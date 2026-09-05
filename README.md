# Quant Project 2 — Pairs Trading

## Overview

A Python implementation and backtest of a **statistical arbitrage pairs trading strategy** using Coca-Cola (KO) and PepsiCo (PEP).

The project investigates whether the two stocks exhibit a stable long-term relationship and attempts to profit from temporary deviations in their price relationship.

## Methodology

* Estimate the hedge ratio using linear regression
* Test for cointegration using the Engle-Granger test
* Construct the price spread
* Calculate spread z-scores
* Generate long/short trading signals based on z-score thresholds
* Backtest the strategy including transaction costs
* Evaluate performance using returns, Sharpe ratio and maximum drawdown
* Compare training and out-of-sample test performance

## Results

| Metric           | Training |   Test |
| ---------------- | -------: | -----: |
| Total Return     |   23.70% |  8.59% |
| Sharpe Ratio     |    0.661 |  0.620 |
| Maximum Drawdown |   -7.36% | -8.08% |

The strategy achieved a **8.59% return and 0.62 Sharpe ratio on the out-of-sample test period**.

For comparison, a 50/50 KO–PEP buy-and-hold portfolio returned 5.48% over the same test period.

## Technologies

Python, NumPy, Pandas, Matplotlib, SciPy, Statsmodels, Jupyter Notebook.

## Key Concepts

**Cointegration · Mean Reversion · Statistical Arbitrage · Z-Scores · Backtesting · Risk-Adjusted Returns**

## Disclaimer

This is an educational quantitative finance project and does not constitute investment advice.

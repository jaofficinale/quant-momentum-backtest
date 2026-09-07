# Cross-Asset ETF Momentum Backtest

## Objective

This project tests whether a monthly-rebalanced, long-only ETF momentum strategy can outperform an equal-weight benchmark after estimated trading costs.

The project is an educational historical simulation. It is not investment advice and does not establish future performance.

## Research question

Can a 12–1 cross-sectional momentum strategy, holding the three strongest ETFs in a diversified ETF universe, outperform an equal-weight benchmark after accounting for turnover-based transaction costs?

## Universe

- SPY: U.S. large-cap equities
- QQQ: U.S. technology/growth equities
- IWM: U.S. small-cap equities
- EFA: Developed international equities
- EEM: Emerging-market equities
- TLT: Long-term U.S. Treasury bonds
- IEF: Intermediate U.S. Treasury bonds
- GLD: Gold
- VNQ: U.S. real-estate investment trusts

## Strategy rules

- Signal: trailing 12–1 month momentum
- Formation: end of each month
- Holdings: three ETFs with the highest signal
- Weighting: equal weight, 33.33% per selected ETF
- Rebalancing: monthly
- Cost assumption: 10 basis points per unit of one-way turnover
- Benchmark: equal-weight portfolio of all ETFs
- Risk-free rate: assumed to be zero for the reported Sharpe ratio

## Methodology safeguards

- Adjusted price data are downloaded from Yahoo Finance using `yfinance`.
- Signals use lagged monthly prices.
- Portfolio weights are lagged before being multiplied by realized returns.
- Turnover is calculated from changes in target asset weights.
- Estimated transaction costs are deducted from gross monthly strategy returns.
- Robustness checks test alternative holding counts, momentum lookbacks, and trading-cost assumptions.

## Results

Insert your actual result table here after running `04_evaluation.ipynb`.

| Metric | Momentum strategy, net | Equal-weight benchmark |
|---|---:|---:|
| Annualised return | [x%] | [x%] |
| Annualised volatility | [x%] | [x%] |
| Sharpe ratio | [x.xx] | [x.xx] |
| Maximum drawdown | [x%] | [x%] |
| Average monthly turnover | [x%] | N/A |

## Figures

![Equity curve](figures/equity_curve_gross_net_benchmark.png)

![Drawdowns](figures/drawdowns.png)

![Monthly turnover](figures/monthly_turnover.png)

## Robustness checks

Summarize whether performance remains similar across:

- Top 2, top 3, and top 4 holdings
- 6–1, 9–1, and 12–1 momentum signals
- 5, 10, and 25 basis-point transaction-cost scenarios

Report every tested variation rather than choosing only the most favorable configuration.

## Limitations

- Historical simulations do not predict future returns.
- The ETF universe was manually selected and may create selection bias.
- Yahoo Finance is convenient public data, not institutional-grade survivorship-bias-free data.
- The transaction-cost model is simplified and excludes taxes, bid–ask spreads, market impact, borrowing, and execution timing.
- Monthly adjusted closing prices do not model the exact intraday time at which trades could be executed.

## How to run

```bash
conda create -n quant python=3.12
conda activate quant
python -m pip install -r requirements.txt
jupyter lab
```

Run the notebooks in numerical order from `01_market_data.ipynb` through `05_robustness_checks.ipynb`.

## Project structure

```text
notebooks/  # Research workflow
data/       # Downloaded, intermediate, and final data outputs
figures/    # Generated charts
```

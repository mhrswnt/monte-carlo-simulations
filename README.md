# Monte Carlo Simulations for Portfolio Risk

A Jupyter notebook that uses Monte Carlo simulation and historical market data (via Yahoo Finance) to explore
risk and portfolio construction for Indian equities (NSE).

## What's inside

All of the work lives in [`monte_carlo_simulations.ipynb`](monte_carlo_simulations.ipynb), split into sections:

| Section | What it does |
| --- | --- |
| **Monte Carlo VaR** | Fits a normal distribution to one year of daily returns for a stock (default `TCS.NS`), simulates 10,000 one-day outcomes and reports the 95% Value at Risk. |
| **Correlation** | Computes annualised mean, volatility, variance, covariance and correlation matrices from log returns for groups of stocks (IT: INFY / HCLTECH / WIPRO; Tata Steel / Reliance). |
| **Markowitz** | Generates 10,000 random portfolios (Dirichlet-sampled weights) across 7 stocks, plots the efficient frontier and picks the maximum Sharpe ratio portfolio. |
| **Rebalancing** | Compares current holdings against target weights and lists the buy/sell adjustments needed once a deviation threshold is breached. |
| **Non-financial risk** | Simulates synthetic scores for operational, regulatory, ESG, technology, political, reputation and management risk, normalises them to 0-100 and combines them with weights. |
| **Nifty 50 annual returns** | Plots calendar-year returns of the Nifty 50 (`^NSEI`) since 2007 and the mean annual return. |

## Getting started

```bash
git clone https://github.com/mhrswnt/monte-carlo-simulations.git
cd monte-carlo-simulations

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

jupyter lab                      # or: jupyter notebook
```

Then open `monte_carlo_simulations.ipynb` and run the cells top to bottom.

Python 3.10+ is recommended (the notebook was developed on 3.11).

## Configuration

Parameters are plain variables at the top of each section, so change them in the notebook:

- `ticker`, `confidence_level`, `num_simulations`, `time_horizon` in the VaR section
- `tickers`, `year_backs`, `risk_free_rate`, `num_portfolios` in the Markowitz section
- `target_allocation`, `current_portfolio`, `threshold` in the Rebalancing section

Any Yahoo Finance ticker works (NSE stocks use the `.NS` suffix).

## Notes and limitations

- Market data is downloaded live from Yahoo Finance with [`yfinance`](https://github.com/ranaroussi/yfinance), so
  you need an internet connection and results change with the date you run it.
- Simulations are not seeded, so VaR and optimal weights vary slightly between runs.
- The VaR model assumes daily returns are normally distributed and i.i.d., which understates tail risk in real
  markets.
- The Markowitz section uses random sampling rather than a solver, so the "optimal" portfolio is an approximation.
- The non-financial risk section uses randomly generated, illustrative data only.

## Disclaimer

This project is for learning and experimentation. It is not financial advice.

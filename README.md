# Portfolio Risk Analysis: Volatility, Correlation and Value at Risk

A Python project measuring the risk of a 5-stock portfolio (NVDA, META, AAPL, MSFT, JPM) using daily price data from 2021 onwards.

## What it does

1. **Volatility** – annualised standard deviation of daily returns for each stock and for the portfolio
2. **Correlation** – heatmap of how the stocks move together, and how much risk diversification removes
3. **Value at Risk (VaR)** – 95% one-day VaR, calculated two ways:
   - Historical VaR (from the actual distribution of past returns)
   - Parametric VaR (assuming normally distributed returns)
4. **Backtesting** – a rolling 250-day VaR tested against each following day, counting breaches against the expected 5%
5. **Expected Shortfall (ES)** – the average loss on the worst 5% of days, plus the 97.5% ES used under the Basel rules

## Results

Equal-weighted portfolio, daily data from 4 Jan 2021 to 12 Nov 2026 (Expected Shortfall rows from a re-run on 13 Nov).

| Measure | Value |
|---|---|
| Portfolio annual volatility | 25.78% |
| Volatility removed by diversification | 8.83 percentage points (from 34.61% to 25.78%) |
| 95% 1-day Historical VaR (on £10,000) | £263 (2.63%) |
| 95% 1-day Parametric VaR (on £10,000) | £256 (2.56%) |
| Backtest breach rate (expected 5%) | 5.6% |
| 95% 1-day Historical Expected Shortfall | £360 (3.60%) |
| 97.5% 1-day Historical Expected Shortfall | £433 (4.33%) |

**Key findings**

- Diversification removed about a quarter of the risk, even though four of the five stocks are large US tech companies that tend to move together.
- Parametric VaR came out lower than historical VaR, consistent with real returns having fatter tails than a normal distribution.
- The backtest breach rate of 5.6% is close to the expected 5%, so the model is broadly reliable, but it slightly underestimates risk.
- On the worst 5% of days, the average loss (Expected Shortfall) was £360, about 1.4 times the £263 VaR. VaR on its own hides how bad the bad days are.

## Limitations

- Historical VaR assumes the past is representative of the future
- Normal VaR underestimates extreme losses because real returns have fat tails
- Correlations tend to rise during market crises, reducing diversification when it matters most

## How to run

Open `Portfolio_Risk_VaR.ipynb` in Google Colab and select **Runtime → Run all**.

Built with Python, pandas, NumPy, SciPy, matplotlib and yfinance.

# SQL Stock Market Analytics Pipeline

A SQL-driven analysis of 5 years (2021–2025) of daily price data across 12 stocks spanning Technology, Energy, Consumer Staples, and Financials, built with Python, SQLite, and pandas.

## Pipeline

Pulled OHLCV data via yfinance, reshaped from wide to long format, and loaded into a normalized two-table SQLite schema (prices, stocks) to avoid data redundancy. Sector and company metadata lives in one place, not duplicated across thousands of price rows.

## Key Findings
- AAPL showed bullish momentum (20-day MA above 50-day MA) on 720 of ~1,255 trading days (~57%), computed entirely in SQL using window functions, replicating the Golden Cross signal from my Trading Backtester project without leaving the database layer.
- META was the most volatile stock in the basket (2.73 std dev of daily returns), nearly 3x KO, the least volatile (0.99). Consumer staples clustered at the bottom, tech and communication names at the top.
- Technology led all sectors in 2023 with a 0.257% average daily return, over 3x Financials. But, also carried the highest sector-level volatility (2.06 vs. Financials' 1.65), a real risk/reward tradeoff visible directly in the data.
- These sector-level patterns independently corroborate the correlation clusters found in the "NetworkX-based stock correlation" phase of my Backtester project, despite using a completely different methodology.
## SQL Techniques Used
- LAG() for daily returns
- Rolling AVG() with frame clauses for moving averages
- ROW_NUMBER() for per-group extremes
- Hand-built standard deviation via nested subqueries (SQLite has no native STDDEV)
- Multi-table JOINs for sector-level aggregation

### Tech Stack
Python, SQLite, pandas, yfinance, matplotlib

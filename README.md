# Cointegration-Based Statistical Arbitrage (Pairs and Triplets Trading)

This project explores **statistical arbitrage via cointegration-based pairs trading**, focusing on whether apparent mean-reverting relationships actually translate into **tradable edge after realistic constraints**.

Rather than assuming cointegration automatically implies profitability, the goal here is to **stress-test the full pipeline** — from statistical tests to signal construction, execution logic, and risk-adjusted performance.

---

## Project Objectives

- Identify cointegrated asset pairs using **Engle–Granger** and **Johansen** tests  
- Estimate mean-reversion speed via **half-life calculations**
- Construct trading signals based on **z-scored spreads**
- Backtest multiple strategy variants with realistic assumptions
- Evaluate performance using **Sharpe Ratio, drawdowns, and volatility targeting**
- Explicitly study *where intuition breaks down*

---

## Data

- **Universe**: Equity pairs (5 years of daily price data) in Indian Automobile Industry.
- **Frequency**: Daily
- **Source**: Yahoo Finance (via `yfinance`)
- **Equities**: 
* Maruti Suzuki India Limited
* Mahindra & Mahindra
* Tata Motors
* Bajaj Auto
* Hero MotoCorp
* TVS MotorCompany
* Eicher Motors
* Ashok Leyland

---

## Methodology Overview

### 1. Cointegration Testing

- **Engle–Granger test**  
  - Quick pairwise screening
- **Johansen test**
  - Multivariate cointegration validation
  - Eigenvalue-based rank selection
  - Cointegration vectors extracted and normalized

> Key takeaway:  
> *Statistical cointegration ≠ economically useful mean reversion.*

---

## Results (so far)

So far I have only implemented statistical analysis using static beta. 

Based on Engle-Granger there are 4 co-integrated pairs:
* Ashok Leyland, Eicher Motors
* Ashok Leyland, Maruti Suzuki India Limited
* Eicher Motors, Maruti Suzuki India Limited  
* Maruti Suzuki India Limited, TVS MotorCompany

At a daily frequency the half-life of these pairs indicated that it is not tradable. 
Half lives:
* Ashok Leyland, Eicher Motors -> 5927.07 days
* Ashok Leyland, Maruti Suzuki India Limited -> 12000.85 days
* Eicher Motors, Maruti Suzuki India Limited -> 23848.02 days
* Maruti Suzuki India Limited, TVS MotorCompany -> Neg => Spread is not mean reverting.

Based on intuition, there is 1 triplet:
* Ashok Leyland, Eicher Motors, Maruti Suzuki India Limited

Half-life obtained from Johannsen test: 22.43 days. 

The cumulative PnL using this triplet looks like: 
<img width="1189" height="690" alt="image" src="https://github.com/user-attachments/assets/672e7bc4-f2ab-4776-9be7-2dc86849da12" />

---

## Future Plans
Will test the same with rolling hedge ratios, regime filters etc. 

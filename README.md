# Advanced Portfolio Construction: Risk-Based Allocation & The Markowitz Frontier

## 📌 Project Overview (Week 3)
In this phase of the research, we transition from **individual stock selection** to **systematic portfolio construction**. Leveraging a 50-asset universe of S&P 500 constituents, we evaluate the performance of three distinct allocation regimes: **Equal-Weight (1/N)**, **Risk Parity (Inverse Volatility)**, and **Mean-Variance Optimization (MVO)**.

## 🛠️ Methodology & Data Integrity
- **Universe**: 50 High-Liquidity U.S. Equities + S&P 500 Benchmark (`^GSPC`).
- **Time Horizon**: 2016 – 2026 (10-year lookback).
- **Data Cleaning**: Implemented a robust ingestion pipeline to handle Multi-Index data structures and ticker-level anomalies (e.g., unit-consistency for `BRK-B` and ticker corrections for `ABBV`).
- **Returns**: Logarithmic returns used for covariance stability and time-additivity.

---

## 🔍 Phase 1: Risk Diagnostics & Topology
Before allocating capital, we diagnosed the structural risk of the universe using **Hierarchical Clustering**.



### **Key Diagnostic Metrics (Equal-Weight Baseline)**
- **Portfolio Beta**: **0.9577** (Indicates a slightly defensive posture relative to the S&P 500).
- **Diversification Ratio (DR)**: **1.6375** (Measures the risk reduction from non-perfect correlation).
- **Insight**: The clustermap reveals intense "risk blocks" in Mega-cap Tech and Financials, suggesting that a naive 1/N allocation may be over-exposed to specific sector shocks.

---

## 📈 Phase 2: Heuristic Allocation vs. Risk Parity
We compared the standard $1/N$ approach against a **Simple Risk Parity (Inverse Volatility)** approximation where weights are defined as $w_i \propto 1/\sigma_i$.

### **Performance Summary (2016-2026)**

| Strategy | Ann. Return | Ann. Volatility | Sharpe Ratio | Max Drawdown |
| :--- | :--- | :--- | :--- | :--- |
| **S&P 500 Index** | 12.28% | 15.53% | 0.79 | -24.77% |
| **Equal-Weight (1/N)** | 22.04% | 16.94% | 1.30 | -23.36% |
| **Risk Parity (1/Vol)** | **20.57%** | **14.67%** | **1.40** | **-19.60%** |

**Observation**: Risk Parity successfully reduced portfolio volatility by **~230 bps** compared to Equal-Weight, leading to a superior risk-adjusted return (Sharpe Ratio of 1.40).

---

## 🎯 Phase 3: The Markowitz Efficient Frontier
The final stage involves solving the quadratic programming problem to identify the **Pareto Optimal** boundary.



### **Optimization Results**
- **Monte Carlo Simulation**: 5,000 random portfolios generated to define the feasible set (The Cloud).
- **Tangency Portfolio**: Identified the weights that maximize the Sharpe Ratio in-sample.
- **Minimum Variance Portfolio (MVP)**: Identified the allocation that minimizes total portfolio risk regardless of return.

*Note: MVO results are presented as an in-sample theoretical upper bound to highlight the potential for optimization beyond heuristic models.*

## 📂 Repository Structure
- `Week3_Risk_Parity_and_Markowitz_Optimization.ipynb`: Full Python implementation.
- `requirements.txt`: Environment dependencies.
- `README.md`: Research summary and results.

## 🚀 How to Reproduce
1. Clone the repo: `git clone <repo-url>`
2. Install dependencies: `pip install yfinance pandas numpy matplotlib seaborn scipy`
3. Run the Jupyter Notebook to generate the plots and metrics.

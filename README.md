# Regime-Switching Portfolio Strategy using Hidden Markov Models

## Overview
This project develops a **regime-aware portfolio allocation strategy** using a Hidden Markov Model (HMM) to identify latent market regimes from financial market data.

Market regimes often exhibit different correlation structures and risk dynamics. By detecting these regimes and adjusting portfolio allocations accordingly, the strategy aims to improve risk-adjusted returns compared to traditional static allocations.

The strategy is evaluated through historical backtesting and compared against common benchmark portfolios.

---

## Methodology

### 1. Data

The analysis uses historical asset price data for a diversified set of ETFs representing different asset classes:

- **SPY** – US equities  
- **TLT** – Long-term US Treasury bonds  
- **GLD** – Gold  
- **BIL** – Treasury bills (cash proxy)

Daily returns are computed from historical price data and used to construct rolling feature matrices.

---

### 2. Feature Engineering

To capture systemic market behavior, correlation-based features are extracted from rolling windows of asset returns.

**Average Pairwise Correlation**

Measures how strongly assets move together.  
High values often indicate market stress.

**Largest Eigenvalue of the Correlation Matrix**

Represents the strength of the dominant market factor.  
This value tends to spike during crises when asset movements become highly synchronized.

These features serve as inputs to the Hidden Markov Model.

---

### 3. Hidden Markov Model (HMM)

A **Gaussian Hidden Markov Model** is used to infer latent market regimes.

The model learns hidden states that explain changes in the observed feature distributions.

Each regime represents a distinct market environment such as:

- Low correlation / stable markets
- Moderate correlation / transitional markets
- High correlation / crisis periods

The trained model assigns a **regime label to each time step**.

---

### 4. Regime-Based Portfolio Allocation

Each detected regime is mapped to a predefined portfolio allocation across the asset universe.

Example allocations:

| Regime | SPY | TLT | GLD | BIL |
|------|------|------|------|------|
| Calm markets | 60% | 20% | 10% | 10% |
| Moderate stress | 40% | 40% | 10% | 10% |
| Crisis | 20% | 50% | 20% | 10% |

The portfolio dynamically adjusts allocations based on the current regime.

---

### 5. Backtesting

The strategy is evaluated through historical simulation.

Key elements of the backtest include:

- Dynamic portfolio rebalancing
- Turnover calculation
- Transaction cost modeling
- Benchmark comparisons

Benchmarks include:

- **SPY Buy-and-Hold**
- **Equal Weight Portfolio**
- **60/40 Stock-Bond Portfolio**

---

## Performance Evaluation

Strategy performance is evaluated using several standard metrics:

- Annualized Return
- Volatility
- Sharpe Ratio
- Maximum Drawdown
- Turnover

These metrics allow comparison between the regime-switching strategy and benchmark portfolios.

---

## Key Results

The project demonstrates that:

- Market regimes can be effectively identified using correlation-based features.
- Regime-aware allocation can adjust risk exposure during periods of market stress.
- Transaction costs and turnover significantly influence real-world strategy performance.

---

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- scikit-learn
- hmmlearn

---

## Author

David Ogolo  


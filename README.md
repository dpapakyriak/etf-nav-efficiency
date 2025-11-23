# ETF Pricing Efficiency, Mispricing Dynamics, and NAV Behavior  
### A Quantitative Analysis of ETF Premiums, Rolling Z-Scores, Systemic Stress, and NAV Lag

This project investigates the pricing efficiency of Exchange-Traded Funds (ETFs) by analyzing how their traded market prices deviate from official Net Asset Values (NAVs). Using a multi-asset ETF universe covering US equities, sectors, international markets, emerging markets, fixed income, and commodities, the study evaluates:

- daily price-to-NAV premiums and discounts  
- 30-day rolling Z-scores of mispricing  
- cross-sectional mispricing patterns  
- a system-wide ETF Stress Index  
- NAV return construction and NAV lag behavior  

The objective is to understand which ETF categories are structurally efficient, which suffer from NAV staleness or illiquid constituents, and how arbitrage pressures evolve under market stress.

---

## Motivation

ETFs are designed to track the value of a portfolio of underlying assets. In practice, ETF prices can deviate from NAV due to:

- liquidity imbalances  
- stale or model-based NAV calculations  
- time-zone differences  
- creation/redemption frictions  
- underlying market illiquidity  

These deviations become particularly important during periods of market stress, when arbitrage mechanisms may break down and ETFs may begin to lead (rather than follow) their underlying assets.

This project aims to quantify such effects using data-driven, statistically grounded methods.

---

## Dataset

The analysis uses daily data (2017–present) for:

- **ETF Price (`PX_LAST`)**  
- **ETF NAV (`FUND_NET_ASSET_VAL`)**  
- **Trading Volume**  
- Optional: underlying index prices for price-discovery extensions  

Data are from Bloomberg terminal, where each sheet corresponds to an ETF.

---

## Methodology

### 1. **Premium Calculation**

Premium measures deviation of ETF price from NAV:
\[
premium_t = \frac{Price_t - NAV_t}{NAV_t}
\]

### 2. **Rolling 30-Day Z-Score**

Z-score contextualizes premium relative to recent history:
\[
Z_t = \frac{premium_t - \mu_{30}}{\sigma_{30}}
\]

High |Z| indicates abnormal mispricing, typically driven by liquidity or NAV timing issues.

### 3. **Cross-Sectional Mispricing Metrics**

For each ETF:
- mean premium  
- mean absolute premium  
- mean Z-score  
- mean absolute Z-score  

These reveal structural efficiency or inefficiency across asset classes.

### 4. **ETF Stress Index**

System-wide arbitrage pressure:
\[
StressIndex_t = \frac{1}{N}\sum_{i=1}^N |Z_{i,t}|
\]

Captures broad dislocations across ETF markets.

### 5. **NAV Lag Test**

We test whether ETF returns lead NAV returns:
\[
LagScore = corr(r^{ETF}_t, r^{NAV}_{t+1}) - corr(r^{ETF}_t, r^{NAV}_t)
\]

- **Positive LagScore** → NAV lags; ETF performs price discovery  
- **Negative LagScore** → NAV is synchronous or leading  

This detects stale NAV behavior, especially relevant in fixed income and commodities.

---

## Key Insights

- **US equity ETFs** show minimal mispricing and near-zero lag → highly efficient.  
- **Fixed income ETFs**, especially high-yield and investment-grade corporates, show persistent mispricing and NAV lag driven by illiquid bond markets.  
- **Emerging market ETFs** exhibit structural deviations due to time-zone differences and stale NAV inputs.  
- **Commodity ETFs** show settlement-driven anomalies, especially in silver and oil.  
- The **Stress Index** spikes during known risk events, confirming ETF mispricing as a reliable stress indicator.  
- NAV lag behavior reveals when ETFs become primary price discovery venues rather than passive trackers.

---

## Visualizations

The notebook includes charts for:

- rolling Z-scores across ETFs  
- mean premium and mean absolute premium  
- mean Z-score patterns  
- system-wide Stress Index  
- NAV lag scores per ETF  

These provide intuitive comparisons across categories.

---

## Technologies

- **Python**: pandas, numpy, matplotlib  
- **Data Source**: Bloomberg Terminal
- **Environment**: Jupyter Notebook  

---

## Extensions

Potential research extensions include:

- ETF vs index price discovery (lead–lag with benchmark indices)  
- intraday NAV proxy estimation  
- liquidity-adjusted mispricing models  
- regime-switching behavior in Stress Index spikes  

---

## License

This project is released under the MIT License.




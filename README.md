# Data-Driven Identification of Market Regimes Using Unsupervised Learning

**CSD355 Foundations of Data Science, Course Project, Shiv Nadar University**
Mukhil Charles · Saran Prithvick

This project identifies historical market regimes without predefined labels. Daily data for five instruments (SPY, GLD, CL=F, EURUSD=X, ^VIX) from 2010 to 2025 are turned into 20 features (return, 20-day volatility, 20-day momentum and drawdown for each instrument). The features are reduced with Principal Component Analysis (PCA) and clustered with K-Means. The resulting regimes are then characterised, analysed over time, tested for robustness and validated against known market events.

## Key results

- **Two regimes** were selected (Silhouette Score 0.295): a stress regime covering 18.2% of trading days and a stable regime covering the rest.
- **The stress regime** has higher volatility in all five instruments, falling equity and oil prices and rising VIX.
- **Event validation:** 51–96% of trading days in seven well-known market crises fall in the stress regime, compared with its 18.2% base rate.
- **Cross-asset behaviour:** under stress, the correlation between equity and oil returns rises (0.21 → 0.31), while gold becomes uncorrelated with equities.
- **Robustness:** a 15-day lookback window reproduces the regimes (Adjusted Rand Index 0.686, 92.7% of days with the same label).

The full methodology and discussion are in the report in `report/`.

## Repository structure

```
├── FDS_proj.ipynb          # complete analysis notebook (with outputs)
├── requirements.txt        # Python packages used
├── report/                 # final project report (PDF)
├── data/                   # cleaned prices and engineered features
├── results/                # result tables (CSV)
└── figures/                # figures used in the report
```

| Folder | Files |
|---|---|
| `data/` | `cleaned_market_prices.csv`, `market_features_20day.csv`, `features_15day.csv`, `pca_reduced_features.csv` |
| `results/` | `regime_episodes.csv`, `regime_duration_statistics.csv`, `regime_transition_matrix.csv`, `top_stress_episodes.csv`, `event_validation.csv`, `corr_stress.csv`, `corr_stable.csv`, `regimes_15day.csv`, `regime_comparison.csv`, `robustness_metrics.csv` |
| `figures/` | `fig_pca_variance.png`, `fig_regime_correlations.png`, `fig_regime_timeline.png`, `fig_durations.png` |

## How to run

The notebook was written for **Google Colab**.

1. Open `FDS_proj.ipynb` in Google Colab (File → Upload notebook, or open it from this GitHub repository).
2. Select **Runtime → Run all**. The notebook installs `yfinance`, downloads the data from Yahoo Finance and runs the full pipeline in a few minutes.
3. Output files are written to `/content/`.

To run locally instead, install the packages with `pip install -r requirements.txt` and change the `/content/` paths in the notebook to a local folder.

**Note:** Yahoo Finance occasionally revises historical prices, so a fresh download may give results that differ very slightly from those in the report.

## Data

All data are publicly available from Yahoo Finance and retrieved with the `yfinance` library:

| Ticker | Instrument |
|---|---|
| SPY | SPDR S&P 500 ETF (US equities) |
| GLD | SPDR Gold Shares (gold) |
| CL=F | WTI crude oil futures |
| EURUSD=X | Euro–US dollar exchange rate |
| ^VIX | Cboe Volatility Index (implied volatility) |

Period: 1 January 2010 to 31 December 2025. The negative crude-oil price of −37.63 on 20 April 2020 was removed during preprocessing, because percentage-based features are undefined for negative prices.

# Brent-WTI Crude Oil Spread Analysis

## Research Question

To what extent are weekly movements in the Brent-WTI spread associated with U.S. physical oil market fundamentals -- such as Cushing stocks, refinery utilization, and crude imports -- from 2020 to 2026?

## Repository Structure

```
├── README.md                          # This file
├── requirements.txt                   # Python requirements
├── blog.ipynb                         # Main analysis notebook
├── data/
│   ├── raw/
│   │   ├── prices_daily.csv          # Daily Brent and WTI prices
│   │   └── eia_weekly.csv            # Weekly EIA petroleum data
│   └── processed/
│       └── analysis_data.csv         # Merged weekly dataset (generated)
└── output/
    └── figures/                       # Visualization outputs (generated)
```

## Data Sources

All of the data used are taken from the U.S. Energy Information Administration (EIA):

**Price Data:**
- Daily Brent and WTI crude oil spot prices
- Period: January 2020 - April 2026

**Physical Market Data (Weekly):**
- Cushing, OK crude oil stocks: EIA series W_EPC0_SAX_YCUOK_MBBL
- U.S. refinery capacity utilization: EIA series WPULEUS3
- U.S. crude oil imports: EIA series WCRIMUS2
- Period: January 2020 - April 2026 (328 weekly observations)

## Requirements

- Python 3.9 or higher
- Packages listed in the `requirements.txt`

## Installation

```bash
pip install -r requirements.txt
```

## Replication Instructions

### Step 1: Clone Repository

```bash
git clone https://github.com/HShikarov/brent-wti-spread-analysis.git
cd brent-wti-spread-analysis
```

### Step 2: Install Requirements

```bash
pip install -r requirements.txt
```

### Step 3: Run Analysis in Jupyter

**Where:**
- Select "Kernel" → "Restart & Run All"
- All cells will execute in chronological order
- Expected runtime is about 30 seconds

### Step 4: View Results

The analysis generates:
1. Cleaned weekly dataset (`data/processed/analysis_data.csv`)
2. OLS regression results (displayed in the notebook)
3. Five visualizations in `output/figures/`:
   - 01_prices_over_time.png
   - 02_spread_over_time.png
   - 03_stocks_scatter.png
   - 04_coefficients.png
   - 05_refinery_spread.png

## Methodology

**Specification:**
```
Spread_t = β₀ + β₁(Cushing_Stocks_t) + β₂(Refinery_Util_t) + 
           β₃(Crude_Imports_t) + β₄(Spread_t-1) + ε_t
```

Taking that into account:
- **Spread** = Brent price - WTI price ($ per barrel)
- **Cushing_Stocks** = Cushing, OK crude stocks (in million barrels)
- **Refinery_Util** = U.S. refinery capacity utilization (in %)
- **Crude_Imports** = U.S. crude oil imports (in thousand barrels per day)
- **Spread_t-1** = One-week lagged spread (the persistence parameter)

**Estimation Method:** OLS regression

## Key Findings
The analysis reveals that the Brent-WTI spread exhibits strong persistence over time, with physical market fundamentals playing a multifaceted role in spread dynamics. The lagged spread variable shows significant persistence, suggesting that price differentials adjust gradually rather than instantaneously.

## Limitations:
- Observational data: associations, not causal inference
- Omitted variables, including but not limited to: geopolitical events, infrastructure-related constraints
- Relationships may vary across different market fundamentals/variables

## Acknowledgments:
Data: U.S. Energy Information Administration  (EIA)
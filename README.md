# Germany-grid-stability-simulator
Can renewables handle peak demand? This project simulates Germany's grid at hourly resolution over 5 years, 50,295 hours of data analyzed. Hourly simulation grid under 50%, 80%, and 100% renewable scenarios. Finds that 1,400 GWh of storage is needed for 80% renewables 700x current capacity.

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-red.svg)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📊 Project Overview

Critics argue that renewable energy cannot provide reliable power. This project provides a **data-driven answer** by simulating the German electricity grid under different renewable penetration scenarios using **5+ years of hourly data** (50,295 hours).

**Key Question:** How much storage is needed to make an 80% or 100% renewable grid reliable?

**The Answer:** Germany would need **1,400 GWh of storage** (700x current capacity) to reach 80% renewables reliably.

## 🎯 Key Findings

| Scenario | Renewable Share | Annual Shortfall Hours | Storage Needed (7-day dark doldrum) |
|:---|:---|:---|:---|
| **Current (2015-2020)** | 29% (solar+wind) | 0 hours | 0 GWh |
| **80% Renewables** | ~78% | 15,143 hours (63% of year) | **1,400 GWh** |
| **100% Renewables** | ~95% | 17,543 hours (73% of year) | 1,400+ GWh |

### Key Insights

1. **Germany's current grid (2015-2020) never produced excess solar+wind power** — fossil and nuclear always covered the gap between demand and renewables.

2. **At 80% renewables, the grid would face shortfalls 63% of the year without storage.** The binding constraint is not daily or weekly variability but **multi-week "dark doldrum" periods** (low wind + low solar) in winter.

3. **Reliable 80% renewables requires approximately 1,400 GWh of storage** — 700x Germany's current battery capacity (~2 GWh).

4. **Policy implication:** Reaching 80% renewables is technically feasible but requires **coordinated storage deployment** before or alongside additional solar/wind capacity, not after.

---

## 📈 Key Visualizations

### 1. Residual Load Analysis (Sample Week)
*Residual load = demand - (solar + wind) — must be met by conventional power or storage*

![Residual Load Analysis](images/residual_load_sample.png)

### 2. Scenario Comparison
*Shortfall hours increase dramatically as renewables scale beyond 50%*

![Scenario Comparison](images/scenario_comparison.png)

### 3. Dark Doldrum Period
*The worst 7-day period with lowest renewable generation (typically winter)*

![Dark Doldrum Analysis](images/dark_doldrum_analysis.png)

---

## 🛠️ Methodology

### Tasks Completed

| Task | Description | Status |
|:---|:---|:---|
| **Time Series Simulation** | Modeled grid operations at hourly resolution over 5+ years | ✅ |
| **Risk Analysis** | Calculated probability of shortfalls under different scenarios (63% at 80% renewables) | ✅ |
| **Optimization** | Determined minimal storage required for reliable renewables (1,400 GWh) | ✅ |
| **Scenario Modeling** | Simulated 50%, 80%, and 100% renewable penetration | ✅ |
| **Extreme Event Analysis** | Identified "dark doldrum" periods (low wind + low solar) | ✅ |

### Data Sources

| Data Type | Source | Time Period | Resolution |
|:---|:---|:---|:---|
| Hourly electricity demand | Open Power System Data | 2015-2020 | Hourly |
| Hourly solar generation | Open Power System Data | 2015-2020 | Hourly |
| Hourly wind generation | Open Power System Data | 2015-2020 | Hourly |

**Total observations:** 50,295 hours

### Analytical Approach

| Step | Method | What It Does |
|:---|:---|:---|
| 1 | **Residual load calculation** | `Residual = Demand - (Solar + Wind)` |
| 2 | **Renewable penetration scenarios** | Scale solar/wind to 50%, 80%, 100% of demand |
| 3 | **Shortfall identification** | Count hours where residual exceeds conventional capacity |
| 4 | **Dark doldrum detection** | Find 7-day periods with lowest renewable generation |
| 5 | **Storage requirement** | Calculate energy needed to cover worst shortfall period |

### Scenarios Simulated

| Scenario | Solar Multiplier | Wind Multiplier | Conventional Capacity |
|:---|:---|:---|:---|
| Current (2015-2020) | 1.0x | 1.0x | 85 GW |
| 80% Renewables | 4.0x | 3.0x | 25 GW |
| 100% Renewables | 6.0x | 5.0x | 0 GW |

---

## 💡 Business & Policy Implications

| Stakeholder | Implication | Actionable Recommendation |
|:---|:---|:---|
| **Policymakers** | Storage is the binding constraint, not generation | Deploy storage *before* reaching 80% renewables |
| **Grid operators** | Dark doldrum periods drive storage needs | Plan for multi-week storage, not just daily cycling |
| **Investors** | 1,400 GWh storage opportunity | Target winter-resilient storage technologies |
| **Energy companies** | Current 2 GWh is insufficient | Scale storage 700x |

---

## 🚀 How to Reproduce This Analysis

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn
Steps
Clone the repository

bash
git clone https://github.com/yourusername/Germany-grid-stability-simulator.git
cd grid-stability-simulator
Launch Jupyter Notebook

bash
jupyter notebook
Open and run code/Germany_grid_stability_simulator.ipynb

Quick Start Code
python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load data
df = pd.read_csv('data/time_series_60min_singleindex.csv')

# Calculate residual load
df['residual_mw'] = df['load_mw'] - (df['solar_mw'] + df['wind_mw'])

# Calculate renewable share
renewable_share = (df['solar_mw'].sum() + df['wind_mw'].sum()) / df['load_mw'].sum() * 100
print(f"Renewable share: {renewable_share:.1f}%")

📊 Results Summary

GRID STABILITY SIMULATION - EXECUTIVE SUMMARY
============================================================

DATA OVERVIEW
-------------
Total hours analyzed: 50,295
Time period: 2015-2020
Current renewable share (solar+wind): 29.1%

TASKS COMPLETED
---------------
✅ Time series simulation — hourly resolution over 5+ years
✅ Risk analysis — 63% probability of shortfall at 80% renewables
✅ Optimization — 1,400 GWh storage needed
✅ Scenario modeling — 50%, 80%, 100% scenarios analyzed
✅ Extreme event analysis — dark doldrum periods identified

SCENARIO RESULTS
----------------
80% Renewables Scenario:
   - Renewable share: ~78%
   - Annual shortfall hours: 15,143 (63% of year)
   - Storage needed (7-day dark doldrum): 1,400 GWh

100% Renewables Scenario:
   - Renewable share: ~95%
   - Annual shortfall hours: 17,543 (73% of year)

POLICY RECOMMENDATION
---------------------
Germany can reach 80% renewables, but requires 1,400 GWh of storage
(current capacity: 2 GWh). Storage deployment must precede or accompany
additional solar/wind capacity, not follow it.

📝 Limitations
Limitation	Explanation	Mitigation
No transmission constraints	Assumes perfect grid	Conservative on storage needs
Perfect forecasting assumed	No uncertainty	Actual storage needs higher
Excludes biomass/hydro	Understates current renewable share	Focuses on variable renewables only
2015-2020 data only	Missing recent changes	Captures full weather variability

🔮 Future Work
Direction	Method	Expected Insight
Add transmission constraints	Power flow modeling	Identify regional storage needs
Include wind-solar correlation	Multivariate analysis	Optimize renewable mix
Forecast to 2030-2040	Climate/load projections	Long-term storage requirements
Compare multiple countries	Cross-national analysis	Export best practices

📚 Data Sources
Source	Data	License
Open Power System Data	Hourly load, solar, wind (Germany 2015-2020)	CC BY 4.0

👤 About the Author
Name: Fanuel Bayeh

Data Analyst / Energy Researcher

Interests: Energy Transition, Grid stability, renewable integration, energy storage

📧 fanbayeh@gmail.com

🐙 github.com/08fbyte

Why This Project?
This project demonstrates:

Energy domain expertise — Understanding of grid operations, renewable integration, storage

Technical skills — Python, pandas, time series simulation, scenario analysis

Policy acumen — Actionable recommendations for 80% renewable targets

Methodological rigor — 5+ years of hourly data, dark doldrum detection, 5 completed analytical tasks

📄 License
This project is licensed under the MIT License.

🙏 Acknowledgments
Data provided by Open Power System Data (OPSD)

ENTSO-E for original transparency data

German Federal Network Agency (Bundesnetzagentur)

📧 Contact
Questions or collaboration? Reach out:

Email: fanbayeh@gmail.com
GitHub: github.com/08fbyte

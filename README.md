# ☀️ Solar PV System Performance Analysis

> End-to-end performance monitoring and diagnostic framework for three rooftop PV systems at Andre Agassi Preparatory Academy (Las Vegas, NV), using NREL PVDAQ data to detect inverter faults, shading/soiling, and sensor anomalies.

<p align="left">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="Pandas"/>
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" alt="NumPy"/>
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=flat-square" alt="Matplotlib"/>
  <img src="https://img.shields.io/badge/Seaborn-444876?style=flat-square" alt="Seaborn"/>
  <img src="https://img.shields.io/badge/Plotly-3F4F75?style=flat-square&logo=plotly&logoColor=white" alt="Plotly"/>
  <img src="https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white" alt="Colab"/>
</p>

---

## Problem

Solar PV operators need to detect underperformance quickly — but distinguishing between weather-driven drops and real equipment issues (inverter faults, soiling, sensor failures) is difficult with raw data alone. This project builds an automated diagnostic pipeline that processes sub-hourly generation data from three co-located PV systems, computes performance metrics, flags anomalies, and enables cross-system peer comparison to isolate system-specific faults.

## Data

- **Source**: NREL PVDAQ (PV Data Acquisition) dataset
- **Site**: Andre Agassi Preparatory Academy, Las Vegas, NV
- **Systems analyzed**:
  - System 1276 — 68.48 kW (single inverter)
  - System 1277 — 40.56 kW (single inverter)
  - System 1278 — largest system (dual inverter)
- **Resolution**: 15-minute intervals across full year (2019)
- **Variables**: AC/DC power, current, voltage, POA irradiance, module temperature, ambient temperature, wind speed, inverter error codes, power factor

## Approach

**Data Engineering**
- Ingested and consolidated hundreds of daily CSV files per system from Google Drive
- Standardized column names across three systems with different sensor configurations
- Aggregated dual-inverter data for System 1278 (summed currents/power, averaged voltages)
- Normalized timestamps to 15-minute intervals and handled missing data

**Performance Metrics**
- Calculated **Actual Energy (Wh)** from measured AC power
- Computed **Expected Energy (Wh)** using POA irradiance and system size
- Derived **Performance Ratio (PR)** to normalize performance against available solar resource

**Automated Diagnostic Flagging**
- `flag_ac_zero_under_sun` — zero AC output despite irradiance > 100 W/m² (inverter fault)
- `flag_low_pr_possible_shading_or_soiling` — PR below 60% during high irradiance (> 400 W/m²)
- `flag_inverter_error` — non-zero inverter error codes
- `flag_power_spike` — sudden fluctuations via rolling standard deviation
- `flag_missing_data` — gaps in energy data
- `flag_poa_sensor_issue` — abnormally low irradiance variance (stuck sensor)
- `flag_low_pr_vs_reference` — PR more than 20% below peer system (System 1277 as baseline)

**Peer Comparison**
- Compared daily average PR across all three co-located systems to isolate system-specific issues from site-wide weather effects

## Key Results

| System | Key Finding |
|---|---|
| **System 1276 (68.48 kW)** | 813 instances of zero AC output under sun, 7,100 POA sensor anomalies, 6,666 low-PR intervals during high irradiance — consistent underperformer flagged for inverter/sensor investigation |
| **System 1277 (40.56 kW)** | Most stable system — fewest flags, tightest PR distribution (60–90%), used as peer reference baseline |
| **System 1278 (dual inverter)** | Highest absolute power output but showed intermittent clipping, power spikes, and PR dips unrelated to weather — dual-inverter behavior needs further diagnostics |

**Cross-system insight**: System 1276's underperformance was confirmed as system-specific (not weather-driven) because Systems 1277 and 1278 performed normally on the same days.

## Visualizations

- Time-series plots of irradiance vs. AC power per system
- Performance Ratio trends over the full year
- Scatter plots of POA irradiance vs. AC power (diagnostic)
- Stacked area charts of daily flag counts per system
- Calendar heatmaps showing temporal distribution of anomalies
- Cross-system daily PR comparison
- [Power Bi Dashbaord](https://app.powerbi.com/view?r=eyJrIjoiZTQ1N2RmYzQtZDJmNS00ZDdkLWE4NzItM2Q4MmVlOWU2MmM0IiwidCI6IjMxNGE4NjhkLTc4OWUtNDRhMC1hMTBmLTc1OTNkNjI0MzhiYSJ9&pageName=34a4f6ac2df63348c435)

## How to Run

```bash
# Clone the repo
git clone https://github.com/patilshan/solar-pv-performance-analysis.git
cd solar-pv-performance-analysis

# Install dependencies
pip install pandas numpy matplotlib seaborn plotly jupyter

# Launch the notebook
jupyter notebook Solar_PV_System_Performance_Analysis_Project.ipynb

# Note: Original analysis used Google Colab with Drive-mounted PVDAQ data
```

## Project Structure

```
├── Solar_PV_System_Performance_Analysis_Project.ipynb   # Full analysis notebook
└── README.md
```

## What I Learned

- How to build a scalable diagnostic framework that handles multiple PV systems with different inverter configurations and sensor schemas
- The power of peer-comparison flagging — comparing co-located systems under identical weather conditions is the most reliable way to isolate equipment-specific faults
- That extreme Performance Ratio values often signal data quality issues (sensor noise, low-irradiance denominators) rather than actual system behavior
- Designing flag outputs in a format ready for integration with BI tools like Power BI for operational dashboards

---

<p align="center">
  <a href="https://github.com/patilshan">← Back to profile</a>
</p>

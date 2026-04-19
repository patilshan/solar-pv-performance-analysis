# ☀️ Solar PV System Performance Analysis

> Analyzing real-world photovoltaic output data to uncover degradation patterns, seasonal trends, and actionable maintenance insights for solar installations.

<p align="left">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="Pandas"/>
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=flat-square" alt="Matplotlib"/>
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white" alt="SciPy"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white" alt="Jupyter"/>
</p>

---

## Problem

Solar PV installations degrade over time, but the rate and pattern of degradation vary based on environmental conditions, equipment quality, and maintenance practices. Plant operators need data-driven methods to benchmark system performance, detect underperformance early, and schedule maintenance cost-effectively.

## Approach

- Cleaned and preprocessed time-series generation data from a real PV system
- Performed exploratory data analysis to identify seasonal and diurnal output patterns
- Computed capacity factor and performance ratio metrics to benchmark system health
- Applied time-series decomposition to isolate trend, seasonal, and residual components
- Generated data-driven recommendations for maintenance scheduling

## Key Results

| Metric | Detail |
|---|---|
| **Analysis Type** | Time-series performance benchmarking |
| **Key Techniques** | Capacity-factor modeling, seasonal decomposition, trend analysis |
| **Outcome** | Identified degradation patterns and optimal maintenance windows |

## How to Run

```bash
# Clone the repo
git clone https://github.com/patilshan/solar-pv-performance-analysis.git
cd solar-pv-performance-analysis

# Install dependencies
pip install pandas numpy matplotlib scipy jupyter

# Launch the notebook
jupyter notebook Solar_PV_System_Performance_Analysis_Project.ipynb
```

## Project Structure

```
├── Solar_PV_System_Performance_Analysis_Project.ipynb   # Main analysis notebook
└── README.md
```

## What I Learned

- How to work with real-world energy generation data including handling missing readings and sensor noise
- Applying statistical decomposition techniques to extract meaningful signals from noisy time-series
- Translating analytical findings into actionable maintenance recommendations

---

<p align="center">
  <a href="https://github.com/patilshan">← Back to profile</a>
</p>

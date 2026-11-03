# ⚡ Real-Time Dynamic Pricing for Urban Parking Lots

<div align="center">

[![Summer Analytics 2025](https://img.shields.io/badge/Summer%20Analytics%202025-Capstone%20Project-4A90D9?style=flat-square)](https://www.caciiitg.com/sa/course25/)
[![Pathway](https://img.shields.io/badge/Pathway-Streaming%20Framework-00D4B2?style=flat-square)](https://pathway.com)
[![Bokeh](https://img.shields.io/badge/Bokeh-Live%20Visualization-2B7A78?style=flat-square)](https://bokeh.org)
[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

**Capstone Project — Summer Analytics 2025**
*Hosted by the Consulting & Analytics Club × Pathway*

*A real-time pricing engine simulating 14 urban parking lots over 73 days using Pathway's streaming framework, comparing three models of increasing intelligence — from a simple linear baseline to a Haversine spatial-competitive model with live Bokeh visualization.*

</div>

---

## 📸 Demo Preview

> **TODO:** Add a screenshot of the live Bokeh streaming chart showing multi-lot price evolution here.
> Suggested file: `assets/pricing-bokeh-live.png`
>
> Capture: Live Bokeh plot with 14 lot price lines updating as the Pathway stream processes data rows.

---

## 🧩 Problem Overview

Urban parking is a high-demand, limited-resource service. Static pricing leads to poor utilization: either under-use during off-peak hours or over-congestion during peak times. This project simulates a real-time, data-driven dynamic pricing engine that ingests occupancy and demand signals to continuously recalculate fair, efficient prices.

We model and compare **three levels of pricing intelligence**:

1. **Model 1:** Baseline Linear Model
2. **Model 2:** Demand-Based Pricing
3. **Model 3:** Competitive Pricing with Spatial Proximity (Haversine)

---

## 📊 Dataset Summary

| Property | Value |
|---|---|
| **Duration** | 73 days |
| **Frequency** | Every 30 minutes (08:00 AM – 04:30 PM) |
| **Time Steps / Day** | 18 |
| **Parking Lots** | 14 lots |
| **Total Records** | ~18,000 – 20,000 |

Each record includes: Location (Lat/Long), Capacity, Occupancy, Queue Length, Vehicle Type (car / bike / truck), Nearby Traffic Condition, Special Day Indicator.

---

## ⚙️ Pricing Model Descriptions

### Model 1 — Linear Pricing

```
Price(t+1) = Price(t) + α × (Occupancy / Capacity)
```
- Starts at $10, bounded between $5 and $20.
- Smooth, continuous price changes based solely on fill rate.

### Model 2 — Demand-Based Pricing

```
Demand = α·(Occupancy/Capacity) + β·QueueLength − γ·Traffic
       + δ·IsSpecialDay + ε·VehicleTypeWeight

Price(t) = BasePrice × (1 + λ × NormalizedDemand)
```
Weights are manually tuned for interpretability.

### Model 3 — Competitive Pricing with Haversine Proximity

Enhances Model 2 by incorporating neighboring lot prices within a **0.5 km radius** using the Haversine formula. Adjusts dynamically based on competitor pricing to prevent localized congestion.

---

## 🌊 Real-Time Simulation with Pathway

```python
# Data streamed row-by-row through Pathway
mode = "streaming"
autocommit_duration_ms = 300

# Features processed live with @pw.udf
# Output piped to CSV and Bokeh dashboard
```

- CSV dataset ingested in streaming mode — Pathway replays records as if arriving live.
- Pathway UDFs compute pricing features and model outputs per time step.
- Results emitted to `realtime_output.csv` and a live Bokeh plot.

---

## 📈 Live Visualization with Bokeh

- **Live plot** of predicted prices per lot, refreshing as data flows through Pathway.
- Multi-line chart showing all 14 lots simultaneously with hover tooltips.
- Complements the Pathway progress dashboard.

---

## 📁 Files in This Project

| File | Description |
|---|---|
| `Capstone_Project_Updated.ipynb` | Main notebook — all three models, Pathway streaming, Bokeh visualization |
| `dataset.csv` | Input dataset (~18,000–20,000 records across 14 lots, 73 days) |
| `realtime_output.csv` | Live pricing output generated during streaming simulation |
| `README.md` | Documentation |

---

## 🚀 How to Run

### On Google Colab (Recommended)

1. Open `Capstone_Project_Updated.ipynb` in [Google Colab](https://colab.research.google.com).
2. Upload `dataset.csv` to the Colab session.
3. Install dependencies in the first cell:
   ```bash
   pip install -U pathway bokeh pandas numpy matplotlib
   ```
4. Run all cells top to bottom.
5. View:
   - Pathway progress dashboard in the Colab output panel.
   - Live Bokeh plot of pricing evolution.
6. Export or tune model weights as needed in the configuration cell.

### Locally

```bash
git clone https://github.com/aditweb13/Capston-Project.git
cd Capston-Project

pip install -U pathway bokeh pandas numpy matplotlib jupyter

jupyter notebook Capstone_Project_Updated.ipynb
```

---

## 📐 Assumptions

- Traffic conditions and vehicle type have measurable effects on effective demand.
- Demand normalization is required before applying pricing multipliers.
- Within a 0.5 km radius, lot proximity significantly affects competitive equilibrium.

---

## 📦 Requirements

```bash
pip install -U pathway bokeh pandas numpy matplotlib
```

---

## 🗺️ Roadmap

- [ ] Add price elasticity modelling per vehicle category
- [ ] Integrate real OSM map coordinates for Indian city parking data
- [ ] Deploy as a live Streamlit or web dashboard

---

## 🔗 References

- [Pathway Documentation — First Real-Time App](https://pathway.com/developers/user-guide/introduction/first_realtime_app_with_pathway/)
- [Pathway Deployment Guide — From Jupyter to Deploy](https://pathway.com/developers/user-guide/deployment/from-jupyter-to-deploy/)
- [Summer Analytics 2025 — CnA Club, IIT Guwahati](https://www.caciiitg.com/sa/course25/)

---

## 📄 License

MIT — see [LICENSE](LICENSE).

---

<div align="center">

Built by [Aditya Raj](https://github.com/aditweb13) · [LinkedIn](https://linkedin.com/in/aditya-raj-a1891a285) · [adi111sam121@gmail.com](mailto:adi111sam121@gmail.com)

</div>

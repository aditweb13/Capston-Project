
# 🚗 Real-Time Dynamic Pricing for Urban Parking Lots

## 👨‍💻 Capstone Project – Summer Analytics 2025  
**Hosted by:** Consulting & Analytics Club × Pathway  
**Platform:** Google Colab + Pathway + Bokeh

---

## 📌 Problem Overview

Urban parking is a high-demand, limited-resource service. Static pricing results in poor utilization: either underuse or over-congestion. The objective of this project is to simulate a real-time, data-driven dynamic pricing engine for 14 city parking lots using Python and Pathway.

We model and simulate three increasing levels of pricing intelligence:

1. **Model 1:** Baseline Linear Model  
2. **Model 2:** Demand-Based Pricing  
3. **Model 3:** Competitive Pricing with Proximity Awareness

All models ingest real-time data and produce dynamic pricing using **Pathway's streaming framework**, with real-time visualizations using **Bokeh**.

---

## 📊 Dataset Summary

- **Duration:** 73 days  
- **Frequency:** Every 30 minutes (8:00 AM – 4:30 PM)  
- **Total Time Steps:** 18 per day  
- **Parking Spaces:** 14 lots  
- **Total Records:** ~18,000–20,000  

Each record includes:
- Location (Latitude, Longitude)
- Capacity, Occupancy, Queue Length
- Vehicle Type (car, bike, truck)
- Nearby Traffic Condition
- Special Day Indicator

---

## ⚙️ Model Descriptions

### 🔹 Model 1 – Linear Pricing Model
A simple linear increment model:

```
Priceₜ₊₁ = Priceₜ + α × (Occupancy / Capacity)
```

- Starts at `$10`
- Bounded between `$5` and `$20`
- Smooth, continuous price changes

### 🔹 Model 2 – Demand-Based Pricing Model

```
Demand = α·(Occupancy/Capacity) + β·QueueLength − γ·Traffic 
         + δ·IsSpecialDay + ε·VehicleTypeWeight
```

Pricing is updated as:

```
Priceₜ = BasePrice × (1 + λ × NormalizedDemand)
```

Weights are manually tuned for interpretability.

### 🔹 Model 3 – Competitive Pricing Model

Enhances Model 2 by incorporating nearby competitor lots:
- Proximity via **Haversine formula**
- Dynamic adjustment based on neighboring prices
- 0.5 km radius sensitivity

---

## 🚦 Real-Time Simulation with Pathway

- Data streamed row-by-row using Pathway
- Features processed live with `@pw.udf`
- Output piped to CSV and dashboard

```python
mode="streaming", autocommit_duration_ms=300
```

---

## 📈 Real-Time Visualization with Bokeh

- Live plot of predicted prices
- Refreshes as data flows through
- Complements dashboard view

---

## 📁 Files in This Project

- `Capstone_Project_Updated.ipynb` – Main notebook
- `dataset.csv` – Real-time input data
- `realtime_output.csv` – Live pricing output
- `README.md` – Documentation

---

## 📌 How to Run

1. Upload `dataset.csv` in Colab
2. Run notebook cell-by-cell
3. View:
   - Pathway progress dashboard
   - Live Bokeh plot of pricing
4. Export or tune as needed

---

## 📚 Assumptions

- Traffic/vehicle type affect demand
- Demand normalization required
- Proximity matters for real-world decisions

---

## 📦 Requirements

```bash
pip install -U pathway bokeh pandas numpy matplotlib
```

---

## 📍 References

- [Pathway Docs](https://pathway.com/developers/user-guide/introduction/first_realtime_app_with_pathway/)
- [Pathway Deployment Guide](https://pathway.com/developers/user-guide/deployment/from-jupyter-to-deploy/)
- [CnA Club – Summer Analytics](https://www.caciitg.com/sa/course25/)

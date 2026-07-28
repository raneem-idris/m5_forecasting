# M5 Demand Forecasting & Inventory Optimization Pipeline

> **End-to-end Machine Learning and Prescriptive Analytics pipeline for large-scale retail demand forecasting using the M5 Forecasting Dataset.**

This project combines **time-series forecasting** with **inventory optimization** to generate accurate sales predictions and transform them into actionable replenishment decisions through **Dynamic Safety Stock** and **Reorder Point (ROP)** calculations.

---

## Features

- End-to-end forecasting pipeline
- Automated feature engineering
- Memory-optimized preprocessing
- LightGBM forecasting with Tweedie Loss
- Inventory optimization engine
- Dynamic Safety Stock calculation
- Reorder Point (ROP) generation
- Modular and extensible architecture

---

## Project Structure

```text
M5_STOCK_PREDICTION/
│
├── script/
│   ├── modules/
│   │   ├── data.py
│   │   ├── makeFeatures.py
│   │   ├── lightGBM.py
│   │   └── prescriptiveEngine.py
│   │
│   └── src/
│       └── config.py
│
├── train.py
├── README.md
└── PROJECT_DOCUMENTATION.md
```

---

## Pipeline Overview

```text
Raw M5 Dataset
      │
      ▼
Data Preprocessing
      │
      ▼
Feature Engineering
      │
      ▼
LightGBM Forecasting
      │
      ▼
Demand Forecast
      │
      ▼
Inventory Optimization
      │
      ▼
Safety Stock & Reorder Point
```

---

## Outputs

The pipeline generates:

- Trained LightGBM model
- Demand forecasts
- Safety Stock recommendations
- Reorder Point (ROP)
- Inventory recommendations
- Processed datasets for inference

---

## Technologies

| Category | Tools |
|----------|-------|
| Language | Python |
| Machine Learning | LightGBM |
| Data Processing | Pandas, NumPy |
| Forecasting | Tweedie Loss |
| Feature Engineering | Lag & Rolling Features |
| Inventory Optimization | Safety Stock, Reorder Point |

---

## Why This Project?

Traditional forecasting systems stop after predicting future demand. This project extends forecasting with **prescriptive analytics**, converting predictions into inventory decisions that help reduce stockouts while minimizing excess inventory.

---

## Documentation

For a detailed explanation of the project architecture, data pipeline, feature engineering, model implementation, and inventory optimization process, see:

**📄 PROJECT_DOCUMENTATION.md**

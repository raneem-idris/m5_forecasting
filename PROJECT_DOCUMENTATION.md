# M5 Demand Forecasting & Inventory Optimization

## Technical Documentation

This document provides a detailed explanation of the project architecture, implementation, and workflow.

---

# Table of Contents

1. Project Overview
2. Business Problem
3. Dataset
4. Pipeline Architecture
5. Module Documentation
6. Model Details
7. Inventory Optimization
8. Outputs
9. Future Improvements

---

# 1. Project Overview

The objective of this project is to build an end-to-end machine learning pipeline capable of forecasting retail demand using the M5 Forecasting dataset and transforming those predictions into inventory decisions.

The workflow combines:

- Predictive Analytics
- Prescriptive Analytics

Instead of ending with demand prediction, the pipeline recommends inventory policies by computing Safety Stock and Reorder Point values.

---

# 2. Business Problem

Retail demand is highly dynamic due to seasonality, promotions, holidays, pricing strategies, and customer behavior.

Inaccurate forecasts lead to:

- Stock shortages
- Overstocking
- Increased operational costs
- Lost sales opportunities

The objective is to improve inventory planning through accurate forecasting and data-driven replenishment strategies.

---

# 3. Dataset

The project uses the **M5 Forecasting Dataset**, which contains historical Walmart sales.

Main files include:

- sales_train_validation.csv
- calendar.csv
- sell_prices.csv

These datasets provide historical sales, calendar events, SNAP indicators, and weekly selling prices.

---

# 4. Pipeline Architecture

## Stage 1 — Data Loading

### Objective

Load all required CSV files.

### Input

- Sales data
- Calendar data
- Price data

### Output

Raw DataFrames.

---

## Stage 2 — Data Preprocessing

### Objective

Transform raw data into a machine-learning-ready dataset.

### Operations

- Melt sales table
- Merge calendar
- Merge prices
- Handle missing values
- Convert data types
- Memory optimization

### Output

Integrated historical dataset.

---

## Stage 3 — Feature Engineering

### Objective

Generate predictive features from historical observations.

### Temporal Features

- Lag 7
- Lag 28

### Rolling Statistics

- Mean
- Standard deviation
- Minimum
- Maximum

Window sizes:

- 7 days
- 14 days
- 30 days
- 90 days

### Price Features

- Relative price
- Price difference
- Promotional indicators
- Price elasticity proxies

### Output

Feature-rich dataset ready for model training.

---

## Stage 4 — Model Training

### Algorithm

LightGBM

### Objective Function

Tweedie Loss

### Why LightGBM?

- High prediction accuracy
- Fast training
- Low memory usage
- Excellent performance on structured data

### Output

Forecasted demand for each product and forecasting horizon.

---

## Stage 5 — Inventory Optimization

The forecasting output is transformed into inventory decisions.

### Dynamic Safety Stock

Safety Stock is calculated according to:

- Forecast variability
- Demand uncertainty
- Lead time

The objective is to reduce stockout risk while avoiding excessive inventory.

---

## Stage 6 — Reorder Point (ROP)

The reorder point determines when inventory replenishment should occur.

Formula:

```text
ROP = Forecast Demand During Lead Time + Safety Stock
```

Whenever inventory falls below this threshold, replenishment is recommended.

---

# Complete Workflow

```text
Raw Data
    │
    ▼
Data Preprocessing
    │
    ▼
Feature Engineering
    │
    ▼
LightGBM Training
    │
    ▼
Demand Forecast
    │
    ▼
Dynamic Safety Stock
    │
    ▼
Reorder Point (ROP)
    │
    ▼
Inventory Recommendation
```

---

# 5. Module Documentation

## train.py

Pipeline entry point.

Responsibilities:

- Execute preprocessing
- Generate features
- Train model
- Produce forecasts
- Save trained models

---

## src/config.py

Stores:

- Dataset paths
- Hyperparameters
- Random seed
- Feature configuration

---

## script/modules/data.py

Responsibilities:

- Read datasets
- Merge tables
- Memory optimization
- Data reshaping
- Missing value handling

---

## script/modules/makeFeatures.py

Creates:

- Lag features
- Rolling statistics
- Price features
- Time-based features

---

## script/modules/lightGBM.py

Implements:

- Dataset preparation
- Model training
- Validation
- Prediction
- Model serialization

---

## script/modules/prescriptiveEngine.py

Responsible for:

- Dynamic Safety Stock
- Lead-time demand estimation
- Reorder Point calculation
- Inventory recommendations

---

# 6. Model Details

## Forecasting Algorithm

LightGBM Gradient Boosted Decision Trees.

### Loss Function

Tweedie Loss

This objective is particularly suitable for retail forecasting because it effectively models:

- Sparse demand
- Zero-inflated sales
- Positive continuous values

---

# 7. Inventory Optimization

The project extends traditional forecasting by integrating prescriptive analytics.

Generated inventory metrics include:

- Forecast Demand
- Safety Stock
- Reorder Point (ROP)

These metrics support inventory planning and replenishment decisions.

---

# 8. Outputs

After execution, the pipeline produces:

- Trained LightGBM model (.pkl)
- Demand forecasts
- Safety Stock recommendations
- Reorder Point calculations
- Inventory recommendations
- Processed datasets ready for inference

---

# 9. Future Improvements

Potential extensions include:

- Multi-horizon forecasting
- Deep learning models (LSTM, TFT)
- Hyperparameter optimization with Optuna
- SHAP explainability
- Real-time forecasting API
- Automated retraining pipeline
- Interactive inventory dashboard

---

# Conclusion

This project demonstrates how machine learning can be integrated with inventory optimization to build a complete decision-support system for retail demand planning. By combining accurate forecasting with prescriptive inventory policies, the pipeline enables data-driven replenishment strategies that help reduce stockouts while minimizing excess inventory.

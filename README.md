M5 Demand Forecasting & Inventory Optimization Pipeline

End-to-end Machine Learning and Prescriptive Analytics pipeline for large-scale retail demand forecasting using the M5 Forecasting Dataset.

This project combines time-series forecasting with inventory optimization to generate accurate sales predictions and convert them into actionable replenishment decisions using Dynamic Safety Stock and Reorder Point (ROP) calculations.

Features
End-to-end forecasting pipeline
Automated feature engineering
Memory-optimized preprocessing for large datasets
LightGBM forecasting with Tweedie Loss
Inventory optimization engine
Configurable training pipeline
Modular and extensible codebase
Project Structure
M5_STOCK_PREDICTION/
│
├── script/
│   └── modules/
│       ├── data.py
│       ├── makeFeatures.py
│       ├── lightGBM.py
│       └── prescriptiveEngine.py
│
├── src/
│   └── config.py
│
├── train.py
│
└── README.md
Pipeline Workflow
               Raw M5 Dataset
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
          Sales Forecast Output
                      │
                      ▼
      Inventory Optimization Engine
                      │
      ┌───────────────┴───────────────┐
      ▼                               ▼
 Safety Stock                  Reorder Point

Module Overview
Module	Responsibility
train.py	Executes the complete machine learning pipeline.
config.py	Stores global configuration, file paths, and model hyperparameters.
data.py	Handles preprocessing, joins, reshaping, and memory optimization.
makeFeatures.py	Generates lag, rolling statistics, and price-related features.
lightGBM.py	Implements the forecasting model using LightGBM with Tweedie Loss.
prescriptiveEngine.py	Converts forecasts into inventory policies (Safety Stock & ROP).

Module Details
1. train.py
Purpose

Acts as the pipeline entry point and orchestrates the complete forecasting workflow.

Responsibilities
Load processed datasets
Execute feature engineering
Train LightGBM models
Save trained models (.pkl)
Produce demand forecasts
2. src/config.py
Purpose

Centralized configuration file used throughout the project.

Responsibilities
Dataset paths
Sampling configuration
Random seed
Model hyperparameters
Feature settings
3. script/modules/data.py
Purpose

Processes the raw M5 dataset into a machine learning-ready format.

Responsibilities
Data Ingestion
Load raw CSV files
Data Reshaping
Melt wide-format sales tables into long format
Data Integration

Merge with:

Calendar events
Promotions
Weekly prices
Memory Optimization

Reduce RAM usage through datatype downcasting.

Examples:

float64 → float32
int64 → int16
int64 → int8
4. script/modules/makeFeatures.py
Purpose

Creates predictive features from historical sales and pricing information.

Generated Features
Temporal Features
7-day lag
28-day lag
Rolling Statistics
Moving Average
Moving Standard Deviation
Moving Minimum
Moving Maximum

Window sizes:

7 days
14 days
30 days
90 days
Price Features
Relative price changes
Promotional discounts
Price elasticity indicators
5. script/modules/lightGBM.py
Purpose

Forecasts intermittent demand using Gradient Boosted Decision Trees.

Algorithm
LightGBM
Objective Function

Tweedie Loss

Ideal for:

Sparse demand
Zero-inflated sales
Retail forecasting
Output

Forecasted demand for each product and time period.

6. script/modules/prescriptiveEngine.py
Purpose

Transforms demand forecasts into inventory decisions.

Inventory Policies
Dynamic Safety Stock

Calculates inventory buffers based on:

Demand uncertainty
Forecast variability
Lead time
Reorder Point (ROP)

Automatically computes replenishment thresholds using:

ROP = Forecast Demand During Lead Time + Safety Stock
End-to-End Pipeline
Raw Data
    │
    ▼
Preprocessing
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
Safety Stock
    │
    ▼
Reorder Point
    │
    ▼
Inventory Recommendation
Outputs

After training, the pipeline generates:

Trained LightGBM model (.pkl)
Demand forecasts
Safety Stock recommendations
Reorder Point (ROP) calculations
Processed datasets ready for inference
Technologies
Category	Tools
Language	Python
Machine Learning	LightGBM
Data Processing	Pandas, NumPy
Forecasting	Tweedie Loss
Feature Engineering	Lag & Rolling Features
Inventory Optimization	Safety Stock, Reorder Point
Why This Project?

This repository demonstrates how predictive analytics and prescriptive analytics can be integrated into a unified workflow. Rather than stopping at demand forecasting, the pipeline extends predictions into inventory optimization, enabling data-driven replenishment strategies that help reduce stockouts while minimizing excess inventory.


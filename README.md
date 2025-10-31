# Quantifying Cumulative Space Radiation Dose and Cancer Risk

## Project Overview
Hybrid physics-machine learning model for predicting cumulative radiation dose and cancer risk for long-duration spaceflight missions (ISS, Lunar Gateway, Mars transit).

## Directory Structure
```
├── data/
│   ├── raw/              # Original downloaded datasets
│   └── processed/        # Cleaned and merged data
├── src/
│   ├── data_acquisition/ # Scripts to fetch NASA/NOAA data
│   ├── physics/          # Shielding calculations, dose conversions
│   ├── ml_models/        # XGBoost training and prediction
│   └── visualization/    # Streamlit dashboard
├── models/               # Trained model artifacts
├── notebooks/            # Jupyter notebooks for exploration
└── docs/                 # Documentation and methods
```

## Data Sources
See `docs/data_sources.md` for detailed catalog of radiation environment datasets, solar activity indices, and conversion references.

## Installation
```bash
pip install -r requirements.txt
```

## Usage
Coming soon: instructions for data acquisition, model training, and dashboard deployment.

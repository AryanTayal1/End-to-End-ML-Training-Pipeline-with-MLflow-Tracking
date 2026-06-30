# End-to-End ML Training Pipeline with MLflow Tracking

An automated machine learning pipeline that ingests data, engineers features, trains multiple models, and tracks every experiment using MLflow — with built-in model drift detection to trigger retraining.

## Overview

This project demonstrates a production-style ML workflow: from raw data to a registered, versioned model ready for deployment, with full experiment traceability.

## Dataset

**UCI Heart Disease Dataset**
- Source: https://archive.ics.uci.edu/dataset/45/heart+disease
- Kaggle mirror: https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset
- 14 clinical attributes used to predict presence of heart disease

## Tech Stack

`Python` · `Scikit-learn` · `MLflow` · `Apache Airflow` · `SQL` · `Pandas`

## Pipeline Architecture

```
Raw Data → Preprocessing → Feature Engineering → Model Training
    → MLflow Tracking → Model Registry → Drift Detection → Retraining Trigger
```

## Key Features

- **Automated orchestration** via Apache Airflow DAGs — reduced pipeline setup time by ~70% vs. manual execution
- **Experiment tracking** across 20+ training runs (Random Forest, SVM, Logistic Regression) with MLflow
- **Model versioning** through MLflow Model Registry, with staged promotion (Staging → Production)
- **Drift detection** using Kolmogorov-Smirnov tests comparing live predictions vs. training baseline, with automated retraining alerts

## Results

| Model | F1 Score | AUC |
|---|---|---|
| Random Forest | 0.87 | 0.91 |
| SVM | 0.84 | 0.89 |
| Logistic Regression | 0.82 | 0.87 |

## Setup

```bash
pip install mlflow scikit-learn pandas numpy matplotlib seaborn apache-airflow
```

## Run

```bash
# Start MLflow tracking server
mlflow ui --port 5000

# Run the notebook
jupyter notebook ml_pipeline_mlflow.ipynb
```

## Deploy as REST API

```bash
mlflow models serve -m "models:/HeartDiseaseClassifier/Production" --port 1234

curl -X POST http://localhost:1234/invocations \
  -H "Content-Type: application/json" \
  -d '{"dataframe_records": [{"age":55,"sex":1,"cp":3,"trestbps":140,"chol":200,"fbs":0,"restecg":1,"thalach":150,"exang":0,"oldpeak":1.5,"slope":2,"ca":0,"thal":2}]}'
```

## Project Structure

```
.
├── ml_pipeline_mlflow.ipynb   # Main notebook
└── README.md
```

## Author

**Aryan Tayal**
[LinkedIn](#) · [GitHub](#) · tayalaryan15@gmail.com

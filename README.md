# Insurance Premium Predictor API

A production-ready FastAPI service that predicts an insurance premium category based on user demographic, lifestyle, and financial information.
The service uses a pre-trained scikit-learn model and performs strict input validation and feature engineering using Pydantic v2.

---

## Table of Contents

- Overview
- Project Structure
- Architecture
- Features
- API Endpoints
- Request & Response Examples
- Running Locally
- Running with Docker
- Model Details
- Validation & Feature Engineering
- Tech Stack
- License

---

## Overview

The Insurance Premium Predictor API accepts structured user profile data and returns:

- Predicted insurance premium category
- Confidence score for the prediction
- Probability distribution across all supported classes

The API is designed with strong schema validation, deterministic feature computation, and container-ready deployment.

---

## Project Structure
```
Insurance_premium_predictor/
├── app.py
├── Dockerfile
├── requirements.txt
│
├── Model/
│   ├── predict.py
│   └── model.pkl
│
├── config/
│   └── city_tier.py
│
└── schema/
    ├── user_input.py
    └── prediction_response.py
```
---

## Architecture
```
Client
  |
  v
FastAPI Endpoint (/predict)
  |
  v
Pydantic Validation
  |
  v
Feature Engineering
  |
  v
Scikit-learn Model (model.pkl)
  |
  v
Prediction + Probabilities
  |
  v
JSON Response
```
---

## Features

- Strict request validation using Pydantic v2
- Computed features derived at request time
- Versioned ML model loading
- Probability-based prediction output
- Health-check endpoint
- Docker-ready deployment

---

## API Endpoints

GET /
Returns a welcome message.

GET /health
Health check endpoint to verify model and API status.

POST /predict
Predicts the insurance premium category.

---

## Request & Response Examples

Prediction Request (JSON)

{
  "age": 30,
  "weight": 70,
  "height": 1.72,
  "income_lpa": 10,
  "smoker": false,
  "city": "Pune",
  "occupation": "private_job"
}

Prediction Response (JSON)

{
  "Response": {
    "predicted_category": "High",
    "confidence": 0.8432,
    "class_probabilities": {
      "Low": 0.01,
      "Medium": 0.1468,
      "High": 0.8432
    }
  }
}

---

## Running Locally

1. Create virtual environment

   python -m venv venv
   source venv/bin/activate

2. Install dependencies

   pip install -r requirements.txt

3. Start the API

   uvicorn app:app --host 0.0.0.0 --port 8000

Swagger UI:
http://localhost:8000/docs

---

## Running with Docker

Build Docker image

   docker build -t insurance-premium-predictor .

Run Docker container

   docker run -p 8000:8000 insurance-premium-predictor

---

## Model Details

- Framework: scikit-learn
- Serialization: pickle
- Model path: Model/model.pkl
- Supported methods:
  - predict()
  - predict_proba()
  - classes_

Model version is defined in Model/predict.py.

---

## Validation & Feature Engineering

Computed features include:

- BMI: Body Mass Index
- Age Group: young, adult, middle_aged, senior
- Lifestyle Risk: low, medium, high
- City Tier: 1, 2, or 3 based on city mapping

City tier classification is defined in config/city_tier.py.

---

## Tech Stack

- FastAPI
- Pydantic v2
- scikit-learn
- pandas
- NumPy
- Uvicorn
- Docker




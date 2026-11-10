
# House Price Prediction MLOps

An end-to-end Machine Learning Operations (MLOps) project for predicting house prices using machine learning, with FastAPI-based prediction serving, experiment tracking, data versioning, Docker containerization, automated testing, and CI/CD.

**GitHub Repository:** https://github.com/pallu6753/house-price-mlops

---

## 👩‍💻 Student Information

- **Name:** Pallavi R
- **USN:** 1TJ23DS019
- **Degree:** B.E. – Computer Science and Engineering (Data Science)
- **Institution:** T. John Institute of Technology, Bengaluru
- **GitHub:** https://github.com/pallu6753

---

## 📌 Project Overview

House Price Prediction MLOps is a machine learning project that predicts real-estate prices based on property-related features.

The project combines machine learning development with MLOps practices to support model training, prediction serving, reproducibility, testing, and deployment.

The trained Random Forest model is exposed through a FastAPI REST API.

## 🎯 Objectives

- Develop a machine learning model for house price prediction.
- Preprocess and validate housing data.
- Train and evaluate regression models.
- Serve predictions through FastAPI.
- Track experiments using MLflow.
- Manage data and pipelines using DVC.
- Containerize the application using Docker.
- Automate validation using GitHub Actions.
- Deploy the API using Render.

## ✨ Key Features

- Machine learning-based house price prediction.
- Random Forest prediction model.
- FastAPI REST API.
- Interactive Swagger documentation.
- Single and batch prediction endpoints.
- Model information and health-check endpoints.
- MLflow experiment tracking.
- DVC pipeline and data versioning.
- Pytest-based automated testing.
- Docker and Docker Compose support.
- GitHub Actions CI/CD workflow.
- Render cloud deployment.

## 🏗️ System Architecture

```text
             Housing Dataset
                    |
                    v
             Data Preprocessing
                    |
                    v
             Feature Engineering
                    |
                    v
             Model Training
                    |
                    v
          Model Evaluation
                    |
                    v
          Trained ML Model
                    |
                    v
             FastAPI Backend
                    |
          +---------+---------+
          |                   |
          v                   v
      /predict           /predict/batch
          |                   |
          +---------+---------+
                    |
                    v
             Prediction Output
                    |
                    v
             Render Deployment
```

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Pandas | Data processing |
| NumPy | Numerical operations |
| Scikit-learn | Machine learning |
| FastAPI | REST API development |
| Uvicorn | API server |
| MLflow | Experiment tracking |
| DVC | Data and pipeline versioning |
| Pytest | Automated testing |
| Docker | Containerization |
| Git | Version control |
| GitHub Actions | CI/CD automation |
| Render | Cloud deployment |

## 📊 Model Features

The prediction model accepts the following six input features:

| Feature | Description |
|---|---|
| `transaction_date` | Transaction date value |
| `house_age` | Age of the house |
| `distance_to_nearest_mrt` | Distance to nearest MRT station |
| `convenience_stores` | Number of nearby convenience stores |
| `latitude` | Property latitude |
| `longitude` | Property longitude |

### Prediction Model

- **Model:** Random Forest Regressor
- **Model Version:** 1.0.0
- **Prediction Unit:** 10,000 New Taiwan Dollar per Ping

## 📁 Project Structure

```text
house-price-mlops/
│
├── .github/
│   └── workflows/
│
├── app/
│   ├── main.py
│   ├── schemas.py
│   └── services/
│
├── src/
│   ├── train.py
│   ├── preprocess.py
│   └── evaluate.py
│
├── tests/
│
├── docs/
│
├── requirements.txt
├── requirements-runtime.txt
├── params.yaml
├── dvc.yaml
├── Dockerfile
├── docker-compose.yml
├── .gitignore
└── README.md
```

*Note: This is the project's intended high-level structure. Check the repository for the exact files included in the current version.*

## ⚙️ Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/pallu6753/house-price-mlops.git

cd house-price-mlops
```

### 2. Create a Virtual Environment

**Windows PowerShell:**

```powershell
python -m venv venv

.\venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

```bash
python -m pip install --upgrade pip

pip install -r requirements.txt
```

## 🚀 Model Training

Run the training script:

```bash
python src/train.py
```

The training workflow is intended to load the dataset, preprocess features, train the configured regression model, evaluate performance, and save the trained model artifact.

### Evaluation Metrics

- MAE – Mean Absolute Error
- MSE – Mean Squared Error
- RMSE – Root Mean Squared Error
- R² – Coefficient of Determination

Use the actual evaluation results generated by the training process.

## 🌐 Running the API

Start the FastAPI server:

```bash
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

Open the API documentation:

- Swagger UI: http://127.0.0.1:8000/docs
- ReDoc: http://127.0.0.1:8000/redoc

## 🔗 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | API information |
| GET | `/health` | Health check |
| GET | `/model-info` | Model information |
| POST | `/predict` | Single house price prediction |
| POST | `/predict/batch` | Batch predictions |

### Example Prediction Request

**POST `/predict`**

```json
{
  "transaction_date": 2013.5,
  "house_age": 15.2,
  "distance_to_nearest_mrt": 850.5,
  "convenience_stores": 5,
  "latitude": 24.982,
  "longitude": 121.543
}
```

### Example Prediction Response

```json
{
  "predicted_price_per_unit_area": 37.12484933862435,
  "unit": "10,000 New Taiwan Dollar per Ping",
  "model_name": "random_forest",
  "model_version": "1.0.0"
}
```

This is an example response observed during local API testing. Predictions depend on the input features and loaded model.

## 🐳 Docker Setup

Build the Docker image:

```bash
docker build -t house-price-mlops-api .
```

Run the container:

```bash
docker run --rm -p 8000:8000 house-price-mlops-api
```

Open:

http://localhost:8000/docs

### Docker Compose

```bash
docker compose up --build
```

Stop the services:

```bash
docker compose down
```

## 🔄 DVC – Data Version Control

Reproduce the configured pipeline:

```bash
dvc repro
```

Check pipeline status:

```bash
dvc status
```

DVC remote storage must be configured before pushing or pulling data from a remote location.

## 📈 MLflow – Experiment Tracking

Start the MLflow UI:

```bash
mlflow ui
```

Open:

http://127.0.0.1:5000

Experiments will appear when the training code logs runs to the configured tracking store.

## 🧪 Testing

Run automated tests:

```bash
pytest -v
```

Testing should cover data processing, model predictions, API validation, and application behavior.

## ⚡ CI/CD – GitHub Actions

GitHub Actions workflows are maintained in:

```text
.github/workflows/
```

To inspect workflow results:

1. Open the GitHub repository.
2. Select the **Actions** tab.
3. Open the latest workflow run.
4. Review the build and test results.

## ☁️ Render Deployment

The FastAPI application is deployed using Render.

**Build Command:**

```bash
pip install -r requirements.txt
```

**Start Command:**

```bash
uvicorn app.main:app --host 0.0.0.0 --port $PORT
```

Render automatically provides the `PORT` environment variable.

After deployment, verify:

- API homepage
- Health endpoint
- Model information
- Swagger documentation
- Prediction endpoint

## 🔮 Future Improvements

- Compare multiple regression algorithms.
- Improve feature engineering and data validation.
- Enhance experiment tracking.
- Add model monitoring and data-drift detection.
- Improve automated model retraining.
- Expand API integration testing.
- Enhance deployment automation.

## 👩‍🎓 Author

**Pallavi R**

B.E. – Computer Science and Engineering (Data Science)  
T. John Institute of Technology, Bengaluru

**USN:** 1TJ23DS019

**GitHub:** https://github.com/pallu6753

**Project Repository:** https://github.com/pallu6753/house-price-mlops

---

*This project is developed for educational and demonstration purposes. Predicted property prices are model estimates and should not be treated as professional property valuations.*

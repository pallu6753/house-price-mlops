House Price Prediction MLOps
An end-to-end machine learning and MLOps project that predicts
real-estate unit prices using a trained regression model and exposes
predictions through a FastAPI REST API. The project also includes
tooling for experiment tracking, data/pipeline versioning, testing,
containerization, CI/CD, and cloud deployment.

Repository: https://github.com/pallu6753/house-price-mlops
Project Overview
This project demonstrates a reproducible workflow for developing and
serving a house-price prediction model. The API accepts property-related
features and returns a predicted price per unit area.

The prediction request uses the following features:
- transaction_date
- house_age
- distance_to_nearest_mrt
- convenience_stores
- latitude
- longitude
The currently tested API response identifies the model as
random_forest and reports the prediction unit as 10,000 New Taiwan
Dollar per Ping. Predictions are estimates from the trained model and
should not be treated as professional property valuations.
Student / Author
Pallavi R
USN: 1TJ23DS019
B.E. -- Computer Science and Engineering (Data Science)
T. John Institute of Technology, Bengaluru
- GitHub: https://github.com/pallu6753
- Project repository: https://github.com/pallu6753/house-price-mlops
Key Features
- House-price prediction using a trained machine-learning regression
  model.
- FastAPI REST API with interactive Swagger documentation.
- Single-record and batch prediction routes, where implemented.
- Model metadata and health-check endpoints.
- MLflow experiment tracking, when configured.
- DVC data and pipeline versioning, when configured.
- Automated tests using Pytest.
- Docker containerization and Docker Compose configuration.
- GitHub Actions workflow for CI checks.
- Cloud deployment on Render.
The availability of an individual MLOps feature depends on its
configuration in the repository. Use the commands and status reported
by the actual project rather than assuming that every optional service
is active.

Technology Stack
  Technology                          Purpose
  Python                              Main programming language

  Pandas / NumPy                      Data processing and numerical
operations

  Scikit-learn                        Machine-learning model training and
evaluation

  FastAPI                             REST API

  Uvicorn                             ASGI application server

  MLflow                              Experiment tracking and
model-related metadata

  DVC                                 Dataset and pipeline versioning

  Pytest                              Automated testing

  Docker / Docker Compose             Containerization and local service
orchestration

  Git / GitHub                        Source-code version control

  GitHub Actions                      CI automation
Render                              Cloud hosting
Model Features and Prediction Unit
The API input schema uses these six fields:

  Field                       Description
  transaction_date          Transaction date value used by the dataset
house_age                 Age of the house
distance_to_nearest_mrt   Distance to the nearest MRT station
convenience_stores        Number of nearby convenience stores
latitude                  Property latitude
longitude                 Property longitude

The prediction is returned as predicted_price_per_unit_area. The unit
reported by the API is 10,000 New Taiwan Dollar per Ping.
Project Structure
The following is a high-level guide. The actual files in the repository
are authoritative; optional folders or files may differ by version.
house-price-mlops/
├── .github/
│   └── workflows/
├── app/
│   ├── main.py
│   ├── schemas.py
│   └── services/
├── src/
│   ├── train.py
│   ├── preprocess.py
│   └── evaluate.py
├── tests/
├── docs/
├── requirements.txt
├── requirements-runtime.txt
├── params.yaml
├── dvc.yaml
├── Dockerfile
├── docker-compose.yml
└── README.md
Prerequisites
Install the tools required for the workflow you intend to run:
- Python 3.10 or later, subject to dependency compatibility.
- Git.
- Docker Desktop or Docker Engine (for container workflows).
- DVC (for DVC workflows).
Check installations:
python --version
git --version
docker --version
dvc --version
Installation
1. Clone the repository
git clone https://github.com/pallu6753/house-price-mlops.git
cd house-price-mlops
2. Create and activate a virtual environment
Windows PowerShell:
python -m venv venv
.\venv\Scripts\Activate.ps1
macOS / Linux:
python -m venv venv
source venv/bin/activate
3. Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt
If you only need the runtime API dependencies and the repository's
runtime requirements file is present, you can install:
pip install -r requirements-runtime.txt
Train the Model
From the repository root, run:
python src/train.py
The training script is responsible for loading and preparing the
dataset, training the configured regression model, evaluating it, and
saving the model artifact. Check the script's output and configured
artifact path to confirm where the trained model is stored.

Common regression evaluation metrics include:
- MAE --- Mean Absolute Error
- MSE --- Mean Squared Error
- RMSE --- Root Mean Squared Error
- R² --- Coefficient of determination
Record actual values produced by your training run. Do not insert
assumed performance numbers into project documentation.
Run the API Locally
Start the FastAPI server from the repository root:
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
Open the API documentation:
- Swagger UI: http://127.0.0.1:8000/docs
- ReDoc: http://127.0.0.1:8000/redoc
The API entry point shown above matches the local command used for this
project. If the application module is changed, update the command
accordingly.
API Endpoints
The project API includes the following routes:

  Method   Endpoint           Purpose
  GET    /                API information
GET    /health          Health check
GET    /model-info      Model information
POST   /predict         Predict one property price
POST   /predict/batch   Predict for multiple records

Swagger UI is available at /docs while the API is running.
Example request: POST /predict
{
  "transaction_date": 2013.5,
  "house_age": 15.2,
  "distance_to_nearest_mrt": 850.5,
  "convenience_stores": 5,
  "latitude": 24.982,
  "longitude": 121.543
}
Use values appropriate to the dataset and the model's expected input
ranges. The example is illustrative; it is not a guarantee of a
particular prediction.
Example response
{
  "predicted_price_per_unit_area": 37.12484933862435,
  "unit": "10,000 New Taiwan Dollar per Ping",
  "model_name": "random_forest",
  "model_version": "1.0.0"
}
This is an example of a successful response observed during local API
testing. A prediction can vary with the input values and the loaded
model artifact.
Docker
Build the image:
docker build -t house-price-mlops-api .
Run the container:
docker run --rm -p 8000:8000 house-price-mlops-api
Open:

http://localhost:8000/docs

If the repository's Docker Compose configuration is ready to use, start
its services with:
docker compose up --build
Stop the Compose services with:
docker compose down
DVC
If DVC is configured in the repository, reproduce the pipeline with:
dvc repro
To inspect DVC-tracked files and pipeline status:
dvc status
A DVC remote must be configured and accessible before pushing or pulling
remote data. Follow the existing .dvc/config and repository setup; do
not initialize DVC again if it is already initialized.
MLflow
If MLflow tracking is configured, start the tracking UI using the
tracking configuration for the project. A common local command is:
mlflow ui
Then open:

http://127.0.0.1:5000

The tracking UI will show runs only when the training code logs
experiments to the configured tracking store.
Testing
Run the test suite from the repository root:
pytest -v
A successful test run should complete without failures. Include only
test results that have actually been executed.
CI/CD
The GitHub Actions workflows are stored in:
.github/workflows/
To inspect a workflow run:
1. Open the repository on GitHub.
2. Select Actions.
3. Open the latest workflow run.
4. Review each job and its logs.
5. Fix any failed step before treating the workflow as successful.
A successful build or test workflow does not by itself prove that a
Docker image was published or that a deployment completed. Those steps
require their own configuration and successful run.
Deploy on Render
The FastAPI service can be hosted on Render as a Web Service.

Typical settings for this repository:

Build command
pip install -r requirements.txt
Start command
uvicorn app.main:app --host 0.0.0.0 --port $PORT
Set environment variables only when the application requires them.
Render provides the PORT value automatically; do not hard-code it.
Confirm that the trained model artifact is included in the repository or
generated during the deployment build.

After deployment, test the Render service's /, /health,
/model-info, and /docs routes. Add the exact public Render URL here
once confirmed:
Live API: <add-your-render-service-url>
Swagger UI: <add-your-render-service-url>/docs
Troubleshooting
ModuleNotFoundError
Install the dependencies in the active virtual environment:
pip install -r requirements.txt
Uvicorn cannot import the application
Run the command from the repository root and verify that app/main.py
exists and exposes a FastAPI object named app:
uvicorn app.main:app --reload
Model artifact not found
Confirm that training has completed and that the saved model path
matches the path expected by the API. Ensure the artifact is available
in the Render build/runtime environment.
DVC pipeline cannot run
Check that dvc.yaml contains valid stages and that required data
files, dependencies, parameters, and outputs are available.
Render deployment fails
Review the Render build and runtime logs. Verify the build command,
start command, Python dependency compatibility, and availability of the
trained model artifact.
Future Improvements
- Add stronger data validation and input-range checks.
- Compare multiple regression algorithms using the same evaluation
  split.
- Improve experiment tracking and model version management.
- Add API integration tests and deployment health checks.
- Configure shared DVC remote storage.
- Add prediction monitoring and data-drift detection.
- Automate model retraining and validation.
License
Add an appropriate open-source license before granting public reuse or
redistribution rights. Without a license, do not assume that others have
permission to reuse the project.
Educational project. Predicted prices are model estimates and are not
professional property valuations.

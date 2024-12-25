# end_to_end_churn_prediction

# Churn Prediction Project

## Overview
This project demonstrates an end-to-end machine learning lifecycle for predicting customer churn using the Telco Customer Churn dataset. The lifecycle includes data versioning, experiment tracking, model registry, CI/CD, and model inferencing, leveraging Azure Machine Learning (Azure ML).

---

## Features
- **Data Versioning:** Raw and processed datasets managed using DVC (Data Version Control).
- **Experiment Tracking:** Track model performance metrics and logs using Azure ML.
- **Model Registry:** Maintain multiple versions of the trained model in Azure ML.
- **CI/CD Pipeline:** Automate the training, testing, and deployment workflows using Azure DevOps.
- **Model Deployment:** Deploy the trained model as a REST API on Azure Kubernetes Service (AKS).
- **Monitoring:** Monitor deployed models for performance and drift.

---

## Dataset
**Telco Customer Churn Dataset**

- **Source:** [Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn)
- **Description:** This dataset includes customer information such as demographics, account information, and whether the customer has churned.
- **Features:**
  - `customerID`: Unique customer identifier
  - `gender`, `SeniorCitizen`, `Partner`, `Dependents`
  - `tenure`, `MonthlyCharges`, `TotalCharges`
  - `Contract`, `PaymentMethod`, `PaperlessBilling`
  - `Churn`: Target variable (Yes/No)

---

## Project Structure
```
churn-prediction/
|
├── data/                  # Data directory
│   ├── raw/              # Raw dataset
│   └── processed/        # Processed dataset
|
├── scripts/               # Scripts for training and inferencing
│   ├── preprocess.py
│   ├── train.py
│   ├── score.py
|
├── pipeline/              # Azure ML pipeline components
│   ├── pipeline.py
│   └── components/
|
├── config/                # Configuration files
│   ├── config.json
│   └── environment.yml
|
├── requirements.txt       # Python dependencies
├── azure-pipelines.yml    # CI/CD pipeline definition
└── README.md              # Project documentation
```

---

## Workflow

1. **Data Preparation**
   - Raw data is ingested and versioned using DVC.
   - Preprocessing is performed to clean and prepare the data for training.

2. **Model Training**
   - Train a logistic regression model using `scikit-learn`.
   - Log metrics and artifacts to Azure ML.

3. **Model Registration**
   - Save and register the trained model in Azure ML for versioning and deployment.

4. **Model Deployment**
   - Deploy the model as a REST API on Azure Kubernetes Service (AKS).

5. **Monitoring and Continuous Learning**
   - Monitor deployed models for performance and drift.
   - Trigger retraining pipelines using Azure ML pipelines.

---

## Installation

### Prerequisites
- Azure Subscription
- Python 3.8+
- Azure CLI
- Azure ML SDK
- Git
- DVC

### Steps
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd churn-prediction
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Configure Azure ML workspace:
   ```bash
   az ml workspace configure -w <workspace-name> -g <resource-group>
   ```
4. Set up DVC remote storage:
   ```bash
   dvc remote add -d myremote azure://<container-path>
   ```

---

## Usage

### Data Preprocessing
Run the preprocessing script to prepare the data:
```bash
python scripts/preprocess.py
```

### Training
Train the model and log metrics to Azure ML:
```bash
python scripts/train.py
```

### Deployment
Deploy the trained model to AKS:
```bash
python pipeline/deploy.py
```

### Inferencing
Use the deployed model for predictions:
```bash
curl -X POST -H "Content-Type: application/json" -d '{"data": [...]}'' <scoring-uri>
```

---

## CI/CD Pipeline
The project includes a pre-configured Azure DevOps pipeline defined in `azure-pipelines.yml`. It automates the following:
- Install dependencies and run tests.
- Train and evaluate the model.
- Deploy the model to AKS.

To trigger the pipeline, push changes to the `main` branch.

---

## Monitoring
- Monitor the deployed model using Azure Application Insights.
- Set up alerts for performance degradation or drift detection.

---

## Contributions
Contributions are welcome! Please create a pull request for review.

---

## License
This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments
- Dataset sourced from [Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn).
- Azure ML documentation for guidance on implementation.


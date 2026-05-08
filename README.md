# Kidney Disease Classification with MLflow & DVC

A deep learning project for classifying kidney diseases using convolutional neural networks with MLflow for experiment tracking and DVC for data versioning.

## Table of Contents

- [Overview](#overview)
- [Project Setup](#project-setup)
- [Development Workflow](#development-workflow)
- [MLflow Tracking](#mlflow-tracking)
- [DVC Commands](#dvc-commands)
- [AWS CI/CD Deployment](#aws-cicd-deployment)

## Overview

This project implements an end-to-end machine learning pipeline for kidney disease classification using:
- **TensorFlow/Keras** for deep learning model
- **MLflow** for experiment tracking and model management
- **DVC** for data versioning and pipeline orchestration
- **Docker** for containerization
- **AWS EC2 + ECR** for cloud deployment

## Project Setup

### Prerequisites

- Python 3.8+
- pip package manager

### Getting Started

**1. Clone the repository**

```bash
git clone https://github.com/hashd1229/Kidney-Disease-Classification-MLflow-DVC.git
cd Kidney-Disease-Classification-MLflow-DVC
```

**2. Create a virtual environment**

```bash
python -m venv .venv
.venv\Scripts\activate  # On Windows
# source .venv/bin/activate  # On Linux/Mac
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

## Development Workflow

The standard workflow for updating the project:

1. Update `config/config.yaml` with configuration parameters
2. Update `params.yaml` with training hyperparameters
3. Update `secrets.yaml` (optional) for sensitive credentials
4. Update entity classes in `src/cnnClassifier/entity/`
5. Update configuration manager in `src/cnnClassifier/config/`
6. Update component implementations in `src/cnnClassifier/components/`
7. Update pipeline stages in `src/cnnClassifier/pipeline/`
8. Update `main.py` to orchestrate the pipeline
9. Update `dvc.yaml` for DVC pipeline definition
10. Update `app.py` for Flask application (if applicable)

## MLflow Tracking

### Documentation

- [MLflow Official Documentation](https://mlflow.org/docs/latest/index.html)

### Running MLflow UI

```bash
mlflow ui
```

### Integration with DagsHub

DagsHub provides a unified platform for data versioning and ML experiment tracking. Set up your environment variables:

**PowerShell:**
```powershell
$env:MLFLOW_TRACKING_URI=https://dagshub.com/USERNAME/Kidney-Disease-Classification-MLflow-DVC.mlflow
$env:MLFLOW_TRACKING_USERNAME=YOUR_USERNAME
$env:MLFLOW_TRACKING_PASSWORD=YOUR_TOKEN
```

**Bash:**
```bash
export MLFLOW_TRACKING_URI=https://dagshub.com/USERNAME/Kidney-Disease-Classification-MLflow-DVC.mlflow
export MLFLOW_TRACKING_USERNAME=YOUR_USERNAME
export MLFLOW_TRACKING_PASSWORD=YOUR_TOKEN
```

Then run your training script:

```bash
python main.py
```

## DVC Commands

### Initialize and Run DVC Pipeline

```bash
dvc init                    # Initialize DVC (if not already done)
dvc repro                   # Reproduce the entire pipeline
dvc dag                     # View pipeline DAG (directed acyclic graph)
```

## AWS CI/CD Deployment

### 1. AWS Console Setup

Log in to your AWS console and proceed with the following steps.

### 2. Create IAM User for Deployment

Create an IAM user with the following permissions:

**Required Access:**
- **EC2**: Virtual machine instances
- **ECR**: Elastic Container Registry (to store Docker images)

**Required Policies:**
- `AmazonEC2ContainerRegistryFullAccess`
- `AmazonEC2FullAccess`

### 3. Create ECR Repository

Create an ECR repository to store your Docker images.

**Example ECR URI:**
```
586723123187.dkr.ecr.ap-southeast-2.amazonaws.com/kidney
```

Save this URI for later use.

### 4. Launch EC2 Instance

Create a new EC2 instance with Ubuntu operating system.

### 5. Install Docker on EC2

SSH into your EC2 instance and run:

```bash
# Update system packages
sudo apt-get update -y
sudo apt-get upgrade -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Configure Docker user permissions
sudo usermod -aG docker ubuntu
newgrp docker
```

### 6. Configure EC2 as Self-Hosted Runner

In your GitHub repository:

1. Go to **Settings** → **Actions** → **Runners** → **New self-hosted runner**
2. Choose your OS (Linux for Ubuntu)
3. Run the provided commands on your EC2 instance one by one

### 7. Set GitHub Secrets

Add the following secrets in your GitHub repository settings:

```
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
AWS_ECR_LOGIN_URI=586723123187.dkr.ecr.ap-southeast-2.amazonaws.com
ECR_REPOSITORY_NAME=kidney
```

---

For more information, see the [MLflow documentation](https://mlflow.org/docs/latest/index.html) and [DagsHub](https://dagshub.com/).
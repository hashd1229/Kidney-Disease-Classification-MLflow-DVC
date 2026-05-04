# Kidney-Disease-Classification-MLflow-DVC


## Workflows

1. Update config.yaml
2. Update secrets.yaml [Optional]
3. Update params.yaml
4. Update the entity
5. Update the configuration manager in src config
6. Update the components
7. Update the pipeline 
8. Update the main.py
9. Update the dvc.yaml
10. app.py

# How to run?
### STEPS:

Clone the repository

```bash
https://github.com/hashd1229/Kidney-Disease-Classification-MLflow-DVC
```
### STEP 01- Create a virtual environment after opening the repository

```bash
python -m venv .venv
```

```bash
.venv/Scripts/activate
```


### STEP 02- install the requirements
```bash
pip install -r requirements.txt
```

## MLflow

- [Documentation](https://mlflow.org/docs/latest/index.html)


##### cmd
- mlflow ui

### dagshub
[dagshub](https://dagshub.com/)

MLFLOW_TRACKING_URI=https://dagshub.com/YOUR_PROJECT_NAME.mlflow \
MLFLOW_TRACKING_USERNAME=USERNAME \
MLFLOW_TRACKING_PASSWORD=PASSWORD \
python script.py

Run this to export as env variables:

```bash

$env:MLFLOW_TRACKING_URI=https://dagshub.com/USERNAME/YOUR_PROJECT_NAME.mlflow

$env:MLFLOW_TRACKING_USERNAME=USERNAME 

$env:MLFLOW_TRACKING_PASSWORD=YOUR_TOKEN

```

###DVC cmd

1. dvc init
2. dvc repro
3. dvc dag
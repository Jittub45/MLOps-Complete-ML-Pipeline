# MLOps-Complete-ML-Pipeline

## 📌 Overview
This repository provides a complete MLOps pipeline setup for managing machine learning workflows efficiently. It includes:
- Data Version Control (DVC) for experiment tracking and data versioning.
- DVC Live for monitoring and logging metrics.
- AWS S3 Integration for remote storage.
- End-to-end ML pipeline automation with `dvc.yaml`.

# MLOps-Complete-ML-Pipeline

## 📌 Overview
This repository provides a complete MLOps pipeline setup for managing machine learning workflows efficiently. It includes:
- Data Version Control (DVC) for experiment tracking and data versioning.
- DVC Live for monitoring and logging metrics.
- AWS S3 Integration for remote storage.
- End-to-end ML pipeline automation with `dvc.yaml`.


## 🛠 Tech Stack & Tools Used
- Languages: Python
- ML Tools: Scikit-learn, NumPy, Pandas
- Experiment Tracking: MLflow, DVCLive
- Version Control: DVC, GitHub
- Remote Storage: AWS S3, DagsHub
- Deployment: *(Planned for future work)*


## 📂 Project Structure
```
MLOps-Complete-ML-Pipeline/
│── .dvc/                   # DVC metadata
│── dvclive/                # Experiment tracking with dvclive
│── experiments/            # ML pipeline components
│── src/                    # Source code
│── .dvcignore              # DVC ignore file
│── .gitignore              # Git ignore file
│── dvc.lock                # DVC lock file
│── dvc.yaml                # DVC pipeline configuration
│── params.yaml             # Parameters for pipeline execution
│── projectFlow.txt         # Project workflow description
│── README.md               # Project documentation (this file)
│── LICENSE                 # License file
```

## 🚀 Getting Started

1️⃣ Clone the Repository
```bash
git clone https://github.com/Jittub45/MLOps-Complete-ML-Pipeline.git
cd MLOps-Complete-ML-Pipeline
```

2️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

3️⃣ Initialize DVC
```bash
dvc init
git add .dvc .dvcignore
git commit -m "Initialized DVC"
```

## 📌 Setting Up DVC Pipeline

1️⃣ Define Pipeline Stages
Modify `dvc.yaml` to define all stages:
```yaml
stages:
  data_ingestion:
    cmd: python src/data_ingestion.py
    deps:
      - src/data_ingestion.py
    outs:
      - data/raw_data.csv

  feature_engineering:
    cmd: python src/feature_engineering.py
    deps:
      - src/feature_engineering.py
      - data/raw_data.csv
    outs:
      - data/processed_data.csv

  model_training:
    cmd: python src/model_training.py
    deps:
      - src/model_training.py
      - data/processed_data.csv
    outs:
      - models/model.pkl
```

2️⃣ Run DVC Pipeline
```bash
dvc repro
```
Check DAG visualization:
```bash
dvc dag
```

## 🎯 Experiment Tracking with DVC Live

1️⃣ Install DVC Live
```bash
pip install dvclive
```

2️⃣ Modify `main.py`
Add experiment tracking with DVC Live:
```python
from dvclive import Live
import yaml

params = yaml.safe_load(open('params.yaml'))
with Live(save_dvc_exp=True) as live:
    live.log_metric('accuracy', accuracy)
    live.log_metric('precision', precision)
    live.log_metric('recall', recall)
    live.log_params(params)
```

3️⃣ Run Experiments
```bash
dvc exp run
```
Show experiment results:
```bash
dvc exp show
```

## 🌐 Setting Up Remote S3 Storage

1️⃣ Install Dependencies
```bash
pip install dvc[s3] awscli
```

2️⃣ Configure AWS Credentials
```bash
aws configure
```

3️⃣ Add Remote Storage
```bash
dvc remote add -d dvcstore s3://your-bucket-name
```

4️⃣ Push DVC Artifacts
```bash
dvc commit
```
```bash
dvc push
```

## 📈 Tracking Experiments
To remove an experiment:
```bash
dvc exp remove <exp-name>
```
To apply a previous experiment:
```bash
dvc exp apply <exp-name>
```

## 📌 Conclusion
This project provides a structured ML pipeline with DVC for data versioning, DVC Live for experiment tracking, and AWS S3 for cloud storage. This ensures reproducibility, scalability, and efficient ML workflow management.

## 🔗 Repository Link
[GitHub - MLOps-Complete-ML-Pipeline](https://github.com/Jittub45/MLOps-Complete-ML-Pipeline)

## 📜 License
This project is licensed under the MIT License.




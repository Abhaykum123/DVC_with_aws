# ML_pipeline_using_DVC

A structured machine learning pipeline using **DVC (Data Version Control)** to enable reproducible, versioned data processing, experimentation, and model training.

---

## 🚀 Overview

This repository demonstrates how to build a **reproducible ML pipeline** leveraging DVC for data versioning and experiment tracking. It includes:

- A DVC pipeline orchestrated through `dvc.yaml` and parameterized via `params.yaml`.
- Reproducible stages including data transformation, splitting, training, and evaluation.
- Experiment tracking using DVC’s cache, `dvc.lock`, and optionally DVCLive for metrics.

---

## 📂 Project Structure
``
.dvc/
experiments/
src/
.dvcignore
.gitignore
LICENSE
README.md
dvc.yaml
dvc.lock
params.yaml
``

| Item             | Description |
|------------------|-------------|
| `.dvc/`          | DVC’s internal metadata directory. |
| `experiments/`   | (Optional) directory for experiment outputs. |
| `src/`           | Source code, including stages, pipelines, and utilities. |
| `.dvcignore`, `.gitignore` | Files/directories excluded from DVC/Git. |
| `dvc.yaml`       | Definitions of pipeline stages with dependencies, commands, params, outputs. |
| `params.yaml`    | Configuration of hyperparameters and settings for reproducibility. |
| `dvc.lock`       | Auto-generated lock file capturing execution state and hashes. |
| `LICENSE`        | MIT License. |
| `README.md`      | This document. |

---

## ⚙️ Getting Started

### Prerequisites

Ensure you have the following installed:

- Python (3.8+ recommended)
- Git
- DVC (`pip install dvc` or include in `requirements.txt` within `src/`)

Optionally, for remote storage support (e.g., AWS S3):

```bash
pip install "dvc[s3]"
```
---------------------

## Setup Instructions
```base
# Clone the repository
git clone https://github.com/Abhaykum123/ML_pipeline_using_DVC.git
cd ML_pipeline_using_DVC

# Initialize DVC (if not already initialized)
dvc init

# Install dependencies
pip install -r src/requirements.txt
```
# 🔄 Pipeline Workflow

## Stages

### 1. Transform  
- Data preprocessing  
- Patchifying  
- Splitting  
- Cleansing from raw data  

---

### 2. Split  
- Partitioning transformed data into:  
  - Training set  
  - Validation set  
  - Test set  

---

### 3. Train  
- Model training using configurable hyperparameters such as:  
  - Epochs  
  - Learning rate  
  - Batch size  

---

### 4. Evaluate  
- Model evaluation  
- Metric logging (e.g., `metrics.json`) for tracking performance  

---

### 5. (Optional) DVCLive / Experiment Tracking  
- Logging and visualizing metrics across experiments  
- Tracking changes in hyperparameters and datasets  

###
```
dvc repro
```
DVC automatically reruns only the stages where dependencies or parameters have changed.

##Experimentation
1. Edit parameters in `params.yaml`
2. Re-run:
 ```dvc repro```
3. Compare metrics:
 ```dvc metrics show -T ```
4. Commit and tag:
 ```
git add .
git commit -m "Experiment: [description]"
git tag -a exp-name -m "Experiment description"
```
### Visualize DAG
``` dvc dag ```

# 🗂️ Versioning & Storage

- **Git** stores lightweight metafiles (`dvc.yaml`, `dvc.lock`, `.dvcignore`, etc.).  
- **DVC cache** stores actual data and model artifacts.  
- Use `dvc push` / `dvc pull` to sync data with remote storage (e.g., AWS S3, GCP, Azure).  

---

# 💡 Tips & Best Practices

- Always **commit `dvc.lock`** to Git to keep track of pipeline state.  
- **Parameterize** hyperparameters in `params.yaml` for easy experimentation.  
- Use **DVCLive** or **DVC metrics** to log metrics and compare runs.  
- Optionally, **containerize the pipeline with Docker** for cross-environment reproducibility.  

## 📜 License
Distributed under the MIT License.

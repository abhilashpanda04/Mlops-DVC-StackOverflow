# DVC NLP Pipeline: Stack Overflow Tag Classifier

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![DVC](https://img.shields.io/badge/tool-DVC-blue)](https://dvc.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> *"In Machine Learning, tracking code is easy. Tracking data, models, and parameters is the real challenge."*

Welcome to my Data Version Control (DVC) project. I built this repository to demonstrate how to achieve **100% reproducible Machine Learning pipelines** for Natural Language Processing (NLP). 

This project trains a text classification model to predict tags for Stack Overflow questions. However, the focus isn't just on the NLP model—it's on the infrastructure that tracks the data, parameters, metrics, and pipeline execution.

---

## Why I Built This

A common anti-pattern in data science is running a Jupyter notebook, tweaking some parameters, saving a model as `model_final_v3.pkl`, and completely losing track of which data or parameters generated that model.

I built this project to solve that exact problem using [DVC (Data Version Control)](https://dvc.org/). By exploring this repository, you'll see:

1. **Data Versioning**: The raw XML dataset, intermediate TSV files, and final Pickle models are tracked via DVC. They are tied to Git commits but stored externally (Google Drive).
2. **Pipeline Orchestration**: The entire workflow is mapped out in `dvc.yaml`. If a parameter changes, DVC intelligently knows exactly which steps need to be re-run and which can be cached.
3. **Parameter Tracking**: Hyperparameters are centralized in `params.yaml`. Changing a random seed or an n-gram size automatically invalidates the downstream DVC cache.
4. **Metrics & Plots Tracking**: Model evaluation produces `scores.json`, `prc.json`, and `roc.json`, which DVC uses to track performance metrics and visualize ROC/PRC curves directly from the CLI.

---

## How It Works (The Architecture)

The project is structured into modular stages, orchestrated by DVC:

```text
Mlops-DVC-StackOverflow/
├── src/
│   ├── stage_01_get_data.py       ← Downloads XML dataset from Google Drive
│   ├── stage_02_prepare.py        ← Parses XML and splits into train/test TSVs
│   ├── stage_03_featurization.py  ← TF-IDF Vectorization (n-grams, max features)
│   ├── stage_04_train.py          ← Trains the RandomForest classifier
│   ├── stage_05_evaluate.py       ← Evaluates metrics and outputs JSON plots
│   └── utils/                     ← Helper functions
├── configs/
│   └── config.yaml                ← Static file paths and URLs
├── params.yaml                    ← Dynamic hyperparameters (split, n_est, seed)
├── dvc.yaml                       ← The DAG defining inputs, outputs, and dependencies
└── pyproject.toml                 ← Dependency management via uv
```

### The Pipeline Flow (`dvc.yaml`)

When you run the pipeline, DVC executes the Directed Acyclic Graph (DAG):

```text
[get_data] ──→ [prepare_data] ──→ [featurize] ──→ [train] ──→ [evaluate]
```

If you modify `params.yaml` to change the `train.n_est` (number of estimators), DVC knows that `get_data`, `prepare_data`, and `featurize` are unaffected. It will **only** re-run `train` and `evaluate` from cache.

---

## Tech Stack

- **Orchestration & Data Versioning**: DVC (Data Version Control)
- **Package Management**: [uv](https://github.com/astral-sh/uv) 
- **ML Framework**: Scikit-Learn
- **Data Processing**: Pandas, NumPy
- **Remote Storage**: Google Drive (`dvc[gdrive]`)

---

## Getting Started

Want to run this pipeline locally? I've streamlined the setup to take less than a minute.

### 1. Installation

This project uses `uv` for incredibly fast dependency management.

```bash
# Clone the repository
git clone https://github.com/abhilashpanda04/Mlops-DVC-StackOverflow.git
cd Mlops-DVC-StackOverflow

# Install dependencies and create a virtual environment instantly
uv sync

# Activate the virtual environment
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 2. Execute the Pipeline

Run the entire pipeline from start to finish. DVC will download the data, process it, train the model, and evaluate it:

```bash
dvc repro
```

### 3. Visualize the DAG

You can view the execution graph and dependencies directly in your terminal:

```bash
dvc dag
```

### 4. View Metrics & Plots

Check the performance of the trained model:

```bash
# View scalar metrics (Accuracy, F1, etc.)
dvc metrics show

# Generate and view plots (requires a browser/HTML viewer)
dvc plots show
```

---

## Contributing & Feedback

If you're interested in Data Engineering, MLOps, or have feedback on this DVC implementation, I'd love to connect! Feel free to open an issue, submit a PR, or reach out directly.

## About Me

**Abhilash Kumar Panda**
- Email: abhilashk.isme1517@gmail.com
- LinkedIn: [Abhilash Kumar Panda](https://www.linkedin.com/in/abhilash-kumar-panda/)
- Portfolio: [abhilashpanda04.github.io](https://abhilashpanda04.github.io/Portfolio_site/)
- GitHub: [@abhilashpanda04](https://github.com/abhilashpanda04)

---
*If you found this architecture helpful or interesting, please consider giving the repo a star!*

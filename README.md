# DVC NLP UseCase - Stack Overflow

[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![DVC](https://img.shields.io/badge/tool-DVC-blue)](https://dvc.org/)
[![MLOps](https://img.shields.io/badge/approach-MLOps-green)](https://mlops.community/)

NLP project demonstrating MLOps best practices using DVC for data versioning and experiment tracking with Stack Overflow data.

## Overview

This project showcases how to implement DVC for data versioning and experiment tracking in an NLP pipeline with reproducible ML workflows.

## Features

- DVC Pipeline Orchestration
- Data Versioning
- Experiment Tracking
- Metrics Management
- Reproducible Workflows
- Remote Storage Support

## Tech Stack

- Framework: DVC, Python
- Language: NLP with scikit-learn
- Data: Stack Overflow dataset

## Installation

```bash
git clone https://github.com/abhilashpanda04/Mlops-DVC-StackOverflow.git
cd Mlops-DVC-StackOverflow

conda create --prefix ./env python=3.7 -y
conda activate ./env
pip install -r requirements.txt
dvc init
```

## Usage

```bash
# Run pipeline
dvc repro

# View pipeline
dvc dag

# Show metrics
dvc metrics show
```

## License

MIT License

## Author

Abhilash Kumar Panda
- Email: abhilashk.isme1517@gmail.com
- LinkedIn: https://www.linkedin.com/in/abhilash-kumar-panda/

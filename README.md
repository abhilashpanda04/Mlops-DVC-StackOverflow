# DVC-NLP-USECASE

This project demonstrates the use of DVC (Data Version Control) for an NLP use case. DVC helps manage and track large datasets and machine learning models, making it easier to collaborate and reproduce experiments.

## Getting Started

Follow these steps to set up and run the project on your local machine.

### Prerequisites

* Git
* Conda (or Miniconda)

### Steps

1. **Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/dvc-project-template.git
   cd dvc-project-template
   ```
2. **Create a conda environment:
```bash
conda create --prefix ./env python=3.7 -y
conda activate ./env
```
3. Install project dependencies:
```bash
pip install -r requirements.txt
```
4. **Initialize DVC:
```bash
dvc init
```
5. **Commit and push changes (if you've made any):
```bash
git add .
git commit -m "Initialize DVC"
git push origin main
```
6. **Reproducing the Results
```bash
dvc repro
```

DVC Studio

You can also visualize and track your experiments using DVC Studio:

[https://studio.iterative.ai/](https://studio.iterative.ai/)

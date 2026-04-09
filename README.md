# Astronomical Clustering Project: Grader Run Guide

## Final Result (Key Outcome)

The final model for this project is **Spectral Clustering**, which achieved an accuracy of **97.9681%**.
This indicates that the model performs very well and that the full pipeline produces strong clustering quality for distinguishing STAR, GALAXY, and QSO classes.

### Preworkflow Baseline (V6)

As an earlier discovery/preworkflow stage, the first **K-Means model on pure physics-informed features** in `extra folder/V6.ipynb` also produced a strong result with **97.84%** overall accuracy.
This is slightly lower than the final Spectral Clustering model (difference: **0.1281 percentage points**), and it helped validate that the physics-based feature direction was already effective before the final model refinement.

This README explains exactly how to open and run this project in a clean environment.

## Workflow Scope Clarification (Important for Grading)

- `code.ipynb` is the **main, complete workflow notebook**. It includes the introduction, physics/background context, EDA, feature engineering/analysis, and clustering model building/evaluation.
- `model.ipynb` is a **separated modeling-focused version** for convenience, mainly to run and review model-related steps.
- For full context and the complete end-to-end work, graders should prioritize reviewing and running `code.ipynb`.

## 1. Files to Include for Submission

Required files:

1. `code.ipynb`
2. `model.ipynb`
3. `star-galaxy-quasar.csv`

Strongly recommended files (lets grader run the modeling notebook immediately without rerunning full preprocessing):

1. `star-galaxy-quasar_processed.csv`
2. `star-galaxy-quasar_featured.csv`

## 2. Python Environment

Recommended:

- Python 3.10-3.13
- VS Code with Jupyter extension

Create and activate a virtual environment from the project root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell execution policy blocks activation, run in Command Prompt:

```cmd
.venv\Scripts\activate.bat
```

## 3. Install Dependencies

Install required packages:

```powershell
pip install pandas numpy matplotlib seaborn scikit-learn umap-learn hdbscan jupyter ipykernel
```

Note:

- `hdbscan` is optional in code logic (the notebook skips HDBSCAN sections if unavailable), but installing it is recommended for full output parity.

## 4. Run Order (Important)

### Option A: Full pipeline from raw data (recommended for grading)

1. Open `code.ipynb`
2. Set notebook kernel to the created `.venv`
3. Run all cells from top to bottom
4. Confirm generated files exist:
	- `star-galaxy-quasar_processed.csv`
	- `star-galaxy-quasar_featured.csv`
5. Open `model.ipynb`
6. Run all cells from top to bottom

### Option B: Run modeling only

If `star-galaxy-quasar_featured.csv` already exists, you can run only:

1. `model.ipynb` (Run All)

The notebook is set to load:

1. `star-galaxy-quasar_featured.csv` first
2. falls back to `star-galaxy-quasar_processed.csv` if needed

## 5. Expected Outputs

When run successfully, grader should see:

1. Feature engineering and EDA plots from `code.ipynb`
2. Clustering metrics/tables (Silhouette, AMI, ARI, NMI) in `model.ipynb`
3. Confusion matrices and post-hoc model comparison visualizations

## 6. Common Issues and Fixes

### Issue: `FileNotFoundError` for dataset CSV

Fix:

1. Ensure notebook working directory is the project root.
2. Ensure required CSV files are in the same folder as notebooks.

### Issue: `No module named umap` or `No module named hdbscan`

Fix:

```powershell
pip install umap-learn hdbscan
```

### Issue: Wrong kernel selected

Fix:

1. In VS Code notebook toolbar, click Kernel.
2. Select Python interpreter from `.venv`.
3. Restart kernel and run all cells again.

## 7. Reproducibility Notes

The notebooks set fixed random seeds (for example, `random_state=42`) in major modeling steps to keep results stable across runs.

## 8. Quick Grader Checklist

1. Open project folder in VS Code.
2. Create/activate `.venv`.
3. Install packages.
4. Run `code.ipynb` (Run All).
5. Run `model.ipynb` (Run All).
6. Verify tables/plots render without errors.

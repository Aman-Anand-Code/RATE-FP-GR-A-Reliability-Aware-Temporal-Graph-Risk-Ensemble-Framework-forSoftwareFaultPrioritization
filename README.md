# RATE-FP-GR: A Reliability-Aware Temporal Graph-Risk Ensemble Framework for Software Fault Prioritization

This repository contains the complete replication package for the paper:

**RATE-FP-GR: A Reliability-Aware Temporal Graph-Risk Ensemble Framework for Software Fault Prioritization**

The proposed framework is designed for class-level software fault prioritization. It combines static software metrics, temporal software-evolution features, GraphSAGE-based graph-risk scores, and imbalance-aware ensemble learning to rank software classes according to their predicted fault risk.

The goal of this repository is to allow researchers, reviewers, and practitioners to reproduce the experiments reported in the paper, including preprocessing, temporal feature extraction, graph construction, GraphSAGE graph-risk modeling, RATE-FP-GR training, and risk-prioritization evaluation.

---

## 1. Repository Contents

The current repository contains the following files:

| File                                       | Description                                                                                                                                                                                                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Notebook_1_01_JDT_Prototype_ipynb.ipynb`  | Prototype notebook for Eclipse JDT Core. It includes early preprocessing, static and temporal baselines, graph construction, GCN/GraphSAGE modeling, adaptive hybrid ensemble evaluation, and figure generation for the JDT case study. |
| `Notebook_2_02_RATE_FP_All_Datasets.ipynb` | Main replication notebook for all five datasets. This notebook reproduces the complete RATE-FP-GR experimental workflow used in the paper.                                                                                              |
| `data-20260518T094405Z-3-001.zip`          | Dataset package used in the experiments. It contains the AEEEM project files for Eclipse JDT Core, Eclipse PDE UI, Equinox Framework, Lucene, and Mylyn.                                                                                |
| `README.md`                                | Reproducibility instructions and repository documentation.                                                                                                                                                                              |
| `LICENSE`                                  | Repository license.                                                                                                                                                                                                                     |

---

## 2. Paper Summary

Software fault prediction is commonly treated as a binary classification problem, where each class is predicted as defective or non-defective. However, in practical software testing, developers often need a ranked list of high-risk classes because only a limited portion of the system can be inspected before release.

RATE-FP-GR addresses this problem by estimating a fault-risk score for each software class and ranking classes according to their predicted risk.

The framework integrates:

1. Static software metrics
2. Historical change metrics
3. Temporal metric-evolution features
4. Class similarity graph construction
5. GraphSAGE-based graph-risk estimation
6. Graph-risk augmented ensemble learning
7. Fault-risk prioritization using F1-score, PR-AUC, Recall@20%, and Lift@20%

---

## 3. Proposed RATE-FP-GR Workflow

The complete pipeline is:

```text
Raw AEEEM project files
        |
        v
Static metric preprocessing
        |
        v
Temporal feature extraction from biweekly histories
        |
        v
Static-temporal feature fusion
        |
        v
Class similarity graph construction
        |
        v
GraphSAGE graph-risk modeling
        |
        v
Graph-risk score generation
        |
        v
Graph-risk augmented ensemble learning
        |
        v
Fault-risk score prediction
        |
        v
Ranked class list for Top-20% fault prioritization
```

---

## 4. Dataset

The experiments use the AEEEM bug prediction benchmark dataset.

The dataset contains class-level software metrics and post-release defect labels for five Java software systems:

| Project           | Classes | Non-defective | Defective | Defect Ratio |
| ----------------- | ------: | ------------: | --------: | -----------: |
| Eclipse JDT Core  |     997 |           791 |       206 |       20.66% |
| Eclipse PDE UI    |    1497 |          1288 |       209 |       13.96% |
| Equinox Framework |     324 |           195 |       129 |       39.81% |
| Lucene            |     691 |           627 |        64 |        9.26% |
| Mylyn             |    1862 |          1617 |       245 |       13.16% |

A class is labeled as defective if its post-release defect count is greater than zero:

```text
is_defective = 1 if bugs > 0
is_defective = 0 otherwise
```

---

## 5. Dataset Package

The dataset package is included as:

```text
data-20260518T094405Z-3-001.zip
```

After extracting the zip file, the expected folders are:

```text
jdt/
pde/
equinox/
lucene/
mylyn/
```

Each project folder should contain the following files:

```text
change-metrics.csv
single-version-ck-oo.csv
biweekly-ck-values.zip
biweekly-oo-values.zip
```

The purpose of each file is:

| File                       | Purpose                                                                                                                                      |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `change-metrics.csv`       | Historical change/process metrics, including versions, fixes, authors, code churn, lines added, lines removed, and post-release bug counts.  |
| `single-version-ck-oo.csv` | Static CK and object-oriented metrics for the target version of each class.                                                                  |
| `biweekly-ck-values.zip`   | Biweekly historical CK metric values such as CBO, DIT, LCOM, NOC, RFC, and WMC.                                                              |
| `biweekly-oo-values.zip`   | Biweekly historical OO metric values such as fan-in, fan-out, number of attributes, number of methods, inherited members, and lines of code. |

---

## 6. Notebooks

### 6.1 `Notebook_1_01_JDT_Prototype_ipynb.ipynb`

This notebook contains the first prototype experiment using Eclipse JDT Core.

It includes:

* loading JDT files,
* cleaning semicolon-separated CSV files,
* merging change metrics and CK/OO metrics,
* creating the binary defect label,
* training static baseline models,
* extracting temporal features,
* training static-temporal models,
* constructing a class similarity graph,
* training GCN/GraphSAGE models,
* generating graph-risk probabilities,
* building the adaptive hybrid ensemble,
* saving result tables and figures.

This notebook is useful for understanding the development of the method on one dataset.

---

### 6.2 `Notebook_2_02_RATE_FP_All_Datasets.ipynb`

This is the main notebook for reproducing the paper results.

It includes:

* loading all five AEEEM datasets,
* preprocessing all projects,
* extracting temporal features from biweekly histories,
* creating static-temporal feature matrices,
* constructing similarity graphs,
* training GraphSAGE models,
* generating graph-risk scores,
* training RATE-FP-GR models,
* comparing static-only, static-temporal, GraphSAGE, and RATE-FP-GR models,
* computing binary classification metrics,
* computing risk-prioritization metrics,
* generating final summary tables.

Use this notebook to reproduce the final results reported in the paper.

---

## 7. Environment

The experiments were originally executed in Google Colab.

Recommended environment:

```text
Python 3.x
Google Colab or Jupyter Notebook
GPU optional but useful for GraphSAGE
```

Main Python libraries:

```text
numpy
pandas
scikit-learn
xgboost
imbalanced-learn
torch
torch-geometric
matplotlib
seaborn
openpyxl
```

---

## 8. Installation

### 8.1 Clone the repository

```bash
git clone https://github.com/Aman-Anand-Code/RATE-FP-GR-A-Reliability-Aware-Temporal-Graph-Risk-Ensemble-Framework-forSoftwareFaultPrioritization.git
cd RATE-FP-GR-A-Reliability-Aware-Temporal-Graph-Risk-Ensemble-Framework-forSoftwareFaultPrioritization
```

### 8.2 Install standard dependencies

```bash
pip install numpy pandas scikit-learn xgboost imbalanced-learn matplotlib seaborn openpyxl
```

### 8.3 Install PyTorch

Install PyTorch based on your system or Colab runtime.

For Google Colab, PyTorch is usually preinstalled. You can verify it using:

```python
import torch
print(torch.__version__)
print(torch.cuda.is_available())
```

### 8.4 Install PyTorch Geometric

In Google Colab, use:

```python
!pip install -q torch-geometric
```

If installation fails, follow the official PyTorch Geometric installation command matching your PyTorch and CUDA version.

---

## 9. How to Reproduce the Complete Paper Results

This section explains the full replication workflow.

### Step 1: Clone or download the repository

Clone the repository or download it as a ZIP file from GitHub.

### Step 2: Extract the dataset package

Extract:

```text
data-20260518T094405Z-3-001.zip
```

After extraction, confirm that the following project folders are available:

```text
jdt/
pde/
equinox/
lucene/
mylyn/
```

Each project folder should contain:

```text
change-metrics.csv
single-version-ck-oo.csv
biweekly-ck-values.zip
biweekly-oo-values.zip
```

### Step 3: Open the main notebook

Open:

```text
Notebook_2_02_RATE_FP_All_Datasets.ipynb
```

in Google Colab or Jupyter Notebook.

### Step 4: Set the dataset path

In Google Colab, mount Google Drive if needed:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Then set the base dataset path in the notebook to the folder where the extracted project folders are located.

Example:

```python
BASE_DIR = "/content/drive/MyDrive/RATE_FP_Project"
DATA_DIR = BASE_DIR + "/data"
```

If the dataset is in the same folder as the notebook, set the path accordingly.

### Step 5: Verify project folders

The notebook should check whether all project folders exist:

```text
jdt      -> exists
pde      -> exists
equinox  -> exists
lucene   -> exists
mylyn    -> exists
```

If any folder is missing, extract the dataset zip again and confirm the folder names.

### Step 6: Run preprocessing cells

Run the preprocessing section of the notebook.

This will:

* read `change-metrics.csv`,
* read `single-version-ck-oo.csv`,
* remove invalid trailing empty columns,
* convert metric columns to numeric values,
* merge static files using `classname`,
* create the binary target column `is_defective`,
* save the cleaned baseline dataset.

Expected output includes dataset shapes similar to:

```text
jdt:      RATE-FP dataset shape: (997, 192)
pde:      RATE-FP dataset shape: (1497, 192)
equinox:  RATE-FP dataset shape: (324, 192)
lucene:   RATE-FP dataset shape: (691, 192)
mylyn:    RATE-FP dataset shape: (1862, 192)
```

### Step 7: Run temporal feature extraction

Run the temporal feature extraction cells.

For each project, the notebook will:

* unzip or read biweekly CK metric histories,
* unzip or read biweekly OO metric histories,
* replace unavailable `-1` values with missing values,
* compute temporal descriptors for each class.

Temporal descriptors include:

```text
mean
standard deviation
minimum
maximum
first valid value
last valid value
growth
change count
trend slope
```

The temporal features are extracted from 17 biweekly metrics.

### Step 8: Create static-temporal dataset

The notebook merges:

```text
static features + temporal features + defect label
```

This creates the final static-temporal dataset for each project.

### Step 9: Run static-only baseline models

Run the static baseline section.

These models use only static CK, OO, and change metrics.

Typical models include:

```text
Logistic Regression
Support Vector Classifier
Decision Tree
Random Forest
Gradient Boosting
KNN
MLP
```

The notebook reports:

```text
accuracy
precision
recall
F1-score
ROC-AUC
training time
```

### Step 10: Run static-temporal baseline models

Run the static-temporal baseline section.

These models use:

```text
static metrics + temporal descriptors
```

This step evaluates whether temporal software-evolution features improve over static-only metrics.

### Step 11: Construct class similarity graphs

Run the graph construction cells.

For each project:

* node = software class,
* node features = static-temporal features,
* edge = top-k cosine similarity,
* k = 10 nearest neighbors.

The graph is used as input to GraphSAGE.

### Step 12: Train GraphSAGE

Run the GraphSAGE section.

GraphSAGE is trained using:

```text
static-temporal node features
class similarity graph
weighted cross-entropy loss
stratified train-validation-test split
```

The model outputs a graph-risk probability for each class:

```text
graph_risk_score = P(class is defective | graph neighborhood + node features)
```

This score is saved and later used as an additional feature.

### Step 13: Train RATE-FP-GR

Run the graph-risk augmented learning section.

The final RATE-FP-GR feature representation is:

```text
static features + temporal features + graph-risk score
```

The notebook trains imbalance-aware models such as:

```text
Extra Trees
Balanced Random Forest
XGBoost
Graph-risk augmented ensemble
```

### Step 14: Run risk-prioritization evaluation

Run the final risk-prioritization section.

This compares:

```text
Static-only baseline
Static + Temporal baseline
GraphSAGE Risk model
RATE-FP-GR
```

The main metrics are:

```text
F1-score
ROC-AUC
PR-AUC
Recall@10%
Recall@20%
Recall@30%
Lift@10%
Lift@20%
Lift@30%
MCC
Balanced Accuracy
```

The main paper uses:

```text
F1-score
PR-AUC
Recall@20%
Lift@20%
```

### Step 15: Save result files

The notebook saves result CSV files. Depending on the execution path, the following files may be generated:

```text
ALL_PROJECTS_RATE_FP_RESULTS.csv
ALL_PROJECTS_RATE_FP_TUNED_RESULTS.csv
GRAPH_RISK_AUGMENTED_ALL_PROJECTS_seed_42.csv
GRAPH_RISK_AUGMENTED_SUMMARY_seed_42.csv
IMBALANCE_AWARE_RATE_FP_GR_seed_42.csv
IMBALANCE_AWARE_RATE_FP_GR_SUMMARY_seed_42.csv
STABILITY_REGULARIZED_RATE_FP_GR_SELECTOR_seed_42.csv
FINAL_STABLE_RATE_FP_GR_COMPARISON_seed_42.csv
RISK_PRIORITIZATION_RESULTS_seed_42.csv
RISK_PRIORITIZATION_SUMMARY_seed_42.csv
```

The most important final file is:

```text
RISK_PRIORITIZATION_SUMMARY_seed_42.csv
```

---

## 10. Expected Final Results

The final risk-prioritization experiment should produce average results close to the following:

| Model             |     F1 | PR-AUC | Recall@20% | Lift@20% |
| ----------------- | -----: | -----: | ---------: | -------: |
| Static-only       | 0.4606 | 0.4568 |     0.4948 |   2.4645 |
| Static + Temporal | 0.4618 | 0.5115 |     0.4918 |   2.4496 |
| GraphSAGE Risk    | 0.4872 | 0.5076 |     0.5402 |   2.6881 |
| RATE-FP-GR        | 0.5039 | 0.5072 |     0.5112 |   2.5463 |

RATE-FP-GR achieves the highest average F1-score.

In the Top-20% inspection setting, RATE-FP-GR identifies more than half of the defective classes on average and achieves approximately 2.55 times higher defect density than random inspection.

---

## 11. Detailed RATE-FP-GR Results

| Project           |     F1 | ROC-AUC | PR-AUC | Recall@20% | Lift@20% |
| ----------------- | -----: | ------: | -----: | ---------: | -------: |
| JDT Core          | 0.6909 |  0.8867 | 0.7561 |     0.6452 |   3.2258 |
| PDE UI            | 0.4333 |  0.8224 | 0.4726 |     0.6129 |   3.0645 |
| Equinox Framework | 0.6522 |  0.7614 | 0.6791 |     0.3158 |   1.5474 |
| Lucene            | 0.2703 |  0.7146 | 0.2117 |     0.3333 |   1.6508 |
| Mylyn             | 0.4727 |  0.8382 | 0.4166 |     0.6486 |   3.2432 |
| Average           | 0.5039 |  0.8047 | 0.5072 |     0.5112 |   2.5463 |

---

## 12. Feature Importance Results

The top static-temporal features contributing to fault prediction are:

| Feature                                 | Importance |
| --------------------------------------- | ---------: |
| `rfc_temp_change_count`                 |     0.0323 |
| `wmc_temp_change_count`                 |     0.0274 |
| `numberOfLinesOfCode_temp_change_count` |     0.0239 |
| `numberOfLinesOfCode_temp_last`         |     0.0223 |
| `wmc_temp_last`                         |     0.0209 |
| `rfc_temp_std`                          |     0.0207 |
| `wmc`                                   |     0.0205 |
| `numberOfLinesOfCode_temp_max`          |     0.0190 |
| `wmc_temp_std`                          |     0.0186 |
| `wmc_temp_first`                        |     0.0176 |

These features suggest that temporal changes in class responsibility, method complexity, and lines of code are important indicators of fault risk.

---

## 13. How to Reproduce the Figures

The notebooks generate figures used in the paper.

Possible generated figures include:

```text
Figure_F1_Model_Comparison_RATE_FP.tiff
Figure_ROC_RATE_FP_Hybrid.tiff
Figure_Confusion_Matrix_RATE_FP.tiff
Figure_Feature_Importance_RATE_FP.tiff
```

To reproduce the figures:

1. Run the notebook sections that save figures.
2. Check the output directory defined in the notebook.
3. Download the generated `.tiff`, `.png`, or `.pdf` files.
4. Use the generated figures in the manuscript.

If a figure is not generated automatically, rerun the figure-generation cell after the corresponding result CSV file has been created.

---

## 14. Troubleshooting

### Problem 1: Dataset folder not found

Check whether the zip file has been extracted correctly.

Expected folders:

```text
jdt/
pde/
equinox/
lucene/
mylyn/
```

If the folders are inside another nested folder, update the dataset path in the notebook.

---

### Problem 2: Biweekly zip files are not extracted

Each project should include:

```text
biweekly-ck-values.zip
biweekly-oo-values.zip
```

The notebook can extract these files. If extraction fails, manually unzip them inside each project folder.

---

### Problem 3: PyTorch Geometric installation error

PyTorch Geometric installation depends on the PyTorch and CUDA version.

In Google Colab, first check:

```python
import torch
print(torch.__version__)
print(torch.version.cuda)
```

Then install the compatible PyTorch Geometric version using the official installation instructions.

A simple Colab command that may work is:

```python
!pip install -q torch-geometric
```

---

### Problem 4: CUDA is not available

GraphSAGE can run on CPU, but it may be slower.

Check device:

```python
import torch
device = "cuda" if torch.cuda.is_available() else "cpu"
print(device)
```

If CUDA is not available in Colab:

```text
Runtime -> Change runtime type -> Hardware accelerator -> GPU
```

Then rerun the notebook from the environment setup cells.

---

### Problem 5: Results are slightly different

Small differences may occur due to:

```text
random seed
package versions
CPU/GPU differences
train-validation-test split
threshold selection
```

The reported paper results use stratified train-validation-test splitting and validation-based threshold tuning.

---

## 15. Notes on Reproducibility

* The experiments were originally run in Google Colab.
* The main notebook is `Notebook_2_02_RATE_FP_All_Datasets.ipynb`.
* GPU acceleration is useful for GraphSAGE but not mandatory for traditional ML baselines.
* The final paper results are based on stratified training, validation, and testing splits.
* The validation set is used for threshold tuning and model selection.
* The test set is used only for final evaluation.
* Minor numerical variations may occur depending on runtime and package versions.

---

## 16. Citation

If you use this repository or reproduce the experiments, please cite:

```bibtex
@article{anand2026ratefpgr,
  title={RATE-FP-GR: A Reliability-Aware Temporal Graph-Risk Ensemble Framework for Software Fault Prioritization},
  author={Anand, Aman},
  journal={Submitted to Science of Computer Programming},
  year={2026}
}
```

---

## 17. License

This repository is released under the MIT License.

See the `LICENSE` file for details.

---

## 18. Contact

For questions about the replication package, please contact:

**Aman Anand**
GitHub: [Aman-Anand-Code](https://github.com/Aman-Anand-Code)

---

## 19. Repository Link

Public replication package:

```text
https://github.com/Aman-Anand-Code/RATE-FP-GR-A-Reliability-Aware-Temporal-Graph-Risk-Ensemble-Framework-forSoftwareFaultPrioritization
```

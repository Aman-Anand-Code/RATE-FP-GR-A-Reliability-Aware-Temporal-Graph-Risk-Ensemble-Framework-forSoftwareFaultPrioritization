# RATE-FP-GR: A Reliability-Aware Temporal Graph-Risk Ensemble Framework for Software Fault Prioritization

This repository contains the replication package for the paper:

**RATE-FP-GR: A Reliability-Aware Temporal Graph-Risk Ensemble Framework for Software Fault Prioritization**

The study proposes a class-level software fault prioritization framework that combines static software metrics, temporal software-evolution features, GraphSAGE-based graph-risk scores, and imbalance-aware ensemble learning. The goal is to rank software classes according to predicted fault risk so that testing teams can prioritize high-risk classes under limited inspection budgets.

---

## Repository Contents

The current repository contains the following files:

| File | Description |
|---|---|
| `Notebook_1_01_JDT_Prototype_ipynb.ipynb` | Prototype notebook for Eclipse JDT Core experiments. It includes early preprocessing, baseline models, GraphSAGE modeling, adaptive hybrid ensemble evaluation, and figure generation for the JDT case study. |
| `Notebook_2_02_RATE_FP_All_Datasets.ipynb` | Main notebook for all five AEEEM datasets. It includes preprocessing, temporal feature extraction, graph construction, GraphSAGE risk-score generation, RATE-FP-GR training, and final risk-prioritization evaluation. |
| `data-20260518T094405Z-3-001.zip` | Dataset package used for the experiments. It contains the AEEEM project files for JDT, PDE, Equinox, Lucene, and Mylyn. |
| `README.md` | Reproducibility instructions and repository description. |
| `LICENSE` | Repository license. |

---

## Overview of RATE-FP-GR

RATE-FP-GR is designed for software fault prioritization rather than only binary defect classification. The framework estimates a fault-risk score for each software class and ranks classes according to predicted risk.

The main workflow is:

1. **Static metric preprocessing**  
   CK metrics, object-oriented metrics, and change metrics are cleaned and merged at class level.

2. **Temporal feature extraction**  
   Biweekly metric histories are converted into temporal descriptors such as mean, standard deviation, growth, change count, and trend slope.

3. **Class similarity graph construction**  
   Software classes are represented as graph nodes. Edges are constructed using top-k cosine similarity over static-temporal feature vectors.

4. **GraphSAGE graph-risk modeling**  
   A GraphSAGE model learns neighborhood-aware defect-risk information and generates a graph-risk score for each class.

5. **Graph-risk augmented learning**  
   The graph-risk score is appended to the static-temporal feature vector and used by imbalance-aware ensemble models.

6. **Fault-risk prioritization**  
   Classes are ranked by predicted risk and evaluated using F1-score, PR-AUC, Recall@20%, and Lift@20%.

---

## Dataset

The experiments use the AEEEM bug prediction benchmark dataset.

The dataset contains class-level software metrics and post-release defect labels for five Java software systems:

| Project | Classes | Non-defective | Defective | Defect Ratio |
|---|---:|---:|---:|---:|
| Eclipse JDT Core | 997 | 791 | 206 | 20.66% |
| Eclipse PDE UI | 1497 | 1288 | 209 | 13.96% |
| Equinox Framework | 324 | 195 | 129 | 39.81% |
| Lucene | 691 | 627 | 64 | 9.26% |
| Mylyn | 1862 | 1617 | 245 | 13.16% |

A class is labeled as defective if its post-release defect count is greater than zero.

---

## Dataset Package

The dataset package is provided as:

```text
data-20260518T094405Z-3-001.zip

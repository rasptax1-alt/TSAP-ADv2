# TSAP-AD: Time-Series Additive exPlanations for Intrusion Detection

This repository contains the official open-source implementation for (TSAP-AD), a leakage-controlled, explainable intrusion detection framework designed for resource-constrained Industrial Internet of Things (IIoT) edge gateways. 

TSAP-AD integrates a (leakage-controlled pseudo-chronological evaluation protocol), a (Numba-JIT dynamic time warping (DTW) abstraction layer), and a linear-time (Signed Net-Deviation Attribution (SNDA)) explainer.

---

## 📌 Repository Structure

```text
TSAP.AD/
├── README.md                      # Repository instructions & replication guide
├── requirements.txt               # Environment dependencies
├── src/
│   ├── dtw_numba.py               # Sakoe-Chiba band Numba-JIT DTW abstraction
│   ├── pipeline.py                # Execution pipeline controller
│   ├── preprocessing.py           # Pseudo-chronological windowing & purger
│   └── snda_explainer.py          # Linear O(M) SNDA attribution engine
├── notebooks/
│   ├── 01_pseudo_chronological_v6.ipynb # Replicates Tables 3–6 (Detection & Latency)
│   └── 02_dtw_validity_v7.ipynb        # Replicates v7 DTW mathematical & L2 equivalence
└── results/
    ├── TSAP_v6_results.json       # Aggregated cross-validation metrics
    ├── v6_detection_runs.csv      # Per-fold detection metrics (balanced vs. natural)
    ├── v6_explanation_runs.csv    # SNDA vs. TreeSHAP fidelity & Q-score evaluations
    ├── v6_lstm_runs.csv           # Stratified LSTM baseline training logs
    └── v7_dtw_validity.csv        # Empirical proof of DTW reduction to L2 norm


Quick Start & Installation
1. Prerequisites
Python 3.9 or higher

C++ compiler support (required for Numba JIT compilation)

2. Environment Setup:
# Clone or download the repository
cd TSAP.AD

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate

# Install required dependencies
pip install -r requirements.txt


Replicating Paper Experiments
1. Detection Performance & Latency Benchmarks (Tables 3–6)To replicate the stratified pseudo-chronological cross-validation (B_1, A_1, \dots, B_6, A_6) and micro-benchmarking latency profiles:Open and run notebooks/01_pseudo_chronological_v6.ipynb.
2. DTW Validity & Feature Redundancy Analysis (v7 Analysis)To execute the empirical validation proving that DTW distance against a benign reference reduces to the window L_2 norm (R^2 = 0.9963 relative to rolling statistics):Open and run notebooks/02_dtw_validity_v7.ipynb.

Summary of Main Results:

Evaluation Metric			TSAP-AD Hybrid	StandaloneXGBoost	LSTMBaseline 
Balanced F_1-score			1.00000		1.00000			0.58255
Natural Prevalence PR-AUC		0.783839	0.432315		0.487410
Natural Prevalence FPR    		0.001921	0.003439		0.034453
Edge Gateway Processing Footprint 	3.1119ms	0.9846ms		14.2800ms




License
This project is submitted for open-access publication under the terms and conditions of the Creative Commons Attribution (CC BY) license.


# FedShield-IoT-Security
Code and experimental results for federated learning IDS in IoT


# FedShield: Federated Learning-Based Intrusion Detection System For Secure IoT Networks
<img width="2143" height="123" alt="image" src="https://github.com/user-attachments/assets/ba7c62f6-cc8a-43ec-888b-7fc5583f14c5" />


[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**FedShield** is a privacy-preserving, decentralized Intrusion Detection System (IDS) framework designed for highly heterogeneous Internet of Things (IoT) networks. This repository contains the proof-of-concept code, experiments, and results for our 2026 research paper evaluated on the **CIC-IoT-2023** dataset.

---

## 📌 Research Motivation & The Trilemma
Traditional cloud-based IDS architectures require massive streams of raw packet telemetry, causing severe bandwidth bottlenecks and unacceptable privacy violations (GDPR non-compliance). While Federated Learning (FL) solves the privacy issue, it introduces two major roadblocks in practical IoT environments:
1. **The Non-IID Failure:** Standard FL (FedAvg) crashes when exposed to authentic, highly skewed (Non-IID) edge data.
2. **The Black-Box Trust Gap:** Deep learning models cannot explain *why* they flagged a threat, preventing Security Operations Centers (SOC) from safely deploying automated mitigations.

**FedShield solves this trilemma by synthesizing:**
* **Data Localization:** Raw data never leaves the edge node.
* **FedProx Optimization:** A proximal penalty algorithm that stabilizes training across severe Dirichlet ($\alpha=0.5$) data skews.
* **SHAP Integration:** Post-hoc Explainable AI (XAI) that provides feature-level attribution for every detected anomaly.

---

## 📊 Dataset & Simulation Environment
* **Dataset:** [CIC-IoT-2023](https://www.unb.ca/cic/datasets/iotdataset-2023.html) (Canadian Institute for Cybersecurity).
* **Classes:** 34 distinct network traffic profiles (Benign + 33 modern attack vectors including Mirai, DDoS, DoS, and Spoofing).
* **Heterogeneity Simulation:** Data was partitioned across 5 simulated edge clients using a **Dirichlet Distribution ($\alpha=0.5$)** to enforce severe class imbalance.

---

## ⚙️ Architecture Highlights
* **IDSNet (Local Model):** A highly optimized, lightweight Deep Neural Network (~90k parameters) designed for resource-constrained edge execution, featuring Batch Normalization and Dropout for localized regularization.
* **Aggregation Engine:** Implements **FedProx** ($\mu=0.01$) to mathematically tether localized gradients to the global consensus, preventing catastrophic weight divergence (client drift).

---

## 🚀 Key Results (35 Global Rounds)

Despite the punishing Non-IID constraints, FedShield achieved state-of-the-art stability and diagnostic performance without ever centralizing raw telemetry.

| Metric | Peak Performance |
| :--- | :--- |
| **Global Test Accuracy** | 91.81% |
| **Weighted F1-Score** | 0.9089 |
| **Weighted Precision** | 0.9131 |
| **Macro AUC-ROC** | **0.9961** |
| **Convergence Time** | ~55.5 Minutes (T4 GPU) |

### Visual Proof of Efficacy
*(Note: You can view full-resolution outputs in the `results/` directory).*

**1. Convergence Stability (FedProx in Action)** The proximal penalty successfully smoothed out the chaotic oscillations typically triggered by extreme data skew.  
*(Insert your convergence graph here: `![Convergence](results/02_fl_convergence.png)`)*

**2. Explainable AI (SHAP)** Deconstructing the network's internal logic to prove decisions are based on authentic network behaviors (e.g., anomalous packet arrival intervals) rather than statistical noise.  
*(Insert your SHAP beeswarm here: `![SHAP](results/06_shap_beeswarm.png)`)*

---

## 🛠️ Usage & Installation

### Option 1: Run in Google Colab (Recommended)
The easiest way to replicate these results is to run the pipeline directly in Google Colab.
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](Link_To_Your_Colab_Notebook)

### Option 2: Local Execution
1. Clone the repository:
   ```bash
   git clone [https://github.com/YourUsername/FedShield-IoT-Security.git](https://github.com/YourUsername/FedShield-IoT-Security.git)
   cd FedShield-IoT-Security
DISCLAIMER!
USE OF ANY DOCUMENTS AND CODE OF THIS REPOSITORY WITHOUT PERMISION IS SUBJECT TO COPYRIGHT VIOLATION .

Any kind of taking benefits from the present documentations like manuscript,report, and code without the owner consent may cause IPR protection violation and face legal proceedings.

NOTE: Anyone can take knowledge from the documents and code but don't copy and modify ,also they can contribute for societal advantage to this repository.

# CAUCCES: Risk-Aware Maintenance Scheduling in Water Networks via Digital Twins

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME/REPO_NAME/blob/main/CAUCCES_Digital_Twin_Implementation.ipynb)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Research%20Prototype-orange)

## 📖 Overview

This repository contains the official implementation of the **CAUCCES Framework**, a Cyber-Physical Digital Twin designed for sustainable and risk-aware management of water distribution networks.

The core innovation of this framework is the integration of **Ensemble Forecasting** with a novel **Explainable Confidence Index (ECI)** to drive a **Risk-Aware Constraint Programming (CP)** scheduler. This allows utility operators to dynamically defer non-critical maintenance tasks during periods of high environmental uncertainty (e.g., rapid temperature shifts), ensuring hydraulic stability and minimizing SLA breaches.

> **Note:** Due to data privacy regulations regarding critical infrastructure, this implementation includes a **Synthetic Data Generator** that mathematically mimics the statistical properties (seasonality, temperature correlation, and noise) of the real-world dataset used in the original study (Extremadura, Spain).

---

## 🚀 Key Features

### 1. Advanced Environmental Forecasting
- **Hybrid Ensemble:** Combines **Prophet** (Trend/Seasonality), **LightGBM** (Tree-based regression), and **LSTM** (Deep Learning for sequential patterns).
- **Feature Engineering:** Implements physics-based environmental features including **Heat Index** (NOAA eq) and **Evapotranspiration (ET)** approximations.

### 2. Explainable Confidence Index (ECI)
A lightweight metric derived from Information Theory to quantify epistemic uncertainty in real-time:
- Uses **Shannon Entropy** to measure model disagreement.
- Uses **Variance** to measure aleatoric uncertainty.
- **Outcome:** A normalized score $(0, 1)$ representing forecast reliability.

### 3. Risk-Aware Optimization
- **Solver:** Google OR-Tools (CP-SAT).
- **Objective:** Multi-objective optimization minimizing Makespan and Risk.
- **Novelty:** Implements a **Risk Penalty Mechanism** that increases the cost of scheduling tasks during low-ECI windows, effectively pushing maintenance to stable weather windows.

---

## 🛠️ Architecture

The implementation follows the pipeline described in the paper:

1.  **Data Ingestion:** Synthetic generation of Water Consumption ($W_t$), Temperature ($T_{max}, T_{min}$), Precipitation, and Humidity.
2.  **Preprocessing:** Lag generation, Rolling means, and Environmental feature extraction.
3.  **Modeling:** Training of independent forecasters.
4.  **Fusion:** Dynamic weighting based on prediction variance.
5.  **Decision Support:** The Scheduler receives $W_{pred}$ and $ECI_t$ to output an optimal Gantt chart for maintenance crews.

---

## 💻 Installation & Usage

### Method 1: Google Colab (Recommended)
The easiest way to reproduce the results is to click the **Open in Colab** badge at the top of this README. The notebook handles all dependency installations automatically.

### Method 2: Local Execution
1.  Clone the repository:
    ```bash
    git clone [https://github.com/USERNAME/REPO_NAME.git](https://github.com/USERNAME/REPO_NAME.git)
    cd REPO_NAME
    ```
2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3.  Run the notebook via Jupyter Lab or VS Code.

---

## 📊 Requirements

- `numpy` & `pandas`
- `scikit-learn`
- `prophet`
- `lightgbm`
- `tensorflow` (Keras)
- `ortools` (Google Optimization Tools)
- `matplotlib` & `seaborn`

---

## 📜 Citation

If you use this code or the CAUCCES framework in your research, please cite the original paper:

```bibtex
@article{Homaei2024CAUCCES,
  title={Risk-Aware Maintenance Scheduling in Water Networks via Digital Twins},
  author={Homaei, Mohammadhossein and Mogollon-Gutierrez, Oscar and Rezaee, Mostafa and Caro, Andres and Avila, Mar},
  journal={Springer Nature / SN Computer Science},
  year={2024},
  note={Implementation available at GitHub}
}

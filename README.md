# Vanguard IDS

**Network Anomaly Detection and Prediction using Machine Learning (Work in Progress)**

## 🧭 Overview

**Vanguard IDS** is a machine learning–based intrusion detection system designed to simulate a **real-world defensive pipeline** against evolving network threats. Rather than relying on a single, monolithic classifier, Vanguard takes a **modular per-attack approach**, training **dedicated models** for each attack category — starting with **DDoS detection**.

The current implementation focuses on **binary classification (DDoS vs. Benign)** using structured network telemetry (\~22k records). The primary goal is to ensure **detection stability**, **low false positives**, and **deployment readiness** — rather than optimizing for benchmark scores alone.

> This is the foundation for a multi-stage, interpretable intrusion detection framework capable of real-time inference under operational constraints.

### 🔭 Vision & Future Goals

* **Short-term**:
  Build dedicated classifiers for common attack types including:

  * DDoS
  * Port Scanning
  * Infiltration
  * A lightweight anomaly detector for general suspicious behavior

* **Long-term**:

  * Integrate with socket-level traffic streams for **live monitoring**
  * Develop a **two-step detection pipeline** (anomaly → attack classifier) for reduced computation cost
  * Support **API/Docker-based deployment** for real environments

## 🚧 Current Status

* ✅ Binary classification: **DDoS vs. Benign**
* ✅ Achieves **99.9% accuracy** via **Stratified K-Fold Cross-Validation**
* ✅ Uses **Random Forest** as the baseline model
* ⚙️ Per-feature transformation (log-based) for reducing skew and improving stability
* 🔜 Architecture prepared for **per-attack modular expansion**

## 🧠 Machine Learning Pipeline

* **Dataset**:
  Custom subset (\~22,000 records) from **CICIDS2017**, pre-cleaned and balanced

* **Feature Selection**:
  Reduced to high-performing, low-noise numerical features based on correlation and predictive value

* **Model**:
  `RandomForestClassifier` (scikit-learn), tuned for high recall and low false positives

* **Evaluation Strategy**:
  10-Fold **Stratified Cross-Validation**, ensuring no label leakage and consistent performance across folds

* **Model Export**:
  Saved using `joblib` for reproducibility and deployment (`model.pkl`)

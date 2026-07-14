# 🔬 Unified EEG Ablation Study: ASD vs. TD Classification

This repository contains a comprehensive ablation study comparing modern sequence models (Mamba, Transformer) against traditional deep learning baselines (1D-CNN, LSTM, GRU, CNN-LSTM) for the classification of autism spectrum disorder (ASD) vs. typically developing (TD) individuals using EEG data.

## 📋 Project Overview
The study evaluates model performance across two distinct datasets to test generalizability and robustness across varying channel densities and hardware environments.

### **Key Methodology**
- **Epochs:** 50 (Fixed for fair comparison)
- **Input Window:** 256 samples
- **Metrics:** Test Accuracy (%) and ROC-AUC
- **Architecture:** Standardized hidden dimensions ($d_{model}=64$) across all models.

---

## 📊 Comparative Findings

### **Dataset 1: High-Density EEG (64 Channels)**
*Source: 64-channel CSV data — ASD vs. TD*

| Model | Test Accuracy (%) | ROC-AUC |
| :--- | :---: | :---: |
| **Mamba** | **86.32%** | 0.920 |
| **CNN-LSTM** | 86.26% | 0.926 |
| **1D-CNN** | 86.49% | 0.924 |
| **Transformer** | 84.03% | **0.928** |
| **GRU** | 80.60% | 0.912 |
| **LSTM** | 80.60% | 0.918 |

**Finding:** On high-density data, Mamba achieved the highest raw accuracy at 86.32%, while the Transformer demonstrated the best discriminative power via AUC (0.928).

### **Dataset 3: Low-Density EEG (8 Channels + M-CHAT)**
*Source: Raw 8-channel CSVs — ASD vs. Control (Sensor saturation handled via interpolation)*

| Model | Test Accuracy (%) | ROC-AUC |
| :--- | :---: | :---: |
| **Transformer** | **93.36%** | **0.985** |
| **Mamba** | 79.63% | 0.891 |
| **CNN-LSTM** | 78.26% | 0.815 |
| **1D-CNN** | 72.54% | 0.816 |
| **LSTM** | 68.19% | 0.762 |
| **GRU** | 57.67% | 0.661 |

**Finding:** In the low-density/M-CHAT clinical context, the Transformer significantly outperformed all other architectures, achieving near-perfect AUC (0.985).

---

## 📈 Summary of Conclusions
1. **Transformer Superiority in Low-Channel Contexts:** The Transformer model showed exceptional adaptability to the 8-channel dataset, suggesting it effectively captures global dependencies even with limited spatial information.

2. **Mamba Consistency:** Mamba remained a top-tier performer in both scenarios, showing high stability and competitive accuracy (approx. 80-86%) regardless of channel count.

3. **Hybrid Advantages:** The CNN-LSTM hybrid consistently outperformed standalone RNNs (LSTM/GRU), proving that local temporal feature extraction via CNN layers is critical for EEG analysis.

4. **Baseline Performance:** Traditional RNNs (LSTM/GRU) struggled the most with the classification task compared to attention-based or state-space models.

## 🛠️ Environment
- **Framework:** PyTorch
- **Optimization:** Adam Optimizer, Cross-Entropy Loss
- **Features:** Subject-wise Z-score normalization, Sliding-window segmentation, Sensor saturation masking.


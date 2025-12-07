# AI-Driven Process Monitoring & Anomaly Detection (Tennessee Eastman Process)

This project implements a complete unsupervised anomaly detection pipeline for industrial process monitoring using the Tennessee Eastman Process (TEP) benchmark — one of the most widely used datasets for evaluating fault detection systems.

### 🔍 Problem
Industrial plants operate with hundreds of interacting sensor variables. Detecting anomalies early is critical to avoid shutdowns or unsafe conditions. Traditional rule-based approaches fail under noisy, nonlinear conditions.

### 🚀 Solution
I built an end-to-end anomaly detection system using:

- Multivariate sensor preprocessing (52 variables)
- Sliding-window temporal encoding (100-step windows)
- A deep **autoencoder** trained exclusively on fault-free data
- Reconstruction error as anomaly score
- Thresholding via statistical tail analysis
- Visualization of anomaly timelines and error distributions

---

## 📊 Performance

**Overall evaluation on unseen data:**

| Metric | Score |
|--------|-------|
| True-Normal Accuracy | **~97%** |
| Fault Detection Accuracy | **~72%** |
| Average Accuracy | **~84%** |

The model reliably reconstructs normal dynamics and produces significantly higher error on faulty trajectories, demonstrating effective anomaly detection capability even under subsampling constraints.

---

## 🧠 Methodology

1. Loaded 250k samples of fault-free TEP data + millions of faulty samples  
2. Removed label/meta columns (`faultNumber`, `simulationRun`, `sample`)  
3. Standardized 52 sensor variables (`xmeas_*`, `xmv_*`)  
4. Constructed **100-step sliding windows** to capture temporal correlations  
5. Trained a deep autoencoder with a **4-dimensional bottleneck**  
6. Computed reconstruction error on test sets  
7. Selected anomaly threshold using 97th percentile of normal error  
8. Evaluated accuracy on both full and post-fault trajectories  
9. Generated visual diagnostics:
   - Error distribution plot  
   - Faulty trajectory anomaly timeline  

---

## 📈 Visuals

### Reconstruction Error Distribution
*(saved as `reports/error_hist.png`)*

### Faulty Trajectory Anomaly Timeline
*(saved as `reports/fault_error_timeline.png`)*

---

---

## 📝 Key Insight

Even with limited data usage and window-stride sampling (due to memory limits), the autoencoder successfully separates normal and faulty behaviours. This setup mirrors real industrial constraints where full-resolution historical data is not always available.

---

## 🧩 Future Improvements
- LSTM/GRU autoencoder for stronger temporal modeling  
- Variational Autoencoder (VAE) for probabilistic scoring  
- Isolation Forest / PCA baseline comparisons  
- Streamlit dashboard for real-time anomaly monitoring  

---




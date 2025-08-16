# 🚀 LSTM-based Server CPU/Memory Anomaly Detection

## 📌 Overview
This project uses a **Long Short-Term Memory (LSTM) Autoencoder** to detect anomalies in **server performance metrics** such as CPU usage, memory utilization, disk I/O, and system load.  
The system identifies not only **when** an anomaly occurs but also **why** — by analyzing **per-feature contributions** to the anomaly score.  

This approach helps **DevOps teams** and **SREs (Site Reliability Engineers)** predict and prevent server outages, reduce downtime, and ensure system stability.

---

## ✨ Key Features
- **Time-series anomaly detection** using LSTM Autoencoder
- **Per-feature contribution analysis** → explains *why* anomalies occur
- **Multi-feature reason reporting** → lists all features causing anomalies
- **Interactive visualizations** for:
  - Metric trends
  - Anomaly points
  - Feature contribution breakdown
- **Exportable PDF/HTML reports** for presentations or incident reports

---

## 📊 Dataset & Features
The model takes historical server performance logs with features such as:

| Feature Name              | Description |
|---------------------------|-------------|
| `timestamp`               | Time of data collection |
| `load-1m`, `load-5m`, `load-15m` | System load averages over the last 1, 5, and 15 minutes |
| `sys-mem-swap-total`      | Total swap memory available |
| `sys-mem-swap-free`       | Free swap memory |
| `sys-mem-free`            | Free physical memory |
| `sys-mem-cache`           | Cached memory |
| `sys-mem-buffered`        | Buffered memory |
| `sys-mem-available`       | Memory available for applications |
| `sys-mem-total`           | Total physical memory |
| `sys-fork-rate`           | Rate of process creation per second |
| `sys-interrupt-rate`      | CPU interrupts per second |
| `sys-context-switch-rate` | Context switches per second |
| `sys-thermal`             | CPU temperature |
| `disk-io-time`            | Time spent on disk I/O operations |
| `disk-bytes-read`         | Bytes read from disk |
| `disk-bytes-written`      | Bytes written to disk |
| `disk-io-read`            | Disk read operations per second |
| `disk-io-write`           | Disk write operations per second |
| `cpu-iowait`              | CPU time waiting for I/O operations |
| `cpu-system`              | CPU usage by system processes |
| `cpu-user`                | CPU usage by user processes |
| `server-up`               | Uptime indicator (1 = up, 0 = down) |

---

## ⚙️ How It Works
1. **Data Preprocessing**
   - Load and clean server logs
   - Scale features using MinMaxScaler
   - Convert into time windows for sequence learning

2. **Model Architecture**
   - LSTM Autoencoder with:
     - Encoder → Compresses time-series patterns
     - Decoder → Reconstructs original sequence
   - Trained to minimize reconstruction error

3. **Anomaly Detection**
   - Reconstruction error computed per timestamp
   - Per-feature error computed to explain anomalies
   - Features exceeding individual thresholds are flagged as causes

4. **Visualization**
   - Timeline plots with anomaly highlights
   - Bar charts showing per-feature contributions
   - Multi-feature anomaly reports

5. **Reporting**
   - Generate PDF/HTML with:
     - Data overview
     - Anomaly detection plots
     - Feature contribution charts
     - Summary tables

---

## 🚀 Getting Started
### Prerequisites
- Python 3.9+
- TensorFlow / Keras
- NumPy, Pandas
- Matplotlib, Seaborn, Plotly
- Scikit-learn
- ReportLab / WeasyPrint (for PDF/HTML reports)

### Installation
```bash
git clone https://github.com/your-username/lstm-server-anomaly-detection.git
cd lstm-server-anomaly-detection
pip install -r requirements.txt

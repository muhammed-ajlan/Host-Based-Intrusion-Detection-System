# How to Run the code
1. If u want to run it cell wise , then use .ipynb file . This will give u cell wise analysis
2. you can run the whole code at a single time , use .py file

# Host-Based Intrusion Detection System (HIDS) using N-Gram Profiling

An anomaly-based Host-Based Intrusion Detection System (HIDS) designed to monitor host-level activities and detect malicious behaviors by analyzing system call sequences. By shifting away from rigid signature-based detection, this system models normal system behavior to effectively identify novel, zero-day attacks.

## 📌 Project Features
* **Behavioral Fingerprinting:** Utilizes an $n$-gram sliding window ($n=3$) to capture execution context from numeric system call sequences.
* **Anomaly-Based Detection:** Builds a baseline profile of legitimate behavior during training and flags deviations using a calculated anomaly score.
* **Dynamic Thresholding:** Automatically determines the optimal classification threshold using ROC (Receiver Operating Characteristic) curve analysis.
* **Performance Focused:** Engineered for sub-millisecond detection latency with a highly lightweight resource footprint.

## ⚙️ How It Works
The system processes operating system data through a structured 5-stage pipeline:
1. **Data Loading:** Parses system call sequences from the standard **ADFA-LD** (Australian Defence Force Academy Linux Dataset) benchmark.
2. **N-gram Extraction:** Converts raw call sequences into behavioral fingerprints using Python sets for $O(1)$ lookup efficiency.
3. **Profile Building:** Establishes a normal behavior profile using the mathematical union of all training sequences.
4. **Anomaly Scoring:** Evaluates test traces by calculating the fraction of unseen execution patterns:
   $$\text{Anomaly Score} = \frac{\text{Number of } n\text{-grams NOT in Normal Profile}}{\text{Total } n\text{-grams in Trace}}$$
5. **Classification:** Labels the trace as `Normal` or `Attack` based on the optimal threshold that maximizes the difference between TPR and FPR.

## 🛠️ Technology Stack
* **Language:** Python 3.x
* **Machine Learning & Data Processing:** NumPy, Scikit-learn
* **System Monitoring:** `psutil` (used for tracking real-time memory footprint and process overhead)
* **Visualization:** Matplotlib, Seaborn (generates evaluation and performance dashboards)

## 📈 Evaluation Metrics
The project evaluates the system's performance across five core pillars:
* **Detection Accuracy:** Validated using precision, recall, F1-score, and ROC-AUC.
* **Latency:** Measures the end-to-end time required to score and classify individual traces (averaging $< 2\text{ ms}$).
* **System Overhead:** Tracks Resident Set Size (RSS) memory changes to ensure minimal RAM consumption ($< 50\text{ MB}$).

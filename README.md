# 🔍 SSH Log Analysis Tutorial (Python + Jupyter Notebook)

This repository demonstrates how to perform **basic log analysis** on Linux authentication logs (`/var/log/auth.log`) using **Python**, **pandas**, and **Jupyter Notebook**.

It provides a step-by-step tutorial showing how to:
- Parse system log files using regular expressions (regex)
- Identify failed SSH login attempts
- Count and visualize attack sources
- Produce time-series plots of authentication activity

---

## 🧱 Project Structure

```
log-analysis-tutorial/
├── LogAnalysis.ipynb         # Main Jupyter Notebook tutorial
├── auth.log                  # Example SSH authentication log
├── createAuthLog.py          # Synthetic log generator (optional)
├── ssh_auth_agg_api.py       # Example preprocessor/aggregator script
├── assets.csv                # Sample asset inventory (used in enrichment)
└── README.md                 # You are here
```

---

## 🚀 Getting Started

### 1️⃣ Prerequisites

- Python **3.9+**
- Jupyter Notebook or JupyterLab
- Git (to clone the repository)

Install Jupyter if you don’t already have it:
```bash
pip install notebook
```

### 2️⃣ Clone this repository

```bash
git clone https://github.com/<your-username>/log-analysis-tutorial.git
cd log-analysis-tutorial
```

### 3️⃣ Launch the notebook

```bash
jupyter notebook LogAnalysis.ipynb
```

or with JupyterLab:

```bash
jupyter lab LogAnalysis.ipynb
```

---

## 📦 Dependencies

The notebook automatically installs the required libraries:

```python
%pip install pandas matplotlib
```

If you prefer manual installation:
```bash
pip install pandas matplotlib
```

---

## 🧠 What You’ll Learn

- How Linux authentication logs are structured (`/var/log/auth.log`)
- How to extract data using **regex groups**
- How to create a **pandas DataFrame** from unstructured text
- How to analyze failed SSH attempts by:
  - Source IP address  
  - Target hostname  
  - Time of day  
- How to visualize trends with **Matplotlib**

---

## 🧩 The Regex Explained

The notebook uses this expression to capture failed SSH logins:

```python
r"^(?P<month>\w{3})\s+(?P<day>\d{1,2})\s+(?P<time>\d{2}:\d{2}:\d{2})\s+(?P<host>\S+)\s+sshd\[\d+\]:\s+Failed password.*?from\s+(?P<ip>[0-9.]+)"
```

| **Group** | **Captures** | **Example** |
|------------|--------------|--------------|
| `month` | 3-letter month abbreviation | `Sep` |
| `day` | Day of month (1–2 digits) | `4` |
| `time` | Time in `HH:MM:SS` format | `01:12:08` |
| `host` | Hostname of the system | `web01` |
| `ip` | Source IP address | `203.0.113.5` |

Example matched log line:
```
Sep  4 01:12:08 web01 sshd[14321]: Failed password for root from 203.0.113.5 port 53211 ssh2
```

---

## 📊 Example Outputs

- **Top Attacking IPs**
  ![Top IPs](https://user-images.githubusercontent.com/example/top-ips.png)

- **Failed Logins per Host**
  ![Failed per Host](https://user-images.githubusercontent.com/example/failed-hosts.png)

- **Time Series of Failed Attempts**
  ![Timeline](https://user-images.githubusercontent.com/example/timeline.png)

*(Note: The above are placeholder images; real plots render inside the notebook.)*

---

## 🧩 Optional Extensions

You can extend this notebook to:
- Parse *successful* logins (`Accepted password`, `Accepted publickey`)
- Join with `assets.csv` to enrich hosts with owners, environments, or criticality
- Detect brute-force bursts (≥5 attempts in 5 minutes)
- Forward results to a SIEM or Node.js API endpoint

---

## 📚 References

- `/var/log/auth.log` — Linux authentication log file  
- [pandas documentation](https://pandas.pydata.org/docs/)  
- [Python Regular Expressions HOWTO](https://docs.python.org/3/howto/regex.html)  
- [Matplotlib Tutorials](https://matplotlib.org/stable/tutorials/)

---

## 🧑‍💻 Author

**Warren Earle**  
Solent University — Cybersecurity & Networking Projects  
> _“Turning raw log data into readable security insights.”_

---

## 🪄 License

MIT License © 2025 — You’re free to use, modify, and share with attribution.

# 🔋 Battery Health Monitoring System
### AI-Based Online Battery Health & Remaining Useful Life Framework

---

> ## ⚠️ Important Note
>
> **This repository contains only the README file.**
>
> This project was developed during my internship at **Reliance Industries**. Due to Reliance Industries' confidentiality and data privacy policies, the source code, datasets, trained models, and all related files **cannot be made publicly available**.
>
> If you have any queries regarding the project, implementation details, or collaboration opportunities, feel free to reach out directly:
>
> 📧 **Email:** shivamchaturvedi.in@gmail.com


---

## 📌 Project Overview

| Aspect | Details |
|--------|---------|
| **Organization** | Reliance Industries — HMD PT Surat |
| **Purpose** | Real-time ML-based battery health prediction |
| **Datasets** | Li-ion, NiCd, VRLA reference batteries |
| **Models** | Ensemble (Gradient Boosting, Random Forest, XGBoost) |
| **SoH Accuracy** | < 3.5% MAE |
| **Status** | ✅ Production-Ready & Maintained |

---

## 📚 Table of Contents
1. [Features](#-features)
2. [System Architecture](#-system-architecture)
3. [AI Model Details](#-ai-model-details)
4. [Alert Thresholds](#-alert-thresholds)
5. [API Endpoints](#-api-endpoints)
6. [Validation Results](#-validation-results)
7. [References & Standards](#-references--standards)
8. [Contact](#-contact)

---

## ✨ Features

### 🤖 Predictive Analytics
- **State of Health (SoH)** — Predicts current battery capacity as a % of nominal with 98.5% training accuracy
- **Remaining Useful Life (RUL)** — Estimates cycles remaining until end-of-life (80% SoH threshold)
- **Degradation Tracking** — Continuous monitoring of battery parameters in real-time
- **Cross-Chemistry Support** — Compatible with Li-ion, NiCd, and VRLA battery types

### 📊 Web Dashboard
- **Real-Time Monitoring** — Live battery status across the entire fleet
- **Trend Analysis** — Historical SoH, capacity, and resistance curves
- **CSV Upload** — Instant AI analysis of uploaded battery telemetry data
- **PDF Reports** — Detailed per-battery assessment documents
- **Performance Metrics** — Model validation statistics and accuracy summaries

### 🚨 Intelligent Alerting
- **Multi-Level Severity** — Warning → Critical → Replace escalation logic
- **Smart Notifications** — Email (SendGrid) and SMS (Twilio) alert delivery
- **Contextual Recommendations** — Specific maintenance action per parameter anomaly
- **Alert Logging** — Full audit trail of all triggered alerts

### 🔒 Production-Grade Engineering
- **Type Safety** — Full Python type hints throughout the codebase
- **Robust Error Handling** — Comprehensive exception management with structured logging
- **Flexible CSV Input** — Auto-detects and maps column names automatically
- **Configuration Management** — Centralized settings via environment variables

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Web Dashboard (Flask)                  │
│         Real-time charts · CSV upload · Reports         │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                  Prediction Engine                       │
│      SoH Model (Gradient Boosting, 400 trees)           │
│      RUL Model (Random Forest, 400 trees)               │
└──────────────┬──────────────────────┬───────────────────┘
               │                      │
┌──────────────▼──────┐   ┌───────────▼───────────────────┐
│  Feature Engineering │   │       Alert Engine            │
│  30+ derived features│   │  IEEE 485 threshold checks    │
│  Rolling averages    │   │  Email (SendGrid) / SMS       │
│  Fade rates, ratios  │   │  (Twilio) notifications       │
└──────────────────────┘   └───────────────────────────────┘
```

---

## 🤖 AI Model Details

| Component | Algorithm | Task |
|-----------|-----------|------|
| SoH Model | RF, XGB, Gradient Boosting — 400 trees | Predict State of Health (%) |
| RUL Model | Random Forest — 400 trees | Predict Remaining Useful Life (cycles) |

### Input Features (15 total)

| Feature | Description |
|---------|-------------|
| `Capacity` | Discharge capacity (Ah) |
| `Re` | Electrolyte resistance (Ω) |
| `Rct` | Charge transfer resistance (Ω) |
| `ambient_temperature` | Operating temperature (°C) |
| `capacity_fade_pct` | % capacity lost from initial value |
| `ir_total` | Total resistance (Re + Rct) |
| `cap_norm` | Capacity normalised per battery |
| `cycle_sqrt` | √cycle — captures early-stage aging |
| `cycle_log` | log(cycle) — captures logarithmic aging |
| `re_rct_ratio` | Resistance ratio between Re and Rct |
| `rolling_cap_3` | 3-cycle rolling mean of capacity |
| `rolling_re_5` | 5-cycle rolling mean of Re |
| `cap_rate` | Capacity fade rate per cycle |
| `re_rate` | Re increase rate per cycle |
| `rct_rate` | Rct increase rate per cycle |

### Supported CSV Column Formats

| Your Column Name | Maps To |
|------------------|---------|
| `Cycle_Index`, `cycle`, `Cycle` | Cycle number |
| `Battery_ID`, `battery`, `Battery` | Battery identifier |
| `Capacity`, `capacity`, `Discharge_Capacity` | Capacity (Ah) |
| `Re`, `electrolyte_resistance` | Re (Ω) |
| `Rct`, `charge_transfer_resistance` | Rct (Ω) |
| `ambient_temperature`, `Temperature`, `temp` | Temperature (°C) |

---

## ⚡ Alert Thresholds (IEEE 485 Standard)

| Parameter | ⚠️ Warning | 🚨 Critical | 🔴 Replace |
|-----------|-----------|------------|-----------|
| SoH % | ≤ 88% | ≤ 80% | ≤ 70% |
| Re (Ω) | ≥ 0.10 | ≥ 0.13 | — |
| Rct (Ω) | ≥ 0.28 | ≥ 0.38 | — |
| Capacity Fade | ≥ 10% | ≥ 18% | ≥ 25% |
| RUL (cycles) | ≤ 30 | ≤ 10 | — |

---

## 📝 License

MIT License — See LICENSE file for details.

---

## 📬 Contact

For any queries regarding this project — implementation details, methodology, collaboration, or internship-related discussions — please contact:

**Shivam Chaturvedi**
- Intern, Reliance Industries
- Email - shivamchaturvedi.in@gmail.com


---

*Battery Health Monitoring System v2.0 · Developed during internship at Reliance Industries*

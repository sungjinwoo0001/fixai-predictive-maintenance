[

![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)

](https://colab.research.google.com/github/sungjinwoo0001/fixai-predictive-maintenance/blob/main/fixai-predictive-maintenance.ipynb)


# ⚙️ FixAI — AI-Powered Predictive Maintenance Platform

An MVP demonstrating **LLM-based reasoning** (Groq `openai/gpt-oss-120b`) over
**Isolation Forest anomaly detection** and sensor trend data, to produce
maintenance risk assessments for industrial machines.

## Why this is different from a typical rule-based system

Most predictive maintenance demos use hardcoded thresholds like:

```python
if temperature > 80:
    risk = "HIGH"
```

FixAI does **not** do this. Instead:

- **Isolation Forest** (traditional ML) flags statistical outliers in sensor
  data — used only as supporting evidence, never as a diagnosis.
- Trends, rates of change, and correlations between sensors are calculated
  as descriptive statistics — not fed into any fixed rule.
- An **LLM** (Groq, `openai/gpt-oss-120b`) reasons over all of this evidence —
  live values, historical trends, anomaly counts, operating hours, and a
  maintenance knowledge base — and produces the actual risk level, likely
  causes, and recommended actions.

There is no hardcoded diagnosis logic anywhere in the pipeline.

## Architecture

```
Sensor Data → Historical Sensor Data → Isolation Forest (statistical anomaly detection)
           → Trend & sensor-relationship extraction → LLM Reasoning (Groq: openai/gpt-oss-120b)
           → AI Maintenance Assessment → Risk + Condition + Causes + Actions
           → Autonomous Maintenance Agent Decision
```

## Features

- 4 simulated machines (Pump, Motor, Compressor, Fan) with ~100 historical
  readings each, including a simulated degradation trend on Compressor-03
- Interactive Colab dashboard: machine selector, live sensor sliders,
  "Run AI Analysis" button
- AI-generated risk score, condition, confidence, detected signals, possible
  causes, and recommended actions — returned as structured JSON
- Sensor trend charts (temperature, vibration, pressure) with anomalies
  highlighted
- "Ask FixAI" chat box to ask follow-up questions about the selected machine
- Graceful error handling for missing/invalid API keys and API failures

## How to run it

1. Open `FixAI_Predictive_Maintenance.ipynb` in **Google Colab**
   (click the file in this repo, then use the "Open in Colab" badge/button,
   or manually open colab.research.google.com and upload it).
2. Get a free API key at [console.groq.com](https://console.groq.com).
3. In Colab, click the 🔑 **Secrets** icon in the left sidebar.
4. Add a new secret named `luffy` with your Groq API key as the value, and
   toggle **Notebook access** on.
5. Run all cells (**Runtime → Run all**).
6. Use the dashboard: pick a machine, adjust sliders if you want, and click
   **RUN AI ANALYSIS**.

No API key is stored in this repository — each user supplies their own via
Colab Secrets at runtime.

## Tech stack

Python · pandas · NumPy · scikit-learn (Isolation Forest) · matplotlib ·
ipywidgets · Groq API (`openai/gpt-oss-120b`)

## Future architecture

This MVP uses synthetic data to demonstrate the reasoning pipeline. A
production version could evolve into:

```
Real IoT Sensors → MQTT/API → Time-Series Database → Anomaly Detection
                 → Predictive / Remaining-Useful-Life Model → LLM Maintenance Agent
                 → Maintenance Work Order → Technician
```

# 💊 AI Medication Management Agent

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15-orange?style=flat-square&logo=tensorflow)
![OpenAI](https://img.shields.io/badge/GPT--4-OpenAI-412991?style=flat-square&logo=openai)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

> An end-to-end AI agent that predicts medication non-adherence using a trained LSTM neural network and uses GPT-4 as a reasoning layer to determine the appropriate clinical intervention — automatically.

---

## 👩‍💻 Built by Virginia McCoy | Solo Project | ITAI 2376

---

## 🧠 Project Overview

Medication non-adherence is responsible for approximately 125,000 deaths and $300 billion in healthcare costs annually in the United States. This agent addresses that problem directly by combining deep learning sequence modeling with large language model reasoning to create an intelligent, automated early-warning system for caregivers and clinical staff.

Instead of manually reviewing patient dose logs, a caregiver gets real-time AI-driven alerts the moment a patient's behavior pattern signals risk — before a missed dose becomes a health crisis.

---

## 🏗️ Architecture

The agent runs a four-stage pipeline that connects a deep learning model to a GPT-4 reasoning layer:

```
[Patient Dose Input] → [LSTM Model] → [GPT-4 Agent Brain + Memory] → [Notification Tool] → [Action Output]
```

1. **Input** — Patient's last 3 doses (binary: 1 = taken, 0 = missed) and weekly adherence rate
2. **LSTM Model** — Trained recurrent neural network predicts the probability of the next dose being missed, learning each patient's unique temporal behavior pattern
3. **GPT-4 Agent Brain** — Receives the LSTM prediction and maintains conversation memory across interactions, enabling context-aware clinical reasoning rather than single-point decisions
4. **Notification Tool** — Executes one of three actions based on the agent's decision: send an SMS reminder, escalate to the physician, or take no action

![Architecture Diagram](architecture.png)

---

## 🔬 Deep Learning Concepts Applied

| Concept | Implementation |
|---|---|
| **LSTM (Long Short-Term Memory)** | Sequential dose prediction — captures temporal patterns unique to each patient that rule-based systems cannot |
| **Transformer Architecture (GPT-4)** | Attention-based reasoning layer for nuanced clinical decision making |
| **Binary Classification** | LSTM output layer uses sigmoid activation to classify next dose as Taken (1) or Missed (0) |
| **Conversation Memory** | Full chat history passed to GPT-4 on every call, enabling multi-interaction context awareness |
| **Sequence Modeling** | Sliding window approach builds training pairs from patient history for supervised learning |

---

## 🛠️ Tech Stack

| Layer | Tool |
|---|---|
| Deep Learning | TensorFlow 2.15 / Keras |
| LLM Reasoning | OpenAI GPT-4 |
| API Integration | OpenAI Python SDK v1.30 |
| Data Processing | NumPy, Pandas |
| Environment | Google Colab / Jupyter Notebook |

---

## ⚙️ Installation & Setup

**Requirements:** Python 3.10+

```bash
# Clone the repository
git clone https://github.com/VirginiaMcCoy/VirginiaMcCoy_Solo_ITAI2376.git
cd VirginiaMcCoy_Solo_ITAI2376

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Add your OpenAI API key to .env
```

---

## ▶️ Running the Agent

Open `medication_agent_demo.ipynb` in Google Colab or Jupyter and run all cells in order.

In **Cell 2**, add your OpenAI API key before running:
```python
OPENAI_API_KEY = 'your-key-here'
```

> ⚠️ Never commit your real API key. The `.gitignore` excludes `.env` automatically — verify before pushing.

---

## 💬 Sample Outputs

**Scenario 1 — Early decline detected**
```
Input:   Last 3 doses: [1, 0, 0] | Weekly adherence: 50%
LSTM:    Prediction → Missed (confidence: 78%)
GPT-4:   ACTION: Send Reminder
         REASON: Downward adherence trend detected — proactive outreach recommended.
Output:  🔔 SMS dispatched | Caregiver dashboard updated
```

**Scenario 2 — Patient on track**
```
Input:   Last 3 doses: [1, 1, 1] | Weekly adherence: 92%
LSTM:    Prediction → Taken (confidence: 91%)
GPT-4:   ACTION: No Action
         REASON: Patient demonstrates strong consistent adherence — no intervention needed.
Output:  ✅ No action taken
```

**Scenario 3 — Critical non-adherence**
```
Input:   Last 3 doses: [0, 0, 0] | Weekly adherence: 33%
LSTM:    Prediction → Missed (confidence: 94%)
GPT-4:   ACTION: Escalate to Doctor
         REASON: Chronic non-adherence at critical threshold — physician review required immediately.
Output:  🚨 Physician notified | Patient chart flagged for follow-up
```

---

## ⚠️ Known Limitations

- LSTM is trained on a simulated 12-dose dataset. Production deployment would require patient-specific longitudinal data for meaningful generalization
- Notification outputs are console-based; no live SMS or EHR system is connected in this version
- Conversation memory is session-scoped — long-term patient history persistence would require a vector database such as Pinecone
- LLM outputs are non-deterministic; slight variation between runs is expected

---

## 🚀 Future Development

- Integrate a **CNN image recognition layer** to visually verify correct medication from a pill bottle photo
- Connect to a real **EHR API** for live patient data ingestion
- Add **persistent vector memory** (Pinecone / ChromaDB) for long-term patient history across sessions
- Build a **caregiver web dashboard** for real-time alert monitoring

---

## 🎥 Demo

[Watch the full demo here](https://houcomcol-my.sharepoint.com/:v:/g/personal/w211295755_student_hccs_edu/IQDiSPdOD9VVQquOeA9dVsiWAeO1iiHIGRsbQGZ-w6mwf5M)

---

## 📄 License

This project was built for academic purposes as part of ITAI 2376 at Houston Community College.

# -ArvyaX-Emotional-Intelligence-System
I have Developed a  system which understand human emotional state,  reason under imperfect and noisy signals,  decide meaningful next actions,  guide users toward better mental states

### *From Understanding Humans → To Guiding Them*

---

## 🚀 Overview

This project builds an intelligent system that goes beyond prediction to:

* Understand human emotional states from messy reflections
* Reason under noisy and incomplete signals
* Decide meaningful next actions
* Guide users toward better mental states

Unlike traditional ML tasks, this system is designed for **real-world conditions**, handling:

* Short and ambiguous text
* Missing values
* Conflicting signals
* Imperfect labels

---

## 🧠 Problem Statement

Given a user reflection and contextual signals, the system predicts:

### 1. Emotional Understanding

* `predicted_state` (e.g., calm, restless, overwhelmed, etc.)
* `predicted_intensity` (1–5 → mapped to 3 levels)

### 2. Decision Layer

* **What to do** (e.g., breathing, journaling, deep work)
* **When to do it** (now, within_15_min, later_today, etc.)

### 3. Uncertainty Awareness

* `confidence` score (0–1)
* `uncertain_flag` (model knows when it is unsure)

### 4. (Bonus) Human-like Support Message

* Context-aware supportive guidance

---

## 📊 Dataset

The dataset contains:

* **Text input**: journal reflections
* **Contextual signals**:

  * sleep_hours
  * stress_level
  * energy_level
  * time_of_day
  * previous_day_mood
  * ambience_type
  * face_emotion_hint
  * reflection_quality

---

## ⚙️ Methodology

### 🔹 1. Data Preprocessing

* Handled missing values:

  * Numerical → median imputation
  * Categorical → "unknown"
* Cleaned text:

  * Lowercasing
  * Removed noise (special characters, “idk”)


---

### 🔹 2. Feature Engineering

#### 📌 Text Features (NLP)

* TF-IDF Vectorization (300 features)


#### 📌 Metadata Features

* sleep_hours, stress_level, energy_level, duration
* text_length
* stress_energy_ratio
* low_sleep indicator

#### 📌 Categorical Encoding

* One-hot encoding for:

  * time_of_day
  * ambience_type
  * previous_day_mood
  * face_emotion_hint
  * reflection_quality

---

### 🔹 3. Feature Combination

Final input:

Text Features + Metadata Features → Combined Feature Vector

---

### 🔹 4. Model Design

#### ✅ Emotional State Model

* Model: XGBoost Classifier
* Target: Multi-class classification

#### ✅ Intensity Model

* Reformulated as **3-class classification**:

  * Low (1–2)
  * Medium (3)
  * High (4–5)

* Model: XGBoost Classifier

---

### 🔹 5. Training Strategy

* Training dataset split into:

  * Train
  * Validation
  * Test

* Final model trained on **full dataset** for maximum learning

* External test dataset used for **final inference only**

---

### 🔹 6. Decision Engine (Core Intelligence)

Rule-based reasoning using:

* predicted_state
* predicted_intensity
* stress_level
* energy_level
* time_of_day

#### Example Logic:

* Overwhelmed → Breathing
* Restless → Grounding
* Focused → Deep Work
* Low energy → Rest

---

### 🔹 7. Uncertainty Modeling

* Confidence computed using model probabilities

* Final confidence = average of:

  * state confidence
  * intensity confidence

* `uncertain_flag = 1` if confidence < 0.55

---

### 🔹 8. Supportive Message Generation (Bonus)

Context-aware human-like responses:

> “You seem slightly restless. Let’s slow things down. Try a short grounding exercise.”

---

## 📈 Model Performance

### 🎯 Emotional State Model

* Accuracy: **~67%**
* Balanced across multiple emotional classes
* Strong performance on:

  * focused
  * calm
  * overwhelmed

---

### 🎯 Intensity Model (3-Class)

* Accuracy: **40%**
* Improved stability compared to 5-class setup
* Handles noisy and subjective labels

---

## 🔬 Ablation Insight

| Model           | Performance |
| --------------- | ----------- |
| Text-only       | Lower       |
| Text + Metadata | Higher ✅    |

👉 Metadata significantly improves predictions.

---

## ⚠️ Challenges Faced

* Ambiguous reflections
* Contradictory inputs
* Noisy labels
* Short text inputs ("ok", "fine")

---

## 🧪 Error Analysis

Common failure cases:

* Mixed emotions → misclassification
* Very short text → low signal
* Conflicting metadata → confusion
* Label noise → reduced accuracy

---

## 📦 Output Format

The system generates:

```csv
id, predicted_state, predicted_intensity, confidence,
uncertain_flag, what_to_do, when_to_do
```

---

## 💻 Edge Deployment Plan

* Lightweight model (XGBoost)
* TF-IDF instead of heavy embeddings
* Suitable for:

  * mobile devices
  * offline inference

### Trade-offs:

* Lower latency ✅
* Lower complexity ✅
* Slight reduction in semantic understanding ⚠️

---

## 🎨 Bonus: UI System

Built using Gradio:

* Interactive input
* Real-time predictions
* Actionable guidance
* Supportive messaging

---

## 🛠️ Tech Stack

* Python
* Scikit-learn
* XGBoost
* NumPy / Pandas
* Gradio

---

## 🚀 How to Run

```bash
pip install -r requirements.txt
```

Run notebook or script to:

* Train models
* Generate predictions
* Launch UI

---

## 💡 Key Learnings

* Real-world ML ≠ clean datasets
* Decision systems are as important as prediction
* Uncertainty awareness is critical
* Combining NLP + structured data improves performance

---

## 🌿 Final Thought

This project moves from:

**Prediction → Understanding → Decision → Guidance**

Building AI systems that don’t just analyze humans,
but actually **help them.**

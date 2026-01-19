# Applied ML System Design  
## Zomato Customer Churn Prediction

---

## 1. Business Motivation

Zomato operates in a highly competitive food delivery ecosystem where customer retention is significantly more cost-effective than acquisition.

This system is designed to **identify users at risk of churn early enough to trigger meaningful retention actions**.

---

## 2. Defining Churn (System-Critical Step)

### Naive Definition
User inactive for 30 days.

### Refined Definition
A user predicted to stop placing orders in the next **21 days**, based on behavioral data from the previous **30 days**.

This definition ensures:
- temporal clarity
- actionability
- consistent labeling

---

## 3. High-Level System Architecture

User Activity
↓
Data Ingestion Layer
↓
Data Validation & Cleaning
↓
Feature Engineering (Time-Aware)
↓
Churn Prediction Model
↓
Decision Engine
↓
Retention Actions
↓
Monitoring & Feedback Loop


---

## 4. Data Sources

- Order history
- App session logs
- Delivery performance
- Payment failures
- Location changes

### Challenges Addressed
- Missing event logs
- Multi-device users
- City migration vs churn confusion

---

## 5. Data Leakage Prevention

### Explicitly Excluded Features
- Account deactivation flags
- Refund outcomes
- Cancellation events after churn

### Temporal Safeguard

Past Behavior → Prediction Time → Future Events (Blocked)


Only information available at prediction time is used.

---

## 6. Feature Engineering Strategy

### Feature Categories

**Recency**
- Time since last order

**Frequency**
- Orders in last 7 / 14 / 30 days

**Trend**
- Increasing or decreasing order activity

**Reliability Signals**
- Delivery failures
- Payment issues

### Key Insight
Recent behavior dominates lifetime aggregates when predicting churn.

---

## 7. Evaluation Strategy

### Avoided Metrics
- Accuracy-only evaluation

### Preferred Metrics
- Recall at top-risk users
- Cost-sensitive evaluation
- Retention uplift

Metrics reflect **business impact**, not just predictive power.

---

## 8. Decision Mapping

Churn Score →
High Risk → Retention Team Call
Medium Risk → Discount / Offer
Low Risk → No Action


This ensures predictions directly influence outcomes.

---

## 9. Monitoring & Retraining

### Monitored Signals
- Feature distribution drift
- Prediction confidence shifts

### Retraining Triggers
- Time-based retraining
- Drift-based alerts

---

## 10. Final System Flow Diagram

User Events
↓
Validated Data Pipeline
↓
Time-Aware Features
↓
Churn Model
↓
Decision Engine
↓
Retention Action
↓
Monitoring & Retraining

---

## 11. Key Takeaway

This project demonstrates that **ML success depends more on system design than algorithm complexity**.

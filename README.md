# 🔐 Cybersecurity Threat Intelligence Dashboard (Power BI)

## 📌 Project Overview
This is my first end-to-end **Data Analytics project** built using **Power BI**.  

The dashboard analyzes cybersecurity attack data to understand attacker behavior, simulating a **Security Operations Center (SOC)** environment.  

Instead of manually sifting through thousands of security logs, the dashboard transforms complex technical data into **interactive visual insights** for monitoring and investigation.

---

---

## 🎯 Project Objectives
- Understand real-world cybersecurity datasets  
- Perform data cleaning and preprocessing  
- Build a **relational data model** (Fact & Dimension tables)  
- Design monitoring and investigation dashboards  
- Visualize cyber attack patterns for actionable insights  

---

## 🧩 Project Workflow

Raw Security Logs  
→ Data Cleaning & Structuring  
→ Data Modeling  
→ Visualization  
→ Threat Monitoring  
→ Investigation & Insights

---

## 🧹 Data Preparation (Pre-Processing)

Before importing data into Power BI, the dataset was cleaned and structured.  

**Key steps performed:**
- Removed missing or invalid values  
- Converted timestamps to proper date-time format  
- Categorized risk levels: **Low / Medium / High**  
- Aggregated attack counts  
- Structured data into **relational tables**  
- Prepared dataset for analytical modeling  

### Example Transformation Logic

```python
import pandas as pd

# Load dataset
df = pd.read_csv("attacks.csv")

# Convert timestamp to datetime
df["timestamp"] = pd.to_datetime(df["timestamp"])

# Risk category classification
def classify_risk(score):
    if score < 4:
        return "Low"
    elif score < 7:
        return "Medium"
    else:
        return "High"

df["risk_category"] = df["threat_score"].apply(classify_risk)

# Aggregate attacks by country and technique
attack_summary = (
    df.groupby(["country", "technique"])
      .size()
      .reset_index(name="attack_count")
)

# Save cleaned dataset
df.to_csv("clean_attacks.csv", index=False)

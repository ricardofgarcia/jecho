# 🔊 J.E.C.H.O.

### **J**ira **E**valuation of **C**omments & **H**ealth **O**utcomes

> **"The status is Green, but what is the team actually saying?"**

**J.E.C.H.O.** is an advanced analytic engine for Technical Program Managers. Unlike standard reports that rely on manual status updates, J.E.C.H.O. "listens" to the textual data (comments, descriptions, summaries) of a Jira hierarchy. It triangulates **Sentiment**, **Velocity**, and **Delivery Math** to produce a true-to-life health assessment.

-----

## 📡 What does it do?

J.E.C.H.O. performs a deep-dive sonar scan on a specific Jira Issue (Outcome, Feature, or Epic) and its children. It answers three critical questions:

1.  **The Vibe (Sentiment):** Is the team frustrated, blocked, or confident?
2.  **The Speed (Velocity):** Based on actual closure rates, how fast are we moving?
3.  **The Reality (Forecast):** Based on Vibe + Speed, when will we *actually* finish?

-----

## 🧮 The J.E.C.H.O. Algorithm

The engine uses a weighted formula to calculate the "Overall Health Score," giving more weight to high-priority items and active development phases.

### 1\. Sentiment Scoring

J.E.C.H.O. reads the room using a weighted average:

$$\text{Overall Score} = \frac{\sum (\text{Text Sentiment} \times \text{Priority Multiplier} \times \text{Status Contribution})}{\sum (\text{Priority Multiplier} \times \text{Status Contribution})}$$

  * **Priority Multipliers:** Critical/Blocker (3x) $\rightarrow$ Minor (0.75x)
  * **Status Weights:** In Progress/Testing (1.3x) $\rightarrow$ Backlog (1.1x) $\rightarrow$ Done (1.0x)

### 2\. Velocity Calculation

It ignores hopeful estimates and calculates raw speed:
$$\text{Velocity} = \frac{\text{Completed Children}}{\text{Weeks Active}}$$

### 3\. Delivery Forecast

It projects the finish line based on current velocity, adding a risk buffer:
$$\text{Est. Date} = \left( \frac{\text{Open Children}}{\text{Velocity}} \right) + \text{Today} + 10\% \text{ Buffer}$$

-----

## 🚦 The "Echo" Status

The final output categorizes the issue into three signal types:

| Signal | Status | Criteria |
| :--- | :--- | :--- |
| 🟢 | **Clear** | Positive Sentiment AND Delivery Date $\le$ Target Date (+1 week) |
| 🟡 | **Distorted** | Neutral Sentiment OR Delivery Date is 1-3 weeks late |
| 🔴 | **Noisy** | Negative Sentiment OR Delivery Date is \>3 weeks late |

-----

## 🛠️ Setup & Configuration

### Prerequisites

  * Python 3.9+
  * Jira API Access

### Environment Variables

Create a `.env` file in your root directory:

```bash
JIRA_BASE_URL="https://issues.redhat.com"
JIRA_USER_EMAIL="your_email@redhat.com"
JIRA_API_TOKEN="your_api_token"
```

### Usage

Pass the top-level issue key you want to analyze. J.E.C.H.O. will fetch the entire hierarchy.

```bash
# Analyze a single Epic or Initiative
python jecho_engine.py --issue PROJECT-1234

# Output:
# > 📡 Pinging hierarchy for PROJECT-1234...
# > 👂 Listening to 15 child issues...
# > 📊 Computing velocity...
# > 📝 Generating Markdown Report...
```

-----

## 📄 Output Format

J.E.C.H.O. generates a rich Markdown report optimized for Google Docs import.

  * **Executive Summary:** A high-level narrative of the risk.
  * **TL;DR:** The 2-sentence reality check.
  * **Cross-Cutting Observations:** "Meta" analysis of the comments (e.g., "The team mentions 'latency' in 4 different tickets").
  * **Child-Level Breakdown:** Per-ticket sentiment analysis.

-----

*Maintained by the TPM Team. Amplifying the signal, reducing the noise.* 🔊

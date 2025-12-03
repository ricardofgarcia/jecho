
# Prompts Evolution

This document traces the evolution of the prompts, from a simple, static query (v0.1) to a sophisticated, formalized Technical Program Management (TPM) tool (v0.6) for assessing Jira issue health and sentiment.

# Core Progression Theme

The prompt evolution shifted from **Simple Sentiment Reporting** (v0.1-v0.3) to **Time-Based Predictive Analysis** (v0.4) and finally to a **Formalized Project Health Assessment Engine** (v0.5-v0.6) complete with formulas, velocity calculations, and structured output.

# Prompt Version Summary

| Prompt | Tagline | Primary Focus & Key Innovation | Limitation Addressed in Next Version |
| :---- | :---- | :---- | :---- |
| **v0.1** | The **Static Snapshot** | Direct, one-time sentiment check on a hard-coded issue. | Not repeatable; lacks structure or roll-up logic. |
| **v0.2** | The **Structured Scaffold** | Established a repeatable structure, explicit data requirements, and foundational status/color roll-up logic. | Lacked timing, velocity, or predictive scheduling. |
| **v0.3** | The **Basic Sentiment Reporter** | Formalized input workflow (requiring issue type) and enhanced the output with narrative sections and per-issue justification. | Lacked any concept of project health, velocity, or predictive delivery. |
| **v0.4** | The **Velocity Vitals** | **Introduced time-based metrics:** Calculated issue velocity (rate of completion) and projected a target delivery date. | Lacked structured health assessment (color-coding) and formalized weighted scoring. |
| **v0.5** | The **Health Color-Coder** | **Introduced Project Health Assessment:** Formalized weighted sentiment scoring, calculated a computed **Color Status** (GREEN/YELLOW/RED), and added a 10% risk buffer to delivery dates. | Velocity calculation was imprecise; core logic needed formal definition/justification. |
| **v0.6** | The **TPM Precision Engine** | **Formalized all logic:** Introduced detailed LaTeX formulas for sentiment and status severity. Refined **velocity calculation** (tied to the *first* child resolution date for higher accuracy) and mandated justification for both Sentiment and Health Status. | N/A (The last version.) |

# Key Concepts and Logic Formalized (v0.6)

* **Sentiment Scoring:** Defined by a formal mathematical formula incorporating explicit weights for Priority (e.g., Blocker=3x) and Status Contribution (e.g., In Progress=1.3x).

* **Velocity:** Defined as `(number of 'completed' children) / (weeks since the first child's Resolution Date)`.

* **Delivery Date:** Calculated as `(open children / velocity) + (current date) + a 10% risk buffer`.

* **Health Status:** Determined by comparing the calculated delivery date against the target date, resulting in a color-coded status (🟢, 🟡, 🔴).


## **🏷️ Prompt Taglines**

| Prompt | Tagline |
| :---- | :---- |
| Prompt v0.1 | The **Static Snapshot**: Asking for a single, direct, one-time sentiment check. |
| Prompt v0.2 | The **Structured Scaffold**: Defining the fields, the format, and the status roll-up. |
| Prompt v0.3 | The **Basic Sentiment Reporter:** Formalizing the flow and asking for explicit input types. |
| Prompt v0.4 | The **Velocity Vitals**: Introducing the concepts of issue pacing and projected delivery dates. |
| Prompt v0.5 | The **Health Color-Coder**: Adding weighted scoring, risk buffers, and a three-color health assessment. |
| Prompt v0.6 | The **TPM Precision Engine**: Formalizing all logic with mathematical formulas and improving velocity accuracy. |

## 📜 Prompt Summaries

### Prompt v0.1: The Static Snapshot

* **Goal:** To perform a **direct, one-off sentiment analysis** on a specific, hard-coded Jira issue and its limited set of "In Progress" children.  
* **Key Action:** Retrieve the limited hierarchy, analyze the `status summary` field and the last week's `comments`, and determine a general sentiment.  
* **Output Focus:** A simple, three-part narrative report (`TL;DR`, `Executive Summary`, `Supporting Information`) focused purely on **summarizing the sentiment**.  
* **Limitation:** The prompt is **not repeatable or flexible**; it uses static JQL embedded in the request and does not define a standard data structure or output template.

### Prompt v0.2:The Structured Scaffold

* **Goal:** To establish a **repeatable Sentiment Analysis Engine** that uses defined JQL to fetch the full open hierarchy and structure the analysis output.  
* **Key Action:** Formalize the input process, explicitly define the **fields to fetch** (including fields for weighted scoring and status tracking), and introduce the core logic for calculating and **rolling up `Status Summary` and `Color Status`**.  
* **Output Focus:** A structured, multi-section Markdown report featuring individual issue details, including calculated status and color, adhering to a formal **`OUTPUT TEMPLATE`**.  
* **Limitation:** While highly structured, it still focuses only on sentiment and status reporting; it **lacks any concept of timing, velocity, or predictive scheduling**.

### Prompt v0.3: The Basic Sentiment Reporter

* **Goal:** To act as a **Sentiment Analysis Engine** that processes a single Jira issue hierarchy and produces a simple report.  
* **Key Action:** Retrieve issue hierarchy, fetch key text fields (`Summary`, `Description`, `Comment`, `Status Summary`), calculate sentiment, and compute a basic `status summary roll up`.  
* **Output Focus:** A narrative report covering **Overall Sentiment**, justification, impact, and a list of supporting issues with their individual sentiment and status.  
* **Limitation:** Lacks any concept of project health, delivery timing, or complex weighted scoring.

### Prompt v0.4: Introducing Time and Velocity

* **Goal:** To expand the analysis by incorporating **time-based metrics** into the report.  
* **Key Action:** Build upon Prompt v0.3 by adding the calculation of **issue velocity** (rate of completion) and using it to project a **target delivery date**.  
* **New Data:** Requires fetching the `Target end Date` from Jira.  
* **Output Focus:** The report remains sentiment-focused but now includes calculated delivery metrics (`Issue Delivery Velocity` and `Delivery Date`) for every issue.

### Prompt v0.5: The Project Health Assessor

* **Goal:** To transform the tool into a comprehensive **Project Health Assessment Engine** by introducing structured scoring and color-coding.  
* **Key Action:** Formalize the sentiment calculation using explicit **Weighted Scoring Logic** (based on `Priority` and `Status`). Introduce the concept of a **`computed color status`** (GREEN, YELLOW, RED) by comparing the calculated delivery date against the target date.  
* **New Data:** Requires fetching `Color Status`, `Type`, and `Resolution Date`.  
* **Output Focus:** The report structure is overhauled to feature **Overall Health Status** prominently alongside sentiment, clearly stating the computed velocity and delivery dates in the Executive Summary.

### Prompt v0.6: The Refined and Formalized Engine

* **Goal:** To formalize all core logic, improve calculation accuracy, and create a robust, context-aware reporting tool for a Technical Program Manager.  
* **Key Action:** Introduce detailed **`CORE LOGIC DEFINITIONS`** for Status Severity and the Sentiment Scoring Formula (using LaTeX). Critically refines **velocity calculation** to be more accurate (based on the first child's resolution date) and adds a risk buffer to the computed delivery date.  
* **New Requirements:** Requires the engine to provide justifications for both **Sentiment** and **Health Status**, and to use color emojis (🟢, 🟡, 🔴) in the final Markdown output.  
* **Overall Theme:** Focus on high accuracy, comprehensive justification, and a professionally structured output for decision-making.

---

## **🔄  Summary of Changes Between Prompts**

### **Prompt v0.1 vs. Prompt v0.2**

The move from **Prompt v0.1** to **Prompt v0.2** represents the transition from a single, static analytical request to establishing the basic **structure, data requirements, and roll-up logic** for an ongoing, repeatable sentiment analysis tool.

| Category | Prompt v0.1 (Single Query) | Prompt v0.2 (Establishing Scaffolding) | Change Summary |
| :---- | :---- | :---- | :---- |
| **Input Method** | **Static.** Analysis of a single, hard-coded issue (XCMSTRAT-1254). JQL is embedded in the request. | **Interactive.** Introduces a formal step to ask the user for the **set of issues** to analyze (comma-separated values). | Shifted from a specific task to an **interactive and repeatable service.** |
| **Hierarchy Scope** | Defined by a specific JQL clause: only open issues with statusCategory in ("In Progress"). | Defined by robust, reusable **JQL templates** for Outcomes/Features/Initiatives and Epics, covering a broader set of "open" issues. | Formalized the use of JQL templates to fetch the **full hierarchy.** |
| **Data Requirements** | Implicitly uses Status Summary and last week's comments. | Explicitly defined **FIELDS TO FETCH** including Summary, Description, Priority, Status, Color Status, and Lifecycle Context fields. | **Formalized Data Structure.** Introduced necessary fields for weighted scoring and status tracking. |
| **Core Logic** | Calculates sentiment based on the two implicit text fields. | Introduced explicit **Intermediate steps** to calculate and **roll up** both **Status Summary** and **Color Status** for parent issues. | Established the foundational **roll-up logic** to aggregate child issue status/color. |
| **Output Structure** | Simple, three-part report (TL;DR, Executive Summary, Supporting Information). | Introduced a detailed, multi-section **OUTPUT TEMPLATE** including fields like Status-Summary (calculated) and Color-Status (calculated) for each issue. | Created a **structured, reusable Markdown template** for professional reporting. |
| **Weighted Scoring** | Not mentioned. | Introduced a **Weighted Scoring** section defining that higher Priority and issues "in progress" should have a higher contribution to sentiment. | Introduced the concept of **weighting** data points, not just text. |

### 

### **Prompt v0.2 vs. Prompt v0.3**

The primary shift between Prompt v0.2 and Prompt v0.3 was to make the engine's interaction more explicit and robust, particularly in how it handles user input and calculates status summaries.

| Category | Prompt v0.2 (Scaffolding) | Prompt v0.3 (Formalized Interaction/Baseline) | Change Summary |
| :---- | :---- | :---- | :---- |
| **Input Workflow** | Asked only for the **set of issues** to analyze. | **Mandated Input:** Added an explicit step to ask for the issue's **type** (Outcome, Epic, etc.), or fetch it if missing. | **Crucial:** Formalized the input requirement, acknowledging the dependency on issue type for selecting the correct JQL. |
| **Logic Roll-Up** | Used ambiguous **Intermediate steps** to calculate and roll up Status Summary and Color Status. | Divided logic into **ADDITIONAL STEPS**: **1\.** Explicitly defined the preference for an existing Status Summary field over the calculated one (referred to as **selected status summary**). **2\.** Removed the explicit step for **Color Status** roll-up. | Simplified the logic by focusing the initial effort on only the Status Summary roll-up. |
| **Output Detail** | Lacked key narrative sections. | **Added Key Narrative Sections:** Included Overall Sentiment, Overall Sentiment Justification, Summary of impact, and Executive Summary headers. | Enhanced the report structure to focus on **narrative and justification**. |
| **Issue Detail** | Issue details in Supporting Information lacked justification. | Added a **Justification** field under each individual issue in the Supporting Information section. | Required the engine to explain the sentiment outcome for *every* issue analyzed, not just the top-level one. |
| **JQL Tooling** | Did not mention any tools in the steps. | Added explicit steps to use the **jira\_search tool** for retrieving the full hierarchy. | Formalized the use of the necessary tool within the workflow instructions. |
| **Status Summary Logic** | Included calculation for Status Summary and Color Status. | Removed Color Status calculation logic (only kept Status Summary logic), simplifying the engine's responsibilities for this version. | Reduced the complexity of the status calculation requirements in this iteration. |

### 

### **Prompt v0.3 (Baseline) vs. Prompt v0.4**

Prompt v0.4 significantly expands the scope by introducing **velocity and delivery date calculations**, requiring new data fields.

| Category | Prompt v0.3 (Baseline) | Prompt v0.4 | Change Summary |
| :---- | :---- | :---- | :---- |
| **New Computations** | status summary roll up | Added: **computed issue velocity** and **target delivery date roll up** (renamed to Delivery Date (calculated) in the output). | Introduced key **timing and pacing metrics.** |
| **Velocity Logic** | N/A | computed issue velocity is defined as the rate of child issues completed per week. | Defined a new computational step. |
| **Fields to Fetch** | Excluded Target end Date. | Added: **Target end Date** (customfield\_12313942) to Lifecycle Context. | Required a **target delivery field** for analysis/comparison. |
| **Output Template** | Issue details end after Justification. | Added: **Issue Delivery Velocity (calculated)** and **Delivery Date (calculated)** fields to every issue in the Supporting Information section. | Updated the report to include the new timing metrics. |
| **Minor Change** | Status Summary (calculated) | Renamed to Status-Summary (calculated) (hyphen added). | Minor formatting change. |

---

### 

### **Prompt v0.4 vs. Prompt v0.5**

Prompt v0.5 introduces **health status assessment, color-coding logic, and formalized sentiment scoring weights**, moving the engine from simple sentiment analysis to a full **project health assessment**.

| Category | Prompt v0.4 | Prompt v0.5 | Change Summary |
| :---- | :---- | :---- | :---- |
| **Task Scope** | Sentiment Analysis | Sentiment Analysis **and Project Health Assessment**. | Broadened the engine's primary goal. |
| **Additional Steps** | 3 steps (compute status summary, velocity, status roll up) | Added: **computed delivery date** logic refinement and **computed color status** (Health Status) logic. | Introduced explicit Health Status logic tied to sentiment and schedule variance. |
| **Velocity Logic** | Calculated as rate of completed children per week using Created Date. | Clarified: rate of **children in 'Done' status** / **number of weeks since the parent issue's Created Date**. | Clarified which date to use for the time window. |
| **Delivery Date** | target delivery date roll up based on velocity \* open children. | Refined: **(open children / velocity) \+ (current date) \+ a 10% risk buffer**. Also requires flagging discrepancies with Target end Date. | Added a **risk buffer** and a comparison/flag requirement. |
| **Sentiment Logic** | General Weighted Scoring section | Formalized **SENTIMENT SCORING LOGIC**: defined Priority multipliers (e.g., Blocker=3x) and Status Contribution (+20% for 'In Progress'). | **Crucial:** Defined the mathematical inputs for the sentiment score. |
| **Fields to Fetch** | Excluded Color Status, Type, Resolution Date. | Added: **Color Status** (customfield\_12320845), **Type** (issuetype), and **Resolution Date** (resolutiondate). | Required fields for color status tracking and more granular velocity calculation. |
| **Output Template** | Overall Sentiment section | Added: **Overall Health Status** section. Changed sentiment/summary to explicitly state computed metrics. Updated all supporting fields to use Summary instead of generic brackets. | Full report redesign to feature **Health Status** prominently. |

---

### 

### **Prompt v0.5 vs. Prompt v0.6**

Prompt v0.6 acts as a **refinement and formalization** of the health assessment logic introduced in Prompt v0.5, specifically improving the **velocity calculation** and **sentiment/status roll-up formulas**.

| Category | Prompt v0.5 | Prompt v0.6 | Change Summary |
| :---- | :---- | :---- | :---- |
| **Context/Tone** | Standard TPM prompt. | Added: **CORE LOGIC DEFINITIONS** section for clarity and a **Disclaimer** in the output. | Formalized the document structure and acknowledged AI generation. |
| **Status Severity** | Implicit (e.g., "summarize the overall progress") | Defined **Status Severity Order**: Blocked \> At Risk \> On Track. | Formalized the basis for the status summary roll up. |
| **Sentiment Formula** | Priority Multiplier list and Status Contribution defined separately. | Introduced the **Formal Mathematical Formula (in LaTeX)** for the Overall Sentiment Score, providing a highly detailed weighting breakdown (e.g., Critical=2x, Major=1.5x, etc., and detailed status weights like 1.3 for 'Review'). | **Highly Detailed Logic:** Precisely defined all weighting factors for sentiment calculation. |
| **Velocity Logic** | (Done children) / (weeks since parent Created Date). | Refined: **(number of 'completed' children) / (weeks since the first child's Resolution Date)**. Introduced a **Resolution/Resolution Date** dependency and an **Edge Case** (denominator=1 if \<1 week old). | Improved accuracy by tying velocity to the time since the *first* completion, not the parent's creation date. |
| **Status Summary (computed)** | Computed for all issues. | Restricted: **Only compute status summaries for issues with a 'Status Contribution' greater than 1.0**. | Reduced computation load by ignoring low-priority/inactive issues. |
| **Color Status Fallback** | Missing Target end Date defaults to Sentiment unless calculated delivery is 6+ months long. | Added: Explicit instruction to use **color emojis** (🟢, 🟡, 🔴, 🔵) in the output template. | Improved visual representation in the final report. |
| **JIRA Queries** | Single set of JQL queries (implicitly only for open issues). | Added two JQL options: **'all' issues** and **'only open' issues** for both Initiatives and Epics. Added a note to run a separate JQL query for multiple top-level issues. | Enhanced flexibility for data retrieval, allowing for analysis of closed issues if needed. |
| **Output Template** | Overall Sentiment Justification | Added: **Overall Health Status Justification** and combined the drivers into **Overall Sentiment and Health Status Drivers**. | Ensured justification is provided for both key final scores. |

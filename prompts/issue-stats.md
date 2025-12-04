# CONTEXT & TASK

## Statistics
Find these statistics for each `Given Issue`, 

1. Fetch the `Number of Descendants`
1. Fetch the `Number of Open Descendants`
1. Calculate the `Number of Closed Descendants`
1. Fetch the `Oldest Resolution Date`
1. Calculate the `Weeks Active`
1. Calculate the `Completion Velocity`

## Fetching Data

### JQL Statements
Use the following JQL statements to fetch the data of interest

#### `Number of Descendants`

```
(
issuekey = `Given Issue` OR
(issuefunction in portfolioChildrenOf("issuekey = `Given Issue`")) OR
issueFunction in issuesInEpics("issueFunction in portfolioChildrenOf('issuekey = `Given Issue`')")
)
```

#### `Number of Open Descendants`
```
(
issuekey = `Given Issue` OR
(issuefunction in portfolioChildrenOf("issuekey = `Given Issue`") and statusCategory not in (Done)) OR
issueFunction in issuesInEpics("issueFunction in portfolioChildrenOf('issuekey = `Given Issue`')") and statusCategory not in (Done)
)
```

#### `Oldest Resolution Date`

(
issuekey = `Given Issue` OR
(issuefunction in portfolioChildrenOf("issuekey = `Given Issue`") AND (statusCategory in (Done) AND resolution = Done)) OR
issueFunction in issuesInEpics("issueFunction in portfolioChildrenOf('issuekey = `Given Issue`')") AND (statusCategory in (Done) AND resolution = Done)
) order by resolutiondate ASC

## Calculations

### `Number of Closed Descendants`
Calculate the `Number of Closed Descendants` by substracting the `Number of Open Descendants` from the `Number of Descendants`.

$$
\begin{equation}
\text{Number of Closed Descendants} = \text{Number of Descendants} - \text{Number of Open Descendants}
\end{equation}
$$


### `Weeks Active`

Calculate the `Weeks Active` by finding the number of days elapsed between two dates and then dividing that total by seven.

$$
\begin{equation}
\text{Weeks Active} = \frac{\text{Today's Date} - \text{Resolution Date}_\text{oldest}}{\text{7 days}}
\end{equation}
$$

#### 1. The Numerator (The Duration in Days)

$$
\begin{equation}
\text{Today's Date} - \text{Resolution Date}_\text{oldest}
\end{equation}
$$

* This calculation determines the **total number of days** that have passed between a specific past event (the oldest issue resolution date) and the current day.
* The **result:** of this subtraction is a single integer representing the number of days.

#### 2. The Denominator (The Conversion Factor)

$$
\begin{equation}
\text{7 days}
\end{equation}
$$

* This constant is used to convert the total duration from **days into weeks**. Since there are 7 days in a week, dividing the total number of elapsed days by 7 gives the result in weeks.

---

#### 3. Variable Definitions

| Variable | Description |
| :--- | :--- |
| **$\text{Weeks Active}$** | The **output** of the formula—the total number of weeks the current issue has been under consideration or active, measured from a baseline event. |
| **$\text{Today's Date}$** | The **current date** on which the calculation is being performed. |
| **$\text{Resolution Date}_\text{oldest}$** | The specific **baseline start date** you are measuring from. This is crucial: it's the date the very first completed (resolved) issue in the hierarchy was closed. |

---

## Issue Completion Velocity

This formula measures how quickly work is moving through your system! This calculation gives you a **velocity score** for an issue's overall effort.

$$
\text{Issue Completion Velocity} = \frac{\text{Number of Closed Descendants}}{\text{Weeks Active}}
$$

---

### Issue Completion Velocity Explained

The formula calculates the **Issue Completion Velocity** as the ratio of the total work completed (closed issues in the hierarchy) to the time the `Given Issue` has been active (in weeks).

#### 1. The Numerator (The Workload)

$$
\text{Number of Closed Descendants}
$$

* This component represents the **total amount of work** (issues) completed that are related to the `Given Issue`.
* **Result:** The outcome is a count of the issues.

#### 2. The Denominator (The Time Elapsed)

$$
\text{Weeks Active}
$$

* This component is the **time taken to process the work** or the duration the work has been in progress, measured in weeks (as defined by your previous formula).
* **Result:** The outcome is a time duration in weeks.

---

#### 3. 🔍 Variable Definitions

| Variable | Description |
| :--- | :--- |
| **$\text{Issue Completion Velocity}$** | The **output** of the formula—a measure of the rate at which an issue's hierarchy is moving toward completion. A **higher** score suggests a faster rate of completion relative to the time spent. |
| **$\text{Number of Closed Descendants}$** | The **count** of all issues (including sub-tasks, bugs, or related stories) that have been **closed** and belong to the hierarchy of the primary issue being evaluated. |
| **$\text{Weeks Active}$** | The total number of **weeks** the current issue has been under consideration or active, measured from a baseline event (calculated by dividing days active by 7). |

# Inputs
`Given Issue` = HCMSTRAT-17

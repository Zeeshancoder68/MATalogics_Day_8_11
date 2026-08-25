# Task 9: AI Operations Manager (Autonomous Business Agent)

> An autonomous AI agent scheduled to check business activity every morning, analyze cross-departmental data, identify bottlenecks, execute permitted actions, and deliver a prioritized briefing to human management.

## System Architecture

The workflow follows a strict, linear pipeline to ingest data, reason, and output a human-in-the-loop report.

* **Trigger:** Schedule by Zapier (Configured to run Every Day in the morning).
* **Data Ingestion (Search Tools):** 
  * Zapier Tables - Sales Table: Checks for stuck or high-value deals[cite: 5].
  * Zapier Tables - Tasks Table: Checks for overdue tasks and heavy workloads[cite: 5].
  * Zapier Tables - Support Table: Checks for critical, unresolved customer tickets[cite: 5].
* **Reasoning Engine:** OpenAI ChatGPT API (Analyzes data, prioritizes problems, and recommends safe actions)[cite: 5].
* **Action Tool:** Zapier Tables (Creates follow-up tasks autonomously based on AI reasoning)[cite: 5].
* **Reporting:** Gmail (Delivers the formatted Daily Operations Report to management)[cite: 5].

## Autonomous Agent Logic & Safety Rules

The AI Operations Manager is strictly bound by compliance rules to ensure system integrity. It is programmed to identify problems and recommend actions rather than simply summarizing data[cite: 5].

**Safety Constraints:**
1. The agent cannot delete any records[cite: 5].
2. The agent cannot send external messages without explicit human approval[cite: 5].
3. The agent cannot change financial information[cite: 5].
4. The agent is restricted to taking predefined safe actions, such as generating internal follow-up tasks[cite: 5].
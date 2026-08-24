# Task 5: Customer Onboarding Pipeline

> A robust, automated CRM-style onboarding and lead management system built natively using Zapier[cite: 1].

---

## 1. Project Overview

This project automates customer intake, database record creation, visual pipeline management, stage-based routing, and delayed conditional checks entirely within the Zapier ecosystem without external CRM dependencies[cite: 1].

---

## 2. Tech Stack & Components

* **Frontend & Forms:** Zapier Forms / Interfaces[cite: 1]
* **Database & CRM:** Zapier Tables[cite: 1]
* **Visual Pipeline:** Zapier Kanban Board[cite: 1]
* **Workflow Automation:** Zapier Workflows (Zaps)[cite: 1]
* **Conditional Logic & Delays:** Paths by Zapier, Delay by Zapier, Filter by Zapier[cite: 1]
* **Notifications:** Gmail / Email by Zapier[cite: 1]

---

## 3. Schema & Architecture

### A. Form Fields (Intake)
The customer onboarding form captures the following 8 required data points[cite: 1]:
* **Client Name**[cite: 1]
* **Company**[cite: 1]
* **Email**[cite: 1]
* **Service**[cite: 1]
* **Project Budget**[cite: 1]
* **Start Date**[cite: 1]
* **Account Manager**[cite: 1]
* **Requirements**[cite: 1]

### B. Kanban Pipeline Stages
The CRM table and Kanban board are configured across 7 sequential columns[cite: 1]:
1. `New Lead`[cite: 1]
2. `Qualified`[cite: 1]
3. `Proposal`[cite: 1]
4. `Won`[cite: 1]
5. `Onboarding`[cite: 1]
6. `In Progress`[cite: 1]
7. `Completed`[cite: 1]

---

## 4. Automation Workflows

### Zap 1: CRM Intake Pipeline
* **Trigger:** New form submission via Zapier Forms[cite: 1].
* **Action (Catch & Update):** Locates the newly created record in Zapier Tables, updates the `Stage` field to **`New Lead`**, automatically calculates a 7-day onboarding deadline (`+7 days`) in the **`Due Date`** field, and maps client project details[cite: 1].
* **Confirmation:** Sends a personalized welcome email to the client via Gmail[cite: 1].

### Zap 2: Stage Routing & Delay Automation
* **Trigger:** Updated Record in Zapier Tables when the `Stage` field changes[cite: 1].
* **Branching Logic (`Paths`):**
  * **`New Lead` $\rightarrow$ `Qualified`:** Sends a qualification email[cite: 1].
  * **`Qualified` $\rightarrow$ `Proposal`:** Automatically triggers proposal creation tasks[cite: 1].
  * **`Won` $\rightarrow$ `Onboarding`:** Dispatches the onboarding welcome packet[cite: 1].
  * **`Onboarding` $\rightarrow$ `In Progress`:** Notifies the project manager[cite: 1].
  * **`In Progress` $\rightarrow$ `Completed`:** Sends the final project completion email to the customer[cite: 1].

### Extra Challenge Implementation (Stalled Lead Alert)
* **Delay Mechanism:** When a card enters the `Qualified` stage, a **Delay For (3 days)** step pauses execution[cite: 1].
* **Database Re-verification:** Executes a **Find Records** search using the client's unique `Record ID` to check their current table status[cite: 1].
* **Conditional Filtering:** Uses **Filter by Zapier** to check if the stage is still strictly `Qualified`[cite: 1]. If the lead has already moved forward, the Zap stops cleanly. If the lead has stalled for more than 3 days, an automated alert email is immediately dispatched to the assigned **Account Manager**[cite: 1].

---

## 5. Live Implementation Links
* **Kanban Pipeline:** [View Kanban Board](https://cmt6p510p00a7ro50mxawg2s.zapier.app/pipeline)[cite: 1]
* **Onboarding Form:** [View Submission Form](https://cmt74vcc4000sphbtzcv5mnsk.zapier.app/new-form)[cite: 1]
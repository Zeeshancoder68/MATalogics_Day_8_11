# Task 6: Recruitment Pipeline

> An automated recruitment management system for evaluating and routing developer candidates using Zapier natively[cite: 2].

---

## 1. Project Overview

This project automates the entire developer hiring lifecycle. It captures candidate applications, automatically scores and prioritizes them based on experience, and manages their progression through a visual Kanban pipeline with stage-specific email routing and stalled-candidate alerts[cite: 2].

---

## 2. Tech Stack & Components

* **Frontend & Forms:** Zapier Interfaces / Forms[cite: 2]
* **Database & CRM:** Zapier Tables[cite: 2]
* **Visual Pipeline:** Zapier Kanban Board[cite: 2]
* **Workflow Automation:** Zapier Workflows (Zaps)[cite: 2]
* **Logic & Delays:** Paths by Zapier, Delay by Zapier, Filter by Zapier, Formatter by Zapier[cite: 2]
* **Communications:** Gmail / Email by Zapier[cite: 2]

---

## 3. Schema & Architecture

### A. Form Fields (Application Portal)
The application form captures the following required data points[cite: 2]:
* **Candidate Name**[cite: 2]
* **Email**[cite: 2]
* **Phone**[cite: 2]
* **Position**[cite: 2]
* **Experience**[cite: 2]
* **Expected Salary**[cite: 2]
* **Resume**[cite: 2]
* **Portfolio**[cite: 2]
* **Availability**[cite: 2]

### B. Kanban Pipeline Stages
The backend Zapier Table and Kanban board track candidates across 7 sequential columns[cite: 2]:
1. `Applied`[cite: 2]
2. `Screening`[cite: 2]
3. `Technical Interview`[cite: 2]
4. `HR Interview`[cite: 2]
5. `Offer`[cite: 2]
6. `Hired`[cite: 2]
7. `Rejected`[cite: 2]

---

## 4. Automation Workflows

### Zap 1: Candidate Intake & Priority Logic
* **Trigger:** New application submitted via Zapier Forms[cite: 2].
* **Priority Analysis:** Evaluates the candidate's experience to assign priority[cite: 2]:
  * **5+ years:** `High`[cite: 2]
  * **2–4 years:** `Medium`[cite: 2]
  * **<2 years:** `Low`[cite: 2]
* **Action:** Creates the candidate record and Kanban card, mapping the assigned priority, and places the candidate in the **`Applied`** stage[cite: 2].

### Zap 2: Stage Routing & Notifications
* **Trigger:** Record updated in Zapier Tables (watches the `Stage` field)[cite: 2].
* **Branching Logic (`Paths`):**
  * **`Screening`:** Sends a screening email to the candidate[cite: 2].
  * **`Technical Interview`:** Sends an interview scheduling email to the candidate[cite: 2].
  * **`HR Interview`:** Sends a notification alert to the HR team[cite: 2].
  * **`Offer` / `Hired`:** Sends a congratulations email to the candidate[cite: 2].
  * **`Rejected`:** Sends a formal rejection email to the candidate regardless of previous stage[cite: 2].

### Extra Challenge: Stalled Candidate Alert
* **Logic:** Built directly into the `Screening` path[cite: 2].
* **Execution:** Once the screening email is sent, a **Delay For (5 days)** is triggered[cite: 2]. 
* **Verification:** Zapier re-searches the candidate record using their `Record ID` and passes it through a **Filter**. If the stage still exactly matches `Screening`, an automated alert is sent to the Recruiter notifying them of the stalled candidate[cite: 2].

---

## 5. Live Implementation Links
* **Kanban Pipeline:** [Insert Your Kanban Link Here]
* **Application Form:** [Insert Your Form Link Here]
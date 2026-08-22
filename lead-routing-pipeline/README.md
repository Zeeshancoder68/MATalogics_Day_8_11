# 🛠️ System Architecture: Automated Lead Intake & Routing Pipeline

**Author:** Zeeshan Sohail 
**Project Phase:** System Design & Logic Configuration

## 📑 Project Overview
This project details the architecture for an automated lead-capture and routing system designed for a high-volume sales team. The system eliminates manual data entry by capturing leads via a frontend form, autonomously calculating a dynamic "Lead Score" based on predefined business rules, storing the enriched record in a database, and selectively routing high-priority leads to the sales team.

## 🧩 Tech Stack & Modules
*   **Frontend Data Capture:** Zapier Interfaces
*   **Database / CRM:** Zapier Tables
*   **Compute / Logic:** Code by Zapier (JavaScript)
*   **Routing Logic:** Filter by Zapier
*   **Notifications:** Slack Integration

---

## 📸 System Configuration & Proof of Logic
*(Note: Workflow execution was halted due to trial limitations during the final deployment phase, but all logic, routing, and data mapping were successfully configured and verified via step-by-step unit testing.)*
<img width="3830" height="1973" alt="Zapier_Lead_Intake_System" src="https://github.com/user-attachments/assets/bbab1fa1-eb4d-4eeb-9713-490e16c0e759" />
<img width="3838" height="297" alt="Zapier_Lead_Table" src="https://github.com/user-attachments/assets/e0954e89-6e9b-4248-ab70-bf847765bcb4" />
<img width="1246" height="1465" alt="LeadIntake-Slack-Update-zapier" src="https://github.com/user-attachments/assets/ddd03ef5-85a7-41e6-806f-fae4e5cefee0" />



---

## ⚙️ Detailed Workflow Execution Logic

### Phase 1: Ingestion (Zapier Interfaces)
The automation is triggered the moment a prospect submits the **Sales Lead Intake** form. The system captures standard contact data alongside critical qualifying metrics:
*   `Budget`
*   `Urgency` (Low, Medium, High)
*   `Lead Source` (Website, LinkedIn, Instagram, Referral, Advertisement)

### Phase 2: Compute & Enrichment (Code by Zapier)
Instead of relying on basic linear mapping, the raw form data is passed into a custom JavaScript execution node. This script processes the variables to output a unique `Lead ID` and calculates a weighted `Lead Score` based on the following criteria:

| Metric | Condition | Point Value |
| :--- | :--- | :--- |
| **Urgency** | High / Medium / Low | +30 / +20 / +10 |
| **Budget** | > $5k / $1k-$5k / < $1k | +30 / +20 / +10 |
| **Source** | Referral / LinkedIn | +20 / +15 |

Based on the total integer, the script assigns a priority tier: **Hot (70+)**, **Warm (40-69)**, or **Cold (<40)**.

### Phase 3: Database Archiving (Zapier Tables)
The enriched dataset—combining the original form inputs with the generated `Lead ID`, `Lead Score`, and `Priority`—is autonomously pushed to a dedicated **Leads** table. 
*   **Default Status:** Every new entry is automatically tagged with a "New" status for pipeline tracking.

### Phase 4: Conditional Routing (Filter by Zapier)
To prevent alert fatigue for the sales team, a strict routing filter is applied. The system evaluates the `Priority` string generated in Phase 2. The pipeline is instructed to immediately halt execution unless the `Priority` exactly matches **"Hot"**.

### Phase 5: Team Notification (Slack)
If a lead bypasses the conditional filter, a formatted payload is dispatched to the `#sales` Slack channel. The alert dynamically injects the prospect's Name, Company, Budget, and Calculated Score directly into the message, allowing the sales team to action the high-value lead instantly.

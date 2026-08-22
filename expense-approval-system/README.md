# 🛠️ System Architecture: Employee Expense Approval & Risk Routing

**Project Phase:** Internal Automation & Conditional Logic

## 📑 Project Overview
This project details the architecture for an automated employee expense approval system. It replaces manual email chains with a centralized portal that automatically evaluates financial risk, checks for required documentation (receipts), and dynamically routes the request to the appropriate parties based on predefined business logic.

## 🧩 Tech Stack & Modules
* **Frontend Data Capture:** Zapier Interfaces
* **Database / CRM:** Zapier Tables
* **Compute / Risk Logic:** Code by Zapier (JavaScript ES6)
* **Conditional Routing:** Paths by Zapier
* **Notifications:** Slack Integration

---

## 📸 System Configuration & Proof of Logic

<img width="1917" height="1882" alt="Workflow_expense-approval-system" src="https://github.com/user-attachments/assets/1e25b19d-4d7b-4f73-bd8c-883c0772a624" />

<img width="1857" height="1820" alt="js-logic" src="https://github.com/user-attachments/assets/356f6767-d656-4b73-9b41-f4444a46a352" />

<img width="1453" height="1267" alt="slack-alert" src="https://github.com/user-attachments/assets/3f3fc22f-4f35-4718-a399-880b687a1f4f" />

<img width="1727" height="1495" alt="path-logic" src="https://github.com/user-attachments/assets/79202e20-41a3-41a2-82be-ed9a443326fe" />


---

## ⚙️ Detailed Workflow Execution Logic

### Phase 1: Ingestion (Zapier Interfaces)
Employees submit expenses via a custom frontend portal. The system captures critical variables including `Employee Name`, `Department`, `Expense Type`, `Amount`, and a `Receipt Upload` file.

### Phase 2: Risk Assessment & Validation (Code by Zapier)
A custom JavaScript execution node processes the raw numerical amount and file attachments to determine risk and status before logging:
1. **Risk Calculation:** 
   * Amount < $100 = `Low` Risk
   * Amount $100 - $500 = `Medium` Risk
   * Amount > $500 = `High` Risk
2. **Validation:** The script checks if the `Receipt Upload` field is null. If missing, it immediately overrides the status to `Receipt Required`.
3. **ID Generation:** Generates a unique `Request ID` (e.g., `EXP-4921`) for tracking.

### Phase 3: Database Logging (Zapier Tables)
The system creates a new immutable record in the **Expense Requests** table, logging the raw form data alongside the computed `Risk Level` and `Approval Status`.

### Phase 4: Conditional Routing (Paths by Zapier)
The workflow splits into three distinct operational paths based on the computed data:

* **Path A: Exception Handling (Missing Receipt)**
  * **Trigger:** `Status` exactly matches `Receipt Required`.
  * **Action:** Halts approval and pings the employee via Slack, dynamically injecting the expense details and prompting them to resubmit with documentation.
* **Path B: Auto-Approval (Low Risk)**
  * **Trigger:** `Risk` exactly matches `Low` AND `Status` does not match `Receipt Required`.
  * **Action:** Bypasses management review and autonomously updates the Zapier Tables record `Approval Status` to `Approved`.
* **Path C: Management Review (Medium/High Risk)**
  * **Trigger:** `Status` exactly matches `Pending Approval`.
  * **Action:** Dispatches a formatted alert to the management Slack channel containing employee details, risk level, amount, and a direct URL to view the uploaded receipt for manual sign-off.

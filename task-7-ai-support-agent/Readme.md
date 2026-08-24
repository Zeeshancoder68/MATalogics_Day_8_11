# Task 7: AI Customer Support Resolution Agent

> An autonomous support agent that analyzes customer issues, determines intent, and routes or resolves tickets automatically without human intervention[cite: 2].

## System Architecture

* **Trigger:** Zapier Tables (New Record submission)[cite: 2].
* **AI Engine:** OpenAI ChatGPT API (System prompt strictly categorizes intent and extracts severity)[cite: 2].
* **Database:** Zapier Tables (Relational setup utilizing a Customer Table and a Ticket Table)[cite: 2].
* **Action Modules:** Zapier Paths, Zapier Filters, Zapier Tables Search/Update/Create, Gmail[cite: 2].

## Autonomous Routing Logic

The AI acts as a router, analyzing the natural language issue and directing the payload into one of five distinct execution paths[cite: 2]:

* **Path A (Password Problem):** Sends an automated password reset instruction email via Gmail[cite: 2].
* **Path B (Billing Question):** Retrieves customer billing data from the database and updates the ticket action status[cite: 2].
* **Path C (Duplicate Payment):** Routes to the finance queue and creates a specialized Finance ticket[cite: 2].
* **Path D (Technical Issue):** Routes to the IT queue and creates a Technical Support ticket[cite: 2].
* **Path E (Angry/Urgent):** Detects high severity and escalates by sending an immediate alert to human support[cite: 2].

## Duplicate Prevention Mechanism

* **Logic:** Prior to creating new finance or technical tickets, the system executes a search query against existing database records[cite: 2].
* **Execution:** A Zapier Filter evaluates the output of the search step[cite: 2].
* **Resolution:** The workflow is halted if a matching record ID already exists for that customer, successfully preventing redundant ticket creation[cite: 2].
# 🏥 AI Clinic Appointment & Conflict Resolution Agent

## 📑 System Architecture Overview
An autonomous scheduling agent designed to handle patient intake, extract temporal data, and execute real-time database validation to prevent scheduling conflicts. The system converts relative natural language (e.g., "tomorrow at 4 PM") into hard calendar dates, queries the clinic's database, and conditionally routes the payload to block double-bookings before dispatching a Slack confirmation.

## 🧩 Tech Stack
* **Conversational Frontend:** Zapier Chatbots
* **NLP & Data Extraction:** AI by Zapier (GPT-4o-mini Structured Data)
* **Database Querying & Logging:** Zapier Tables (Find/Create Record)
* **Logic & Routing:** Filter by Zapier
* **Alerting:** Slack API

## ⚙️ Core Engineering Highlights

### 1. Dynamic Date Translation
The agent processes unstructured conversational text and converts relative timeframes ("next Monday") into strict `YYYY-MM-DD` formats required by the database architecture. 

### 2. Autonomous Double-Booking Prevention
Before writing any data, the workflow executes a 3-point cross-reference query against the Zapier Tables database (matching Doctor + Date + Time). A logic gate (Filter) evaluates the search output; if an existing record ID is detected, the workflow is instantly halted, and the chatbot falls back to suggest alternative slots.

### 3. Automated Dispatch
Upon passing the conflict-resolution gate, the enriched payload is logged to the CRM, and a formatted confirmation ticket is pushed to the clinic's administrative Slack channel.
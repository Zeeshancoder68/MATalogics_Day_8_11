# Task 8: AI Instagram Content Agent

> An autonomous social media manager that decides content topics based on historical data, generates brand-aligned posts, self-evaluates quality, and routes for human approval[cite: 1].

## System Architecture

* **Trigger:** Zapier Tables (New Record in `Content Ideas` table)[cite: 1].
* **Research Phase:** Zapier Tables (Find Records in `Instagram Content Calendar`)[cite: 1].
* **AI Engines:** OpenAI ChatGPT API (Dual-agent setup: Content Generator and Quality Critic)[cite: 1].
* **Action Modules:** Zapier Paths, Zapier Tables Create Record, Gmail[cite: 1].

## Autonomous Agent Logic

This workflow utilizes a dual-agent critic system to ensure quality control without human intervention until the final step[cite: 1]:

1. **Contextual Generation:** The Content Generator analyzes the requested topic and the recent posting history[cite: 1]. It features autonomous behavior: if it detects three recent "Educational" posts, it automatically pivots to a "Case Study" format[cite: 1].
2. **AI Quality Critic:** A secondary AI prompt evaluates the generated post against a strict rubric (hook strength, clarity, relevance, unsupported claims) and assigns a score from 1 to 10[cite: 1].
3. **Deterministic Routing:** 
   * **Path A (Score < 7):** The post is rejected and sent to a rewrite node[cite: 1].
   * **Path B (Score >= 7):** The post is approved, logged into the `Instagram Content Calendar` with an "Awaiting Approval" status, and emailed to the marketing team for final sign-off[cite: 1].
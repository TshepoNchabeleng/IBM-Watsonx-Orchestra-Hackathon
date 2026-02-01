# Project: Autonomous Patent Lifecycle Orchestrator
**Version:** 1.0.0  
**Platform:** IBM watsonx Orchestrate  
**Documentation Date:** February 1, 2026

---

## 1. Executive Summary
This project outlines a **multi-agent ecosystem** designed to automate the intellectual property lifecycle. By chaining specialized agents, we have created a workflow that moves an idea from a **raw concept** to a **formalized legal filing** with zero data loss.

---

## 2. System Architecture
The system is divided into four critical phases, each managed by a dedicated agent.

### **Phase A: The Interviewer Agent**
The "gatekeeper" of the system. It uses an inquisitive persona to ensure "Garbage In, Garbage Out" is avoided.
* **Goal:** Extract the **4 Pillars of Patentability**.
    * **Field:** Industry classification.
    * **Components:** Physical/software parts.
    * **Mechanism:** The internal logic or "how it works."
    * **Novelty:** The unique differentiator.
* **Key Tool:** `brief_generator_tool` (Normalizes chat data into a structured brief).

### **Phase B: The Check-Patent Agent**
The technical investigator. This agent bridges the gap between the user and global patent databases.
* **Technical Implementation:** Uses a **Python-based Data Aggregator**.
* **Process:** 1. Scans patent databases via API.
    2. Uses custom logic to extract `title`, `abstract`, and `publication_number`.
    3. Formats results into an `llm_ready_prompt` for the next stage.

### **Phase C: The Design-Advisor Agent**
The technical consultant. This agent provides high-level strategy based on real-world data.
* **Function:** Identifies "Prior Art" conflicts.
* **Core Action:** Suggests a **Design Pivot**. If a patent is found that overlaps with the user's idea, the advisor suggests a specific mechanical or software change to restore novelty.

### **Phase D: The Drafting & Filing Agent**
The "closer" of the ecosystem. This agent handles the transition from AI to Human Legal Teams.
* **Tool 1 (GenAI Drafter):** Uses a **Senior Patent Attorney** system prompt to write an Invention Disclosure Form (IDF) in formal legal terms.
* **Tool 2 (Auto-Filer):** A secure email connector that triggers a **Submission Form**.
* **Guardrail:** Features a **"Confirm Submission"** button to ensure no data is sent without a final human-in-the-loop review.

---

## 3. Tool Inventory & Descriptions

| Tool Name | Type | Description |
| :--- | :--- | :--- |
| **Invention Brief Gen** | GenAI / Logic | Converts raw transcripts into professional JSON summaries. |
| **Comparison Logic** | **Python (Custom)** | A backend tool that cleans and aggregates patent search results. |
| **Legal Drafter** | LLM / GenAI | A high-fidelity writer that drafts IDFs using vocabulary like *"embodiments"* and *"plurality"*. |
| **Submission Gateway** | API / Email | Securely transmits documentation to `intake@lawfirm.com`. |

---

## 4. Test Cases & Validation
To prove system reliability, we implemented the following test scenarios:

* **TC-01 (Oxy-Shield):** Tested end-to-end flow for a smart air-purifying curtain.
* **TC-02 (Aqua-Pulse):** Tested the **Design-Advisor's** ability to suggest a frequency pivot for an ultrasonic water filter.
* **TC-03 (Safety Halt):** Verified the agent stops the filing process if the user expresses hesitation or if the search finds 100% similarity.

---

## 5. Implementation Log
* **Step 1:** Defined the agent personas and conversation flow.
* **Step 2:** Developed the **Python Comparison Tool** to handle search list data without external SDK errors.
* **Step 3:** Integrated **Generative AI** nodes to replace static templates with adaptive legal drafting.
* **Step 4:** Configured the **watsonx Orchestrate** Skill Studio to handle "Confirm" actions for secure email delivery.

---

> **Legal Disclaimer:** This system is an AI-assisted tool. All drafts produced must be reviewed by a licensed Patent Attorney before submission to the USPTO or relevant authorities.

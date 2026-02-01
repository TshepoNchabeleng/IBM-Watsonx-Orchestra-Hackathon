# IBM-Watsonx-Orchestra-Hackathon
Project: Autonomous Patent Lifecycle Orchestrator
Version: 1.0.0

Platform: IBM watsonx Orchestrate

Status: System Integration Complete (UAT Ready)

1. Executive Summary
The goal of this project was to build a seamless, multi-agent ecosystem that automates the transition from an "inventor's raw idea" to a "lawyer-ready patent filing." The system utilizes specialized agents to handle data intake, prior art analysis, design consultation, and legal document generation.

2. System Architecture & The "Baton" Handoff
The system is built on a linear "Skill Chain" where data persistence is maintained across four distinct agents.

Phase A: The Intake (Interviewer Agent)
The Mission: To extract high-quality technical data using the "4 Pillars of Patentability".

Process: The agent engages in a conversational loop until it identifies:

Field: The industry/category.

Components: The physical/digital parts.

Mechanism: The "How it works" logic.

Novelty: The perceived unique value.

Tool Used: brief_generator_tool – A normalization skill that converts the chat transcript into a structured Invention Brief.

Phase B: The Investigation (Check-Patent & Comparison Tool)
The Mission: To find existing patents and identify the "Technical Delta."

Process: The system takes the Brief and triggers a search.

The Python Tool: We developed a custom Python skill in the Orchestrate Code Editor to handle data transformation.

Logic: It loops through a List[Dict] of search results, extracting the Title, Abstract, Publication Number, and Link.

Output: It produces a llm_ready_prompt, a consolidated string that allows a Generative AI model to read all competitors at once.

Phase C: The Strategy (Design-Advisor Agent)
The Mission: To act as a technical consultant.

Process: Using the output from the Python tool, this agent identifies overlaps.

Guidelines: If a conflict is found, the agent is programmed to suggest a "Design Pivot" (e.g., changing a frequency, material, or sensor trigger) to ensure the inventor avoids infringement.

Phase D: The Filing (Drafting & Filing Agent)
The Mission: To generate legal-grade documentation and submit it.

The GenAI Tool: A custom node with a "Senior Patent Attorney" system prompt.

Function: Automatically fills out an Invention Disclosure Form (IDF) using formal legal vocabulary ("plurality," "comprising," "embodiments").

The Submission Tool: A secure email connector (Outlook/Gmail).

Feature: A "Confirm Submission" button that sends the final draft to the law firm's intake address.

# TCAS Navigator: The AI Companion for Thai University Admissions
Guiding Thai students through the Thai University Central Admission System (TCAS) with AI Agents for schedule tracking, criteria search, and reminders.

## Problem Statement
For over 300,000 Thai high school students every year, the university admission system (TCAS) is a nightmare of information overload. Students must navigate four distinct admission rounds (Portfolio, Quota, Admission, Direct Admission), dozens of exams schedule (TGAT, TPAT, A-Level), and complex scoring criteria that vary by every university faculty.

The problem isn't just finding information; it's managing the timeline. Students constantly miss critical registration deadlines or apply to faculties without realizing they lack specific prerequisites because the data is scattered across massive announcements and confusing websites. There is no centralized tool that proactively helps them manage their personal admission journey.

## Why Agents?
To Solve the university admission puzzle requires more than simple search; it requires distinct types of reasoning:

* **Specialization:** We separate "Knowledge Retrieval" (admission details) from "Deterministic Data" (calendar dates) to ensure accuracy.
* **Orchestration:** We have an intelligent router to handle complex requests like "Find the TGAT date and set a reminder" in a single flow.
* **Centralization:** The Agent act as proactive tool that helps students navigate their personal admission plans.

## The Build
This project was built using a modern AI stack:

* **Framework:** Google ADK (Agent Development Kit) for defining agents, tools, and managing sessions.
* **Model:** Gemini 2.5 Flash Lite for fast, cost-effective reasoning for text query only.
* **Database:** Supabase (PostgreSQL) for storing course requirements, user reminders and sessions.
* **Tools:** Custom Python functions for Agents.
* **Deployment:** Vertex AI Agent Engine.

## What I Created
I built a Hierarchical Multi-Agent System powered by the Google Agent Development Kit (ADK) and Gemini 2.5 Flash Lite.

* 🧠 **Navigator Agent (The Orchestrator):** The root agent that interacts with the user. It routes queries to the correct specialist and manages the session state (saving user name/email).
* ℹ️ **Info Agent:** Uses curl request to Database (Supabase) and TCAS API to retrieve admission criteria and seat counts for specific universities.
* 📅 **Calendar Agent:** A deterministic agent that reads raw JSON/Markdown files to provide 100% accurate dates for exams and application rounds (preventing LLM hallucinations on critical dates).
* 🔔 **Reminder Agent:** Manages the reminder database. It handles creating, reading, and deleting exam reminders. It features Long-Running Operations (Human-in-the-loop) to ask for confirmation before deleting reminder.

## Architecture Diagram:
<img width="2752" height="1536" alt="inbox_30384891_80bcec622790d291960e56f777b5de54_Gemini_Generated_Image_u74nhhu74nhhu74n" src="https://github.com/user-attachments/assets/10be3632-2054-41e0-b8b0-a9e95fe64ad6" />

## Demo
```
    User > Give me a admission details of medicine chulalongkorn
    TCAS_Orchestrator > admission details of round 1 medicine chulalongkorn are as follows:
    **Round 1 (Portfolio):**
    *   **Accepted:** 24 students
    *   **Qualifications:** For students graduating from the standard curriculum and international curriculum.
    *   **Scores:** Portfolio 50%, Interview 50%
    **Note:**
    *   Applicants graduating from vocational curricula, non-formal education curricula (GIA), or GED are         not accepted in any round.
    *   Tuition fee: 34,000 Baht per semester.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    User > TGAT/TPAT exam date?
    TCAS_Orchestrator > The TGAT/TPAT registration period starts from October 30, 2025, to November 6, 2025. The exams will be held from December 13-15, 2025.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    User > Set reminder for TGAT exam and note test test and send to email user123@gmail.com at date 2025-12-20
    TCAS_Orchestrator > I've set a reminder for the TGAT exam on 2025-12-20 with the note "test test" and sent it to koonmartza123@gmail.com.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    User > List all notification reminders for my email user123@gmail.com
    TCAS_Orchestrator > Here are all your reminders:
    1.  TPAT3 (Date: 2025-12-01), Note: TPAT3 exam
    2.  A-Level Physic (Date: 2025-12-20), Note: test A-level phy
    3.  TGAT (Date: 2025-12-20), Note: test test
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    User > delete a notification reminder TGAT for my email user123@gmail.com
    🛑 **Action Required:** The Reminder Agent needs confirmation.
       👉 Do you confirm this action? (yes/no):  no
       User decided: ❌ Rejected
    TCAS_Orchestrator > The deletion was cancelled. Would you like to try deleting it again?
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    User > delete a notification reminder TGAT for my email user123@gmail.com
    🛑 **Action Required:** The Reminder Agent needs confirmation.
       👉 Do you confirm this action? (yes/no):  yes
       User decided: ✅ Approved
    TCAS_Orchestrator > I have successfully deleted the reminder for TGAT for user123@gmail.com. The reminder was for the exam on 2025-12-20.
```

## If I had more time, this is what I'd do
* **Personalized Score Calculation:** I would add a "Calculator Agent" that takes the student's grades, compares them against the retrieved criteria, and predicts their chance of admission.
* **Line/Messenger Integration:** Deploy the agent to Line Messaging API, as that is the primary communication channel for Thai students.
* **RAG Expansion:** Ingests official TCAS PDF manuals and exam blueprints to provide accurate answers to edge-case regulation questions and specific exam details.




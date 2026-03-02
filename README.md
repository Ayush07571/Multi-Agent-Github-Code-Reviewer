# 🤖 Multi-Agent Sequential Code Reviewer (n8n)

A high-fidelity GitHub Pull Request reviewer built on n8n that utilizes a **Smart Sequential Refinement Loop**. This workflow dynamically routes PRs based on size and uses a multi-stage AI pipeline to ensure technical accuracy and human-like feedback.

## 🚀 The "Smart Pipeline" Architecture

This workflow implements a logic-aware pipeline that adapts to the size of the contribution:

### 🚦 The Routing Logic (`If1` Node)

* **Large PRs (>20 Changes):** Trigger the full **4-Stage Sequential Loop** for deep analysis.
* **Small PRs (≤20 Changes):** Route to the **Fast-Track Auditor (AI Agent 4)** for a supportive, one-sentence verification to avoid over-engineering small updates.

### 🧠 The Sequential Loop (Large PRs)

1. **Stage 1: Initial Auditor (AI Agent 1):** Performs the first pass review using **Step-3.5-Flash**, focusing on general logic and code quality.
2. **Stage 2: Critical Reviewer (AI Agent):** Analyzes the first output to identify missed gaps or technical debt using **Nvidia Nemotron-3**.
3. **Stage 3: Synthesizer (AI Agent 2):** Consolidates findings from previous agents, removing redundancies and ensuring the feedback is cohesive.
4. **Stage 4: Polishing Agent (AI Agent 3):** Uses **Nvidia Nemotron-12b** to "humanize" the tone and strictly format the output into a 3-4 line summary.

## 🛡️ Reliability & Oversight

* **Human-in-the-Loop:** Before any comment is posted to GitHub, the workflow sends the finalized suggestion to the user via **Gmail**. The user must approve it via a dropdown form ("Yes/No").
* **Safe-String Processing:** A JavaScript node pre-processes the `git diff`, escaping backticks and triple backticks to prevent formatting breaks in the AI prompts.
* **Automatic Labeling:** Once a review is approved and posted, the PR is automatically tagged with a `ReviewedByAI` label for project tracking.

## 🛠️ Setup Instructions

1. **Import:** Download the `Github_multi_AI_agent_code_reviewer.json` and import it into your n8n instance.
2. **Credentials:** * **GitHub (OAuth2):** For triggers, posting comments, and labeling.
* **Gmail (OAuth2):** For the manual approval step.
* **OpenRouter:** For access to Step-3.5 and Nvidia Nemotron models.


3. **Webhook:** Configure the GitHub Trigger to listen for `pull_request` events on your target repository.
4. **Deploy:** Set the workflow to **Active**.

## 🧠 Why this works

By combining **Dynamic Routing** with **Sequential Refinement**, the system provides deep technical audits for complex changes while remaining lightweight and supportive for minor documentation or style updates. This prevents "AI fatigue" for developers receiving the feedback.

This is a great addition. Since this is a college project, showing that you understand the **social** and **operational** challenges of Open Source (not just the technical ones) will make your work stand out to professors and recruiters.

## 🌟 Open Source & Educational Impact

This project was designed specifically to bridge the gap between **Student Contributors** and **Maintainers** in the open-source ecosystem.

* **Reducing Maintainer Burnout:** For project owners, the "Cognitive Load" of switching from development to reviewing a messy PR is high. This tool acts as a **Teaching Assistant**, pre-digesting diffs into actionable summaries.
* **Instant Feedback Loop:** New contributors often lose interest if their PR sits unaddressed for days. This bot provides immediate, high-quality technical feedback, keeping the momentum of the contribution alive.
* **AI-Powered Mentorship:** By using a **Sequential Refinement** model, the feedback isn't just a list of errors—it’s a structured suggestion that explains the *why* behind a fix, helping students learn better coding patterns.
* **Lowering the Barrier to Entry:** Automated labeling (`ReviewedByAI`) and human-in-the-loop approval ensure that the repository remains professional and welcoming, encouraging more students to submit their first pull request.

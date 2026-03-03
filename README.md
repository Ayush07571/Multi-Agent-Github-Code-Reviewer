## 🤖 Multi-Agent Sequential Code Reviewer (n8n)

A high-fidelity GitHub Pull Request reviewer built on n8n that utilizes a **Smart Sequential Refinement Loop**. This project is designed specifically for **Open Source Maintainers and Student Contributors** to scale mentorship and reduce manual review bottlenecks.

---

## 🚀 The "Smart Pipeline" Architecture

This workflow implements a three-tier routing logic to handle PRs based on their complexity and size:

### 🚦 Dynamic Routing Logic (`If1` & `If2` Nodes)

* **Massive PRs (> 200 Changes):** Automatically flagged for human intervention with a `waitingForHuman` label to prevent AI hallucination on overly large diffs.
* **Standard PRs (21–200 Changes):** Trigger the full **4-Stage Sequential Loop** for deep technical auditing.
* **Small PRs (≤ 20 Changes):** Routed to the **Fast-Track Auditor (AI Agent 4)** for a supportive, one-sentence verification.

### 🧠 The Sequential Refinement Loop

1. **Stage 1: Initial Auditor (AI Agent 1):** Performs the first pass using **Step-3.5-Flash** to identify logic errors and security risks.
2. **Stage 2: Critical Reviewer (AI Agent):** Analyzes the first agent's output using **Nvidia Nemotron-3** to identify gaps or technical debt.
3. **Stage 3: Synthesizer (AI Agent 2):** Consolidates findings from previous stages, ensuring feedback is comprehensive without being redundant.
4. **Stage 4: Polishing Agent (AI Agent 3):** Uses **Nvidia Nemotron-12b** to humanize the tone and strictly format the output into a concise 3-4 line summary.

---

## 🌟 Open Source & Educational Impact

* **Reducing Maintainer Burnout:** Acts as a "Teaching Assistant" by pre-digesting diffs into actionable summaries, allowing maintainers to focus on architectural decisions.
* **Instant Feedback Loop:** Provides student contributors with immediate technical feedback, keeping the momentum of open-source contributions alive.
* **AI-Powered Mentorship:** The sequential model explains the *why* behind a fix, helping students learn better coding patterns through automated peer review.

---

## 🛡️ Reliability & Security

* **Human-in-the-Loop:** Before any comment is posted to GitHub, the workflow sends the finalized suggestion via **Gmail** for manual "Yes/No" approval.
* **Universal Compatibility:** Uses dynamic expressions to pull repository and owner metadata, allowing the workflow to function across any repository it is connected to.
* **Safe-String Processing:** A custom JavaScript node cleans code diffs, escapes formatting-breakers (like triple backticks), and removes binary data to ensure prompt stability.

---

## 🛠️ Setup Instructions

1. **Import:** Download the `github-ai-reviewer.json` from this repo and import it into your n8n instance.
2. **Credentials:** Configure credentials for **GitHub (OAuth2)**, **Gmail (OAuth2)**, and **OpenRouter**.
3. **Webhook:** Configure the GitHub Trigger node to listen for `pull_request` events on your target repository.
4. **Deploy:** Set the workflow to **Active** to start receiving automated, high-quality code reviews.

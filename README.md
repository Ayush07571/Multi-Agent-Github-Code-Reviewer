# 🤖 Multi-Agent Sequential Code Reviewer (n8n)

A high-fidelity GitHub Pull Request reviewer built on n8n that utilizes a **Sequential Self-Refinement Loop**. Instead of a single-pass analysis, this workflow chains multiple specialized AI agents to audit, critique, and humanize code suggestions before they are presented to the developer.

## 🚀 The "Chain of Thought" Architecture
This workflow implements a 4-stage sequential pipeline to ensure maximum accuracy and helpful, "human-like" feedback:

* **Stage 1: The Initial Auditor (AI Agent 1)** Receives the raw `git diff` from the GitHub Trigger and performs the first pass review using the **DeepSeek Chat** model.
  
* **Stage 2: The Critical Reviewer (AI Agent)** Analyzes the first agent's output, identifies missed issues, and suggests enhancements to the initial findings. It leverages **Nvidia Nemotron-3** for a distinct technical perspective.

* **Stage 3: The Synthesizer (AI Agent 2)** Combines the findings from the previous stages into a single cohesive response while eliminating redundancies. It ensures the feedback is comprehensive yet efficient.

* **Stage 4: The Polishing Agent (AI Agent 3)** Final pass to "humanize" the comment. It strictly formats the output into a concise **3-4 line summary** to ensure readability on GitHub.

## 🛡️ Reliability & Oversight
* **Human-in-the-Loop:** After 4 stages of AI refinement, the final comment is sent to the user via Gmail for a manual "Yes/No" approval.
* **Pre-Processing:** A custom JavaScript node cleans the code diffs, escapes formatting-breakers (like backticks), and removes binary data to ensure prompt stability.
* **Automated Labeling:** Upon successful review, the GitHub PR is automatically tagged with a `ReviewedByAI` label.

## 🛠️ Setup Instructions
1. **Import:** Download the `github-ai-reviewer.json` from this repo and import it into your n8n instance.
2. **Credentials:** Set up your credentials for **GitHub (OAuth2)**, **Gmail (OAuth2)**, and **OpenRouter**.
3. **Webhook:** Configure the GitHub Trigger node to listen for `pull_request` events on your target repository.
4. **Deploy:** Set the workflow to **Active** and start receiving automated, high-quality code reviews.

## 🧠 Why this works
By moving from parallel agents to a **Sequential Refinement** model, the system acts as its own "Senior Architect." If the first agent misses a security flaw or a logic error, the subsequent agents are specifically prompted to find those gaps and correct the previous response.

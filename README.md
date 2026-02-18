# 🤖 Multi-Agent AI Code Reviewer (n8n)

An automated GitHub Pull Request reviewer that uses a committee of AI agents to provide high-accuracy, human-vetted feedback.

## 🚀 The Architecture
This project solves the "AI Hallucination" problem by using **Consensus-Based Reviewing**:
* **Trigger:** GitHub Webhook on Pull Request.
* **Data Prep:** A custom JavaScript node cleans the git diff and prepares it for LLM consumption.
* **The Committee:** Three parallel agents (DeepSeek, Nemotron-3, etc.) review the code using specific best practices pulled from a **Google Sheets Knowledge Base**.
* **The Aggregator:** A summary agent (AI Agent 3) reconciles the three reviews, removes duplicates, and formats the output.
* **Human-in-the-Loop:** Before anything is posted to GitHub, the user receives a Gmail notification with a "Yes/No" form to approve or reject the AI's comment.
* **Final Action:** Once approved, the review is posted as a comment on the PR and the issue is labeled `ReviewedByAI`.

## 🛠️ Setup
1. Import the `github-ai-reviewer.json` into your n8n instance.
2. Connect your **GitHub**, **Gmail**, and **OpenRouter** credentials.
3. Link your own **Google Sheet** containing your team's coding standards.
4. Set the GitHub Webhook to trigger on `Pull Request` events.

## 🧠 Why this is different
Unlike simple "Prompt and Post" bots, this system ensures quality through **distributed logic** and **human oversight**, making it safe for production-grade repositories.

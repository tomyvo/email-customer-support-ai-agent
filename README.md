# 🌟 Email Customer Support Automation Workflow

Welcome to the **Email Customer Support Automation** workflow! This powerful n8n workflow leverages AI to handle incoming customer emails, intelligently consult Google Drive documents, and provide professional, polite, and accurate responses—all automatically. 🚀

---

## 🎯 Overview

This workflow automates email-based customer support with these main capabilities:

1. **Receive incoming emails** via Gmail.
2. **Analyze the email content** using an AI agent (powered by Mistral via Ollama).
3. **Fetch relevant documents** from Google Drive to provide precise responses.
4. **Generate structured, polite replies** in HTML format.
5. **Send the reply** back to the original sender automatically.

The workflow ensures that responses are **accurate, customer-focused, and based solely on real information** from the available documents. ❌ No invented answers, ✅ only verified info.

---

## 🧩 Workflow Nodes

Here’s a breakdown of each node and its function:

### 1. Gmail Trigger 📬

- **Type:** `n8n-nodes-base.gmailTrigger`
- **Purpose:** Polls Gmail for new incoming messages.
- **Configuration:**
  - Polls **every minute**.
  - Uses Gmail OAuth2 credentials.

> This node is the starting point of the workflow, catching every customer email as it arrives.

---

### 2. AI Agent 🤖

- **Type:** `@n8n/n8n-nodes-langchain.agent`
- **Purpose:** Acts as the main AI engine to process emails.
- **Functionality:**
  - Reads the email subject and snippet.
  - Understands the **customer intent**.
  - Fetches relevant information from Google Drive if needed.
  - Generates a **structured and polite response**.
- **Important Instructions for the AI Agent:**
  - NEVER invent information.
  - Always consult available documents first.
  - Ask politely for clarification if the email lacks information.
  - Keep responses clear, structured, and professional.
  - Use short paragraphs, no unnecessary jargon.
  - Use **only content from documents and email text**.

---

### 3. Ollama Chat Model 🧠

- **Type:** `@n8n/n8n-nodes-langchain.lmChatOllama`
- **Purpose:** Provides the underlying language model (Mistral) for generating responses.
- **Configuration:** Connects directly to the AI Agent node.

---

### 4. Download File in Google Drive 📂

- **Type:** `n8n-nodes-base.googleDriveTool`
- **Purpose:** Downloads relevant documents from Google Drive to assist the AI in providing accurate answers.
- **Configuration:**
  - Predefined file IDs (e.g., Policy and FAQ document).
  - Uses Google Drive OAuth2 credentials.

> The AI uses this file as a trusted source to ensure all responses are **factual and accurate**.

---

### 5. Code in JavaScript 💻

- **Type:** `n8n-nodes-base.code`
- **Purpose:** Formats the AI output into **HTML** for email readability.
- **Features:**
  - Converts line breaks (`\n`) to `<br>`.
  - Wraps paragraphs in `<p>` tags for clean HTML output.
- **Example Output:**  
  ```html
  <p>Hello,</p>
  <p>Thank you for your inquiry. Based on our documents...</p>

---

### 6. Reply to a Message ✉️

Type: n8n-nodes-base.gmail

Purpose: Sends the AI-generated response back to the customer.

Configuration:

Replies only to the original sender.

Sets AI Agent as the sender name.

Uses Gmail OAuth2 credentials.

---

### 🔄 Workflow Connections

The workflow flows in this order:

Gmail Trigger → AI Agent

AI Agent ↔ Ollama Chat Model (for AI processing)

AI Agent ↔ Download File in Google Drive (for reference documents)

AI Agent Output → JavaScript Code Node (HTML formatting)

JavaScript Node Output → Reply to a Message (send email)

---

### ⚙️ Key Features

Fully automated email support.

Accurate, document-backed responses.

Professional tone and polite structure.

HTML email formatting for readability.

Can handle multiple document sources from Google Drive.

---

### 🌈 Summary

This n8n workflow is perfect for automating customer support with AI. It saves time, ensures accuracy, and maintains professionalism while handling multiple incoming emails.

Imagine an AI agent that reads, understands, researches, and replies to emails all while you focus on other tasks—that’s exactly what this workflow does! 🚀

--- 


### 📌 Notes

Ensure all OAuth2 credentials are properly set up for Gmail and Google Drive.

Update the Google Drive file IDs if document locations change.

AI responses are limited to the content in available documents—this ensures 100% factual correctness.

Works best for support teams looking to reduce manual email handling.

# Shree — AI Collections Assistant 🤖

An AI agent that assists loan/collection agents **during live customer calls**, instantly returning the correct RC (Reason Code) / Disposition, its definition, and suggested call narration — grounded in RBI-aligned collection guidelines.

Built to solve a real problem in NBFCs and Fintechs: fresher collection agents often get short training cycles and join live calls without fully internalizing disposition codes, compliance narration, and process rules. Shree acts as a real-time co-pilot so agents get accurate answers instantly instead of relying on incomplete training or memory.

---

## 💡 What it does

**Agent:** "Customer confirmed PTP for tomorrow"
**Shree:** Returns the matching RC code (`PTP_TOMORROW`), its definition, when to use it, and the suggested compliant narration to log — instantly.

It can answer questions across the full range of collection information: PTP variants, dispositions, RC code definitions, and process guidance — all in a live chat interface.

---

## 🏗️ Architecture

| Component | Role |
|---|---|
| **n8n** | Workflow orchestration — Chat Trigger receives the agent's message and routes it to the AI Agent node |
| **AI Agent node (n8n LangChain)** | Core reasoning layer that decides how to respond and which tools to call |
| **Qwen Cloud Chat Model** | LLM powering the agent's conversational responses |
| **Simple Memory** | Maintains conversation context across a session |
| **Pinecone (Vector DB)** | Stores the RC/Disposition knowledge base as embeddings for semantic retrieval |
| **Collection Knowledge RAG (Tool)** | Retrieval-Augmented Generation tool — the AI Agent queries this to pull accurate, grounded RC/Disposition data instead of hallucinating answers |

**Flow:** `Chat message received → AI Agent → (Chat Model + Memory + RAG Tool) → Response with correct RC/Disposition`

![Workflow Diagram](./assets/workflow-diagram.png)

---

## 🎥 Demo

A short demo showing a live query and Shree's response:

`./assets/shree_demo_clip.mp4`

---

## ⚙️ Setup

1. Import `workflow.json` into your n8n instance (Workflows → Import from File).
2. Connect your own credentials for:
   - Qwen Cloud Chat Model (or swap for any LLM node)
   - Pinecone (API key + index containing your RC/Disposition knowledge base)
3. Update the Chat Trigger node's **Title**, **Subtitle**, and **Initial Message** options to your branding.
4. Activate the workflow — n8n will generate a public webhook chat URL.

> ⚠️ The included `workflow.json` has all credentials and API keys stripped. You must add your own before running it.

---

## 🎯 Why I built this

In the AI era, most NBFCs and Fintechs still can't give fresher collection agents adequate training before they're on live calls. Shree is my attempt at closing that gap — giving every agent, regardless of tenure, instant access to accurate, compliant disposition knowledge during the call itself.

---

## 🧑‍💻 Author

**Sumit Ray**
Product Owner — Backlog & Delivery Ownership, Regulated Financial Services
[LinkedIn](https://www.linkedin.com/in/sumit-ray) · sumitprince121@gmail.com

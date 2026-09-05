# 🤖 N8N Workflow Automation — AI-Powered Notes & Q/A Generator

> **Automated content generation pipeline** built with [n8n](https://n8n.io/), leveraging OpenAI's GPT-4.1 models to generate structured study notes and multiple-choice quizzes from any given topic — in a single click.

---

## 📌 Project Overview

This repository contains production-ready **n8n workflow definitions** that demonstrate real-world **AI automation** capabilities. The flagship workflow accepts a topic via a web form and simultaneously generates:

1. **Comprehensive Study Notes** — 500-word detailed notes powered by GPT-4.1
2. **Multiple-Choice Q&A** — 5 MCQ-based questions for knowledge assessment, powered by GPT-4.1 Mini

Both outputs are generated in **parallel** and merged into a single unified response, showcasing efficient orchestration of concurrent AI tasks.

---

## 🏗️ Architecture

```
┌─────────────────┐
│   Web Form      │  ← User submits a topic
│  (Form Trigger) │
└────────┬────────┘
         │
    ┌────┴────┐
    │         │
    ▼         ▼
┌────────┐ ┌────────┐
│ Notes  │ │  Q/A   │  ← Parallel AI generation
│  Gen   │ │  Gen   │
│(GPT-4.1)│ │(GPT-4.1│
│        │ │  Mini) │
└───┬────┘ └───┬────┘
    │          │
    ▼          ▼
  ┌──────────────┐
  │    Merge     │  ← Combined output
  │   (Join)     │
  └──────────────┘
```

---

## 📂 Workflow Inventory

| Workflow | File | Description |
|----------|------|-------------|
| **Notes & Q/A Generator** | [`Notes and Q_A.json`](Notes%20and%20Q_A.json) | End-to-end pipeline: form input → parallel AI content generation → merged output |

---

## 🔧 Technical Highlights

### Parallel Execution
The workflow leverages n8n's **fan-out pattern** — a single form trigger fans out into two independent LLM chains that execute concurrently, then converge at a Merge node. This reduces total latency by running both AI calls simultaneously rather than sequentially.

### Multi-Model Strategy
- **GPT-4.1** — Used for the notes generator, where richer, more detailed output quality is critical
- **GPT-4.1 Mini** — Used for the Q/A generator, optimizing for cost efficiency on structured question generation

This demonstrates a practical **cost-performance tradeoff** approach to LLM orchestration — using the right model for each task.

### System Prompt Engineering
Each AI agent is configured with a dedicated system prompt to shape its persona:
- Notes Generator: `"You are a helpful notes generation assistant"`
- Q/A Generator: `"You are a helpful Q/A assistant"`

### Dynamic Prompt Templates
Prompts use n8n expression syntax (`{{ $json.Topic }}`) to dynamically inject user input, making the workflow fully reusable across any topic without code changes.

---

## 🚀 Getting Started

### Prerequisites

- [n8n](https://n8n.io/) (self-hosted or cloud)
- OpenAI API key with access to GPT-4.1 models

### Setup

1. **Clone this repository**
   ```bash
   git clone https://github.com/yourusername/n8n-workflows.git
   cd n8n-workflows
   ```

2. **Import the workflow into n8n**
   - Open your n8n instance
   - Navigate to **Workflows → Import from File**
   - Select `Notes and Q_A.json`

3. **Configure credentials**
   - Go to **Credentials** in n8n
   - Add your OpenAI API key under a new **OpenAI** credential
   - Link it to both OpenAI Chat Model nodes in the workflow

4. **Activate & Run**
   - Toggle the workflow to **Active**
   - Access the form trigger URL to submit a topic
   - Receive generated notes and Q/A in the merged output

---

## 🧰 Tech Stack

| Technology | Purpose |
|------------|---------|
| **n8n** | Low-code workflow automation platform |
| **OpenAI GPT-4.1** | Large language model for content generation |
| **OpenAI GPT-4.1 Mini** | Cost-optimized LLM for structured Q/A |
| **LangChain (n8n integration)** | LLM chain orchestration within n8n nodes |

---

## 💡 Key Concepts Demonstrated

- **Workflow Automation** — Designing event-driven automation pipelines
- **LLM Orchestration** — Managing multiple AI model calls within a single workflow
- **Parallel Processing** — Fan-out/fan-in patterns for concurrent task execution
- **Prompt Engineering** — Crafting system and user prompts for targeted AI output
- **Cost Optimization** — Strategic model selection to balance quality and cost
- **Low-Code AI Integration** — Connecting AI capabilities without extensive boilerplate code

---

## 📈 Future Enhancements

- [ ] Add additional output formats (PDF, Markdown, Google Docs)
- [ ] Integrate a vector database for topic-aware RAG (Retrieval-Augmented Generation)
- [ ] Add email/Slack notification upon generation completion
- [ ] Implement a feedback loop for iterative note refinement
- [ ] Add support for multi-language note generation

---

## 👤 Author

**Reuben Kuruvilla**

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

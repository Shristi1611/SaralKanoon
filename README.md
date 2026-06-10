# ⚖️ SaralKanoon (सरल कानून)

Simple Law for Every Indian

A free, multilingual AI legal assistant that helps ordinary Indian citizens understand complex legal documents in their own language -- Hindi, Tamil, Bengali, Telugu, or English.

---

## The Problem

- India has 22 official languages but most legal documents are in dense English
- Lawyers charge Rs 500-5,000 just to explain a document
- Millions of citizens: farmers, workers, tenants, have no access to legal clarity
- Government schemes, court orders, land records remain inaccessible to those who need them most

## The Solution

SaralKanoon lets anyone ask questions about Indian law in their own language and get simple, clear answers sourced directly from the actual legal documents.

---

## Features

- Multilingual: Ask in Hindi, Tamil, Bengali, Telugu, or English
- RAG-powered: Answers sourced from actual Indian legal documents
- Simple language: No legal jargon, explained like a knowledgeable friend
- Multiple laws: Consumer Protection, RTI, Motor Vehicles, Domestic Violence Act, MGNREGA and more
- Completely free: Built on free-tier tools, Rs 0 cost

---

## Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Workflow Automation | n8n (self-hosted) | Connects everything |
| LLM | Groq (Llama 3.3 70B) | Generates answers |
| Vector Database | Qdrant Cloud | Stores legal document chunks |
| Embeddings | Ollama + nomic-embed-text | Converts text to vectors |
| Frontend | Simple and basic HTML/CSS/JS | Chat interface |

---

## Architecture

```
User asks question (any Indian language)
        |
n8n Webhook receives the question
        |
AI Agent searches Qdrant for relevant legal sections
        |
Groq (Llama 3.3 70B) generates simple answer
        |
Answer returned in user's language
```

Ingestion Pipeline:

```
PDF (legal document)
        |
Extract text -> Chunk (1000 chars, 200 overlap)
        |
Generate embeddings (Ollama + nomic-embed-text)
        |
Store in Qdrant Cloud
```

---

## Legal Documents Included

- Consumer Protection Act 2019
- Right to Information Act 2005
- Motor Vehicles Act 1988
- Protection of Women from Domestic Violence Act 2005
- Mahatma Gandhi NREGA 2005
- Maternity Benefit Act 1961

---

## How to Run Locally

### Prerequisites
- Node.js installed
- Ollama installed (ollama.com)
- Free accounts on: Groq, Qdrant Cloud

### Step 1 -- Install and start n8n
```bash
npm install -g n8n@2.23.4
n8n start
```

### Step 2 -- Pull the embedding model
```bash
ollama pull nomic-embed-text
```

### Step 3 -- Set up credentials in n8n
Add these credentials in n8n (Settings -> Credentials):
- Groq API -- from console.groq.com
- Qdrant -- from cloud.qdrant.io
- Ollama -- URL: http://localhost:11434

### Step 4 -- Import workflows
In n8n -> Import from file -> import both JSON files:
- SaralKanoon - Ingestion.json
- SaralKanoon - Chat.json

### Step 5 -- Ingest documents
- Download legal PDFs from indiacode.nic.in
- Place in your n8n files folder
- Run the Ingestion workflow

### Step 6 -- Open the UI
Open saralkanoon.html in your browser and start asking questions!

---

## Example Questions

| Language | Question |
|---|---|
| English | What are my rights as a consumer? |
| Hindi | RTI ke tahat jaankari kaise maangein? |
| English | How do I file a complaint against a defective product? |
| Hindi | Gharelu hinsa ke khilaf mere kya adhikaar hain? |

---

## Planned Features

- PDF upload from UI (users can upload their own documents)
- More Indian languages (Marathi, Gujarati, Kannada)
- Voice input support
- Rebuild in Python with LangChain for easier deployment
- Cloud deployment
- Mobile app

---

## Contributing

Contributions welcome, especially:
- Adding more legal documents
- Improving multilingual support
- Better prompt engineering
- UI improvements

---

## License

Apache 2.0 -- see LICENSE file

---

## Built By

Shristi Sinha - Built from scratch as a learning project to explore AI agents, RAG systems, and multilingual NLP.

"Law should not be a privilege of only those who can afford lawyers."

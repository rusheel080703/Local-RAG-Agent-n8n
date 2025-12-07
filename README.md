# Local-Agentic-RAG-n8n

![n8n](https://img.shields.io/badge/n8n-FF6584?style=for-the-badge&logo=n8n&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## 📖 Overview

**Local-Agentic-RAG-n8n** is a fully autonomous, privacy-centric Retrieval-Augmented Generation (RAG) agent designed to run entirely on local infrastructure. 

This project demonstrates a powerful "No-Code" agentic workflow that effectively replaces cloud-based dependencies (such as OpenAI or Anthropic) with local, open-source alternatives. Orchestrated via **n8n** running in a Docker container, the system utilizes **Ollama** and the **Llama 3.2** model for on-device inference and vector embeddings. This architecture ensures that sensitive data never leaves the local network, creating a secure environment for document analysis and interaction.

## 🚀 Key Features

* **Zero Cost Operations:** Leverages existing local compute resources, eliminating subscription fees and token costs associated with external API providers.
* **Privacy First Architecture:** Designed for strict data sovereignty. No data egress occurs during ingestion, embedding, or inference, making it ideal for processing sensitive or proprietary documentation.
* **Custom Knowledge Base:** Supports the dynamic ingestion of unstructured data (PDF/Text). The system vectorizes uploaded documents locally, allowing for semantic queries over specific domains (e.g., *Complexity Theory* or *Network Analysis*).

## 🛠️ Tech Stack

* **Orchestration:** [n8n](https://n8n.io/) (Workflow Automation)
* **Containerization:** Docker
* **Local Inference Engine:** Ollama
* **LLM & Embeddings:** Llama 3.2
* **Vector Store:** Qdrant / In-Memory Vector Store

## 📂 Repository Structure

```text
Local-Agentic-RAG-n8n/
├── sample_data/
│   ├── network_flow.pdf               # Sample academic paper on Network Flow
│   └── computational_intractability.pdf # Sample material on Complexity Theory
├── screenshots/
│   ├── workflow_graph.png             # Architecture view of the n8n agent
│   └── chat_demo.png                  # Screenshot of the agent in action
├── workflow.json                      # The exportable n8n workflow configuration
└── README.md                          # Project documentation

```

## 📸 Architecture & Workflow

### Agent Architecture

*A visual representation of the n8n agentic workflow, handling document ingestion, vectorization, and recursive retrieval.*

-----

## ⚙️ Installation & Setup Guide

### Prerequisites

  * **Docker Desktop** installed and running.
  * **Ollama** installed locally.

### Step 1: Configuration & Model Setup

Ensure Ollama is running and pull the required model.

```bash
# Pull the Llama 3.2 model
ollama pull llama3.2

# Ensure Ollama is listening on all interfaces (required for Docker connectivity)
# On Linux/macOS:
OLLAMA_HOST=0.0.0.0 ollama serve
```

### Step 2: Launch n8n

Run the n8n orchestrator inside a Docker container. Use the following command to map the necessary ports and volumes:

```bash
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

### Step 3: Workflow Configuration

1.  Open your browser and navigate to `http://localhost:5678`.
2.  Set up the initial n8n admin account.
3.  Go to **Workflows** \> **Import** and select the `workflow.json` file provided in this repository.
4.  **Critical Step:** In the workflow nodes connecting to Ollama, ensure the **Base URL** is set to allow the Docker container to communicate with the host machine:
      * **Base URL:** `http://host.docker.internal:11434`

## 💡 Usage

Once the workflow is active:

1.  **Ingest Data:** Use the chat interface or the upload node to ingest one of the provided sample documents found in `sample_data/`:
      * `network_flow.pdf`
      * `computational_intractability.pdf`
2.  **Query the Agent:** The system will generate vector embeddings for the file. You can now chat with your data.
3.  **Example Prompts:**
      * *"Explain the Max-Flow Min-Cut theorem based on the uploaded document."*
      * *"Summarize the key constraints regarding NP-Hardness mentioned in the text."*

### Agent in Action

-----

## 👨‍💻 Author

This project was developed as part of a Computer Science portfolio exploring local AI sovereignty and agentic workflows.

```
```

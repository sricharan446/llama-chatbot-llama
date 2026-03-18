# Project 1 — Chatbot with Llama

This project is part of the Manning liveProject series:
[Open Source LLMs on Your Own Computer](https://www.manning.com/liveprojectseries/open-source-llms-on-your-own-computer)

A local AI chatbot built using the Llama large language model. The chatbot runs entirely on your own machine with no cloud dependency, using WasmEdge and LlamaEdge for efficient inference.

---

## Project Series

| Project | Title | Repo |
|---------|-------|------|
| Project 1 | Chatbot with Llama | You are here |
| Project 2 | Add Knowledge to the Chatbot | [llama-rag-knowledge](https://github.com/sricharan446/llama-rag-knowledge) |
| Project 3 | Fine-Tune the Llama Model | [llm_project_finetune](https://github.com/sricharan446/llm_project_finetune) |

---

## About

In this project, a chatbot is built that can answer questions and engage in follow-up conversations using the open source Llama LLM from Meta AI. The model runs with very low resources and is equipped with an intuitive web-based user interface.

---

## Project Structure

```
project1_chatbot_llama/
├── chatbot-ui/              # Web frontend for the chatbot
├── ngrok-v3-stable-linux-amd64.zip  # Ngrok for public tunneling
├── nohup.out                # Background server process log
└── README.md
```

---

## Prerequisites

- Linux (or WSL on Windows)
- Docker
- Basic knowledge of command line tools
- Basic knowledge of LLMs

---

## Workflow

### Step 1 — Start the Docker Container

```bash
docker start b7910aa1cc64
docker exec -it b7910aa1cc64 bash
```

### Step 2 — Start the Llama API Server

Inside the container, start the LlamaEdge API server:

```bash
cd /llm_project/llm_project
nohup ./llama-api-server.wasm &
```

The server runs on `http://localhost:8080`.

### Step 3 — Set Up Ngrok (for public access)

```bash
unzip ngrok-v3-stable-linux-amd64.zip
./ngrok http 8080
```

Copy the public URL provided by ngrok to access the chatbot from anywhere.

### Step 4 — Open the Chatbot UI

Open `chatbot-ui/index.html` in your browser, or serve it locally:

```bash
cd chatbot-ui
python3 -m http.server 3000
```

Then visit `http://localhost:3000` in your browser.

### Step 5 — Test the Chatbot

Type any chemistry question in the chat interface. The chatbot will respond using the Llama model running locally.

Example:

```
User: What is molarity?
Bot: Molarity is the number of moles of solute per litre of solution...
```

---

## API Usage

You can also query the chatbot directly via the API:

```bash
curl http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [{"role": "user", "content": "Explain photosynthesis"}]
  }'
```

---

## Tech Stack

- **Model:** Llama (Meta AI)
- **Runtime:** WasmEdge / LlamaEdge
- **Frontend:** HTML, CSS, JavaScript
- **Tunneling:** Ngrok
- **Platform:** Docker on Windows (WSL)

---

## References

- [Manning liveProject Series](https://www.manning.com/liveprojectseries/open-source-llms-on-your-own-computer)
- [WasmEdge](https://wasmedge.org)
- [LlamaEdge](https://github.com/LlamaEdge/LlamaEdge)
- [Meta Llama](https://llama.meta.com)

---

## Author

**Sri Charan**
- GitHub: [@sricharan446](https://github.com/sricharan446)
- Hugging Face: [@SriCharan446](https://huggingface.co/SriCharan446)

# AI Co‑Founder Bot 🤖

A self‑contained, offline "Jarvis‑style" AI assistant with voice-first interaction.

## Features ✨

- **Voice-first chat** – Whisper.cpp → FastAPI → Llama.cpp → Coqui-TTS
- **JWT authentication** – Per-user isolated memory and privacy
- **Private vector store** – FAISS + MiniLM-L6-v2 embeddings for RAG
- **Idea rating engine** – JSON output (novelty/feasibility/impact)
- **To-do & reminder system** – APScheduler + OS notifications
- **Pitch deck generator** – LLM-based slide outline helper
- **Sentiment-aware tone** – Distilbert sentiment detection
- **Rate limiting** – Protects GPU from flood attacks
- **Secure SQLite** – Optional SQLCipher encryption
- **Minimal dependencies** – All free tools, cost ≈ ₹800-₹1500

## Quick Start 🚀

### 1. Install System Dependencies

```bash
sudo apt update
sudo apt install -y git ffmpeg build-essential cmake python3-venv \
    libsndfile1 libasound2-dev
```

### 2. Create Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
```

### 3. Install Python Dependencies

```bash
pip install fastapi[all] uvicorn python-jose passlib sqlalchemy aiosqlite \
    sentence-transformers faiss-cpu apscheduler plyer tqdm llama-cpp-python \
    coqui-tts numpy sounddevice slowapi transformers torch
```

### 4. Download LLM Model

```bash
pip install huggingface_hub
huggingface-cli login
mkdir -p models && cd models
hf download mistralai/Mistral-7B-Instruct-v0.2 --local-dir .
cd ..
```

### 5. Run the Assistant

**API Server:**
```bash
python ai_co_founder.py
# Runs on http://127.0.0.1:8000
```

**Voice Loop (requires server running):**
```bash
python ai_co_founder.py --voice
```

## API Endpoints 📡

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/register` | Register new user |
| POST | `/login` | User login |
| POST | `/chat` | Send message to AI |
| POST | `/task` | Create reminder/task |
| POST | `/pitch` | Generate pitch deck outline |
| GET | `/memory` | Retrieve past context |
| DELETE | `/me` | Delete all user data |
| GET | `/ping` | Health check |

## Configuration ⚙️

- `JWT_SECRET` – Set via environment variable for token signing
- `LLM_MODEL_PATH` – Path to GGML model file
- `WHISPER_EXE` – Path to compiled whisper.cpp binary
- `APP_RATE_LIMIT` – Rate limit (default: 30/minute)

## License

MIT

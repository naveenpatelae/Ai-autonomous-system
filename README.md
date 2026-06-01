# 🌌 Sovereign Edge-to-Cloud AI Orchestration Engine

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![FastAPI](https://img.shields.io/badge/FastAPI-Edge_Server-009688?style=for-the-badge&logo=fastapi)
![Security](https://img.shields.io/badge/Security-AST_Execution_Shield-red?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-macOS-lightgrey?style=for-the-badge&logo=apple)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

A deterministic, multi-agent AI orchestration system that turns a Mac into a sovereign AI workstation. It intelligently routes commands between a local edge node and a cloud-hosted 70B LLM — using a strict AST execution shield to ensure no LLM output ever reaches the OS unvalidated.

---

## Architecture

![Nyxi Architecture](./docs/architecture.png)

The system is split into four clean layers:

- **engine/core** — The domain-agnostic brain. Handles LLM routing, parallel inference (Maker/Checker), speculative decoding, intent extraction, and emotion-aware context. Contains no macOS-specific code.
- **engine/security** — A five-layer execution cage. Every LLM response passes through regex scanning, AST validation, and namespace-isolated `exec()` before touching the OS.
- **engine/memory\_learning** — Three-tier memory (session dict → SQLite → FAISS) plus a nocturnal distillation flywheel that generates DPO preference pairs for on-device fine-tuning.
- **plugins/macos** — The reference implementation. Translates core engine intent into AppleScript, Accessibility API calls, and Zsh scripts. Swappable for any other execution backend.

---

## Quick Start

**Prerequisites:** macOS 13+, Python 3.10+, Kaggle account, Firebase project, Ngrok account, Groq API key.

```bash
git clone https://github.com/naveenpatelae/Autonomous-AI-System.git
cd Autonomous-AI-System

pip install fastapi uvicorn groq firebase-admin pyngrok \
            nest_asyncio httpx requests numpy pyttsx3 \
            SpeechRecognition llama-cpp-python

# Optional accelerators
pip install faiss-cpu mlx mlx-lm mediapipe
```

**Configure secrets:**

```bash
export GROQ_API_KEY="gsk_..."
export NGROK_TOKEN="your_ngrok_authtoken"
export ELEVENLABS_API_KEY="your_key"   # optional
# Place firebase_key.json in the project root
```

**Start the Cloud Brain:** Open `Autonomous-AI-System.ipynb` in Kaggle, add the secrets above via the Kaggle Secrets UI, and run all cells. You should see:

```
🚀 NYXI CLOUD ONLINE AT: https://xxxx.ngrok-free.dev
```

**Start the Edge Node:**

```bash
python nyxi_body.py
```

The particle avatar opens in your browser. Type commands in the text box — voice input is in development.

---

## Security Model

LLM output never reaches the shell directly. Every command passes through five layers:

| Layer | Module | What it does |
|---|---|---|
| 1 | `security_shield.py` | Regex scan — blocks `rm -rf`, `eval()`, `shell=True`, and 7 other patterns |
| 2 | `agent_shield_bridge.py` | Cross-agent policy enforcement, prevents privilege escalation |
| 3 | AST compile | Validates syntax before any execution |
| 4 | Namespace isolation | `exec()` runs in `{"__builtins__": {}}` only |
| 5 | `DeadMansSwitch` | Severs Wi-Fi on critical breach (`networksetup -setairportpower en0 off`) |

---

## Project Status (v1)

**Working end-to-end:**
- ✅ Text prompt → Cloud Brain (70B LLM) → macOS action execution
- ✅ 30+ built-in OS blueprints (apps, system info, audio, clipboard)
- ✅ SecureShield AST execution gate
- ✅ Local RAG index (TF-IDF + FAISS)
- ✅ Air-gap survival mode with offline command queue
- ✅ Firebase Firestore state sync

**In active development:**
- 🔧 Voice input pipeline (wake word → acoustic gate → STT → intent)
- 🔧 On-device DPO fine-tuning flywheel (MLX + distillation factory)
- 🔧 Gesture recognition (webcam-based)
- 🔧 S-LoRA multi-adapter routing

---

## License

MIT — see [LICENSE](LICENSE) for details.

> *"The machine should serve the mind, not the other way around."*
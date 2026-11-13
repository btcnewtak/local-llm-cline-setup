# local-llm-cline-setup
Fix “Cannot convert argument to a ByteString” error in Cline/VS Code when using Ollama locally with fast models (e.g. Qwen 3.5 / 2.5)
# local-llm-cline-setup
Fix “Cannot convert argument to a ByteString” error in Cline/VS Code when using Ollama locally with fast models (e.g. Qwen 3.5 / 2.5)

# 🚀 Fixing Cline & Ollama ByteString Error (Local AI Coding Setup)

A step-by-step guide to resolve the fatal **`TypeError: Cannot convert argument to a ByteString because the character at index X has a value of ... which is greater than 255`** error when using **Cline** (VS Code) with local **Ollama** models.

---

## 🎯 Problem Overview
When connecting the VS Code extension **Cline** directly to Ollama via its native API endpoints, users frequently encounter a ByteString encoding crash. This typically happens when non-ASCII / Unicode characters (like Persian/Arabic or special symbols) are processed in headers or requests by Node.js/Fetch environments.

---

## ⚡ The Solution: OpenAI-Compatible Routing
Instead of relying on the direct Ollama provider option inside Cline, use Ollama's built-in `/v1` (OpenAI-compatible) endpoint. This completely bypasses the encoding mismatch while preserving full tool-calling capabilities (running commands, creating files, and editing code).

### 🛠️ Configuration in Cline (VS Code)

1. Open **Cline** settings in VS Code.
2. Under **API Provider**, select:
   - **`OpenAI Compatible`**
3. Configure the following fields:
   - **Base URL:** `http://127.0.0.1:11434/v1`
   - **API Key:** `ollama` (or any dummy text like `1234`)
   - **Model ID:** `qwen3.5:4b` *(or `qwen2.5-coder:7b`)*
4. Save and restart Cline.

---

## 💻 Recommended Hardware & Model Setup
Tested and verified on mid-range GPUs (e.g., **NVIDIA GTX 1660 Ti 6GB VRAM**):

| Model | Size | Status / Performance |
| :--- | :--- | :--- |
| **`qwen3.5:4b`** | ~3.4 GB | ⚡ Ultra-fast, low VRAM usage, reliable tool-calling |
| **`qwen2.5-coder:7b`** | ~4.7 GB | 🎯 Highly capable for multi-file refactoring |

---

## 🧪 Verification Test
To confirm your agent can execute tools and edit files seamlessly, run this prompt inside Cline:
```
Create a test file named `test_agent.py` in the root workspace that defines an `add(a, b)` function, runs sample assertions, and execute it using Python.
```

If the agent successfully creates and executes the script, your environment is 100% operational!

---
## 💻  🇮🇷 راهنمای فارسی / Persian Guide
برای حل خطای مشهور و آزاردهنده‌ی ByteString هنگام اتصال افزونه Cline در (VS Code) به Ollama لوکال:

🛠️ نحوه تنظیم در Cline:
در تنظیمات افزونه Cline، بخش API Provider را روی حالت OpenAI Compatible قرار دهید.
آدرس Base URL را برابر با این مقدار قرار دهید:
---
   http://127.0.0.1:11434/v1
---
   
در کادر API Key یک مقدار دلخواه (مثل ollama) وارد کنید.
در بخش Model ID نام مدل خود (مثلاً qwen3.5:4b) را بنویسید.
با این روش، ناسازگاری انکودینگ کاراکترها در Node.js دور زده می‌شود و تمام ابزارهای ساخت، ویرایش و اجرای کد بدون خطای ByteString کار خواهند کرد.

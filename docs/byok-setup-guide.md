# Lumi BYOK (Bring Your Own Key) Configuration Guide

Lumi allows you to connect your own LLM and ASR credentials directly inside the browser extension. When a BYOK provider is explicitly selected (**BYOK Override**), requests are sent from your browser to the provider and consume **0 Lumi platform Tokens**.

Full interactive documentation: **[https://islumi.com/zh-CN/docs#providers](https://islumi.com/zh-CN/docs#providers)** | **[https://islumi.com/en/docs#providers](https://islumi.com/en/docs#providers)**

---

## Supported Providers

| Provider | Type | Supported Features | API Key Portal |
| :--- | :--- | :--- | :--- |
| **DeepSeek** | Text / LLM | Subtitle translation, Subtitle Refinement, Video Summary, Video Article, Video Q&A, Web Page Translation | https://platform.deepseek.com/api_keys |
| **OpenAI / Compatible API** | Text / LLM | Full text, summary, Q&A, and subtitle workflows | https://platform.openai.com/api-keys |
| **Anthropic Claude** | Text / LLM | Full text, summary, Q&A, and subtitle workflows | https://console.anthropic.com/settings/keys |
| **Aliyun Paraformer (DashScope)** | Speech-to-Text (ASR) | Uncaptioned video transcription on Bilibili & YouTube | https://bailian.console.aliyun.com/ |
| **Doubao Seed Flash ASR** | Speech-to-Text (ASR) | Uncaptioned video transcription on Bilibili & YouTube | https://console.volcengine.com/speech/app |

---

## 3-Step Setup

1. Open **Lumi Settings -> Models & API Keys** (or **Subtitles & Translation** for ASR).
2. Enter your API Key (and optional custom Base URL / model name for OpenAI-compatible or Anthropic-compatible endpoints).
3. Click **Test connection** to verify credentials, then select that provider as your active translation, summary, or transcription service.

### Key Privacy & Shared Artifact Rules
- Your API keys remain in local extension storage (`chrome.storage.local`) and are **never** uploaded during cross-device preference sync.
- Text BYOK outputs remain private to your browser and do not enter the Shared AI Artifact pool.
- Complete BYOK ASR transcripts that pass coverage and **Stable Audio Identity** verification can contribute to the **Shared ASR Transcript** pool (without exposing your key or raw audio).

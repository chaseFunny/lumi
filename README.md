# Lumi — AI Video Learning Companion for YouTube & Bilibili

<p align="left">
  <a href="https://islumi.com/en"><img src="https://img.shields.io/badge/Website-islumi.com-5A4BC6?style=flat-square" alt="Official Website"></a>
  <a href="https://chromewebstore.google.com/detail/ackkdapdaaemdljhmgpilbbbojmkmdad"><img src="https://img.shields.io/badge/Chrome_Web_Store-Install-4A3CA8?style=flat-square&logo=googlechrome&logoColor=white" alt="Chrome Web Store"></a>
  <a href="https://microsoftedge.microsoft.com/addons/detail/lumi%EF%BC%9Ab%E7%AB%99-youtube-%E5%8F%8C%E8%AF%AD-ai-%E5%AD%97/mmdaplnonheeighjncdffkedmbmknbbn"><img src="https://img.shields.io/badge/Edge_Add--ons-Install-4A3CA8?style=flat-square&logo=microsoftedge&logoColor=white" alt="Edge Add-ons"></a>
  <a href="./README.zh-CN.md"><img src="https://img.shields.io/badge/文档-简体中文-F4F3FD?style=flat-square" alt="简体中文文档"></a>
</p>

**[Lumi](https://islumi.com/en)** is a browser extension for Chrome and Microsoft Edge that turns **YouTube** and **Bilibili** videos into an interactive, searchable study workspace: playback-first bilingual subtitle refinement, AI speech-to-text (ASR) for uncaptioned videos, timestamped chapter summaries, structured reading guides, grounded cross-video Q&A, and side-by-side web page translation.

> **中文说明**：请查看 [**简体中文文档 (README.zh-CN.md)**](./README.zh-CN.md) 或访问 **[Lumi 中文官网 (islumi.com/zh-CN)](https://islumi.com/zh-CN)**。

---

## Why Lumi?

Watching technical talks, university lectures, and foreign-language interviews on YouTube and Bilibili usually breaks down at five points:

1. **Fragmented auto-captions**: YouTube automatic captions split a single thought into 2–3 second slices. Translating each slice line by line scrambles word order and pronoun references.
2. **Uncaptioned Bilibili videos**: Many Bilibili UGC uploads, courses, and interviews have no soft subtitle track at all.
3. **Full-video processing latency**: Waiting for an entire 1-hour lecture to finish resegmenting before you can jump to minute 35 breaks your study flow.
4. **Linear scrubbing friction**: Finding the exact 30-second explanation of an architecture diagram means dragging the progress bar back and forth.
5. **Subscription lock-in for developers**: Engineers who already hold **DeepSeek**, **OpenAI**, **Anthropic Claude**, **Aliyun Paraformer**, or **Doubao ASR** API keys want a clean BYOK path without platform markups.

---

## Core Capabilities & Technical Architecture

| Capability | How Lumi Works | Live Guide & Specifications |
| :--- | :--- | :--- |
| **YouTube Bilingual Subtitle Refinement** | Combines context-aware resegmentation, translation, and readability post-processing. Scheduled via a **Playback-first Refinement Window** around your current playhead so seeking mid-video prioritizes the active passage immediately. | [YouTube Subtitle Refinement](https://islumi.com/en/features/youtube-subtitle-refinement) · [Architecture Doc](./docs/subtitle-refinement-architecture.md) |
| **Bilibili Uncaptioned Video ASR** | Supports Bilibili UGC (`bvid + cid`) and PGC courses/series (`epId + cid`). Prioritizes an opening 5-minute **Preview Segment** for immediate viewing while a durable background queue transcribes subsequent segments (up to 1 hour each). | [Bilibili AI Subtitles & ASR](https://islumi.com/en/features/bilibili-ai-subtitles) |
| **Timestamped Video Summary & Grounded Q&A** | Generates navigable **Timeline Chapters**, continuous **Video Articles**, and multi-video Q&A backed by frozen **Knowledge Scope Snapshots** and permission-bound **Evidence Handles** with clickable timestamps. | [Video Summary & Timestamped Q&A](https://islumi.com/en/features/video-summary-and-chat) |
| **Bilingual Web Page Translation** | Translates technical articles, documentation, and forums paragraph by paragraph in bilingual or translation-only mode while preserving inline `<code>`, links, and layout. | [Bilingual Web Page Translation](https://islumi.com/en/features/bilingual-page-translation) |

---

## Bring Your Own Key (BYOK) & Quota Model

Lumi supports both zero-configuration **Lumi AI** and local **BYOK Override** (your API keys stay in local browser storage and consume **0 Lumi Tokens**):

| Mode / Provider | Supported Workflows | Lumi Platform Quota Cost | Setup Reference |
| :--- | :--- | :--- | :--- |
| **Lumi AI (Free Plan)** | Subtitles, refinement, summaries, Q&A | **200,000 Tokens** one-time welcome grant | [Pricing & Quota](https://islumi.com/en/pricing) |
| **Lumi AI (Pro Plan)** | All AI workflows + Lumi AI web translation + cross-device sync + Shared ASR reuse | **10,000,000 Tokens / month** | [Pricing & Quota](https://islumi.com/en/pricing) |
| **DeepSeek (BYOK)** | Subtitle translation, Subtitle Refinement, Video Summary, Video Q&A, Web Translation | **0 Lumi Tokens** (billed by DeepSeek) | [DeepSeek Setup](https://islumi.com/en/docs#deepseek) · [BYOK Guide](./docs/byok-setup-guide.md) |
| **OpenAI / Compatible API (BYOK)** | Full text & translation workflows | **0 Lumi Tokens** | [OpenAI Setup](https://islumi.com/en/docs#openai) |
| **Anthropic Claude (BYOK)** | Full text & translation workflows | **0 Lumi Tokens** | [Claude Setup](https://islumi.com/en/docs#anthropic) |
| **Aliyun Paraformer / DashScope ASR (BYOK)** | Uncaptioned video speech-to-text | **0 Lumi Quota** (can contribute to Shared ASR Transcript pool) | [Paraformer Setup](https://islumi.com/en/docs#paraformer) |
| **Doubao Seed Flash ASR (BYOK)** | Uncaptioned video speech-to-text | **0 Lumi Quota** (can contribute to Shared ASR Transcript pool) | [Doubao ASR Setup](https://islumi.com/en/docs#doubao) |

---

## Paired Subtitle Resegmentation Sample

From [`samples/youtube-refinement.json`](./samples/youtube-refinement.json) (recorded on Andrej Karpathy's *[1hr Talk] Intro to Large Language Models*, `0–180 s` window, `boundary-v1` mode):

| Before (4 Fragmented Auto-Caption Cues) | After (3 Semantically Resegmented Cues) |
| :--- | :--- |
| `0.16–4.24s` hi everyone so recently I gave a<br>`2.28–6.40s` 30-minute talk on large language models<br>`4.24–8.48s` just kind of like an intro talk um<br>`6.40–10.08s` unfortunately that talk was not recorded | `0.16–4.08s` hi everyone so recently I gave a 30-minute talk on large language models<br>`4.08–6.16s` just kind of like an intro talk<br>`6.16–8.20s` um unfortunately that talk was not recorded |

---

## Curated Study Guides & Comparisons

- **Curated Public Study Library**: [islumi.com/en/explore](https://islumi.com/en/explore)
  - [Andrej Karpathy — Intro to Large Language Models: Bilingual Subtitles & Chapter Guide](https://islumi.com/en/explore/karpathy-intro-to-llms)
  - [Bilibili Study Case: Steve Jobs on Failure & the Courage to Begin (BV1H2Tu6EEzH)](https://islumi.com/en/explore/bilibili-courage-to-try)
- **Video Learning Extensions Compared (Lumi vs. Immersive Translate, Monica & Glarity)**: [islumi.com/en/compare/video-learning-extensions](https://islumi.com/en/compare/video-learning-extensions)
- **Installation**:
  - [Chrome Web Store](https://chromewebstore.google.com/detail/ackkdapdaaemdljhmgpilbbbojmkmdad)
  - [Microsoft Edge Add-ons](https://microsoftedge.microsoft.com/addons/detail/lumi%EF%BC%9Ab%E7%AB%99-youtube-%E5%8F%8C%E8%AF%AD-ai-%E5%AD%97/mmdaplnonheeighjncdffkedmbmknbbn)
  - [Edge Manual ZIP Installation Guide](https://islumi.com/en/edge/manual-install)
- **Machine-Readable LLM Specification**: [islumi.com/llms.txt](https://islumi.com/llms.txt) · [islumi.com/llms-full.txt](https://islumi.com/llms-full.txt)

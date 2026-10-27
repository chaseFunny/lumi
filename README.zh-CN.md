# Lumi — 看懂每一支视频的 B站 & YouTube AI 学习伴侣

<p align="left">
  <a href="https://islumi.com/zh-CN"><img src="https://img.shields.io/badge/官方网站-islumi.com-5A4BC6?style=flat-square" alt="官方网站"></a>
  <a href="https://chromewebstore.google.com/detail/ackkdapdaaemdljhmgpilbbbojmkmdad"><img src="https://img.shields.io/badge/Chrome_应用商店-免费安装-4A3CA8?style=flat-square&logo=googlechrome&logoColor=white" alt="Chrome 应用商店"></a>
  <a href="https://microsoftedge.microsoft.com/addons/detail/lumi%EF%BC%9Ab%E7%AB%99-youtube-%E5%8F%8C%E8%AF%AD-ai-%E5%AD%97/mmdaplnonheeighjncdffkedmbmknbbn"><img src="https://img.shields.io/badge/Edge_加载项-免费安装-4A3CA8?style=flat-square&logo=microsoftedge&logoColor=white" alt="Edge 加载项"></a>
  <a href="./README.md"><img src="https://img.shields.io/badge/Docs-English-F4F3FD?style=flat-square" alt="English Docs"></a>
</p>

**[Lumi](https://islumi.com/zh-CN)** 是专为 **Bilibili（B站）** 与 **YouTube** 打造的 Chrome / Edge 视频深度学习浏览器扩展：提供播放点优先的双语字幕智能断句精修、无字幕“生肉”视频 AI 语音转写（ASR）、带时间戳的章节总结与结构化阅读稿、基于原文证据链的跨视频知识库问答，以及技术网页双语对照翻译。

---

## 核心功能与技术亮点

| 核心模块 | 解决痛点与工程机制 | 线上详情与实测样本 |
| :--- | :--- | :--- |
| **YouTube 双语字幕智能断句精修** | 解决自动字幕“一句话碎成四五段、逐行机翻语序颠倒”的问题。采用 **播放点优先精修窗口（Playback-first Refinement Window）**，拖动进度条到哪就优先处理哪一段，无需等待全片翻译完成。 | [YouTube 双语字幕精修指南](https://islumi.com/zh-CN/features/youtube-subtitle-refinement) · [架构说明](./docs/subtitle-refinement-architecture.md) |
| **B站无字幕视频 AI 语音转写 (ASR)** | 原生适配 B站 UGC（`bvid + cid`）与番剧课程（`epId + cid`）。**开头最多 5 分钟预览段（Preview Segment）优先出字幕**，后续分段由持久化队列后台处理；支持共享 ASR 字幕池（Pro 复用 0 额度消耗）与 YouTube 原版字幕自动匹配同步。 | [B站无字幕 AI 语音转写与双语字幕](https://islumi.com/zh-CN/features/bilibili-ai-subtitles) |
| **AI 视频总结、阅读稿与时间戳问答** | 自动提炼时间轴章节大纲与可精读的结构化文章；跨视频问答采用冻结的 **知识范围快照（Knowledge Scope Snapshot）** 与时间戳证据句柄，点击出处直接跳回原视频对应秒数。 | [AI 视频总结与时间戳问答知识库](https://islumi.com/zh-CN/features/video-summary-and-chat) |
| **AI 网页双语对照翻译** | 阅读海外技术博客、GitHub 文档与论文网页时，按段落呈现双语对照或仅译文模式，保留行内代码 `<code>`、链接与排版结构。 | [AI 网页双语对照翻译](https://islumi.com/zh-CN/features/bilingual-page-translation) |

---

## 零配置 Lumi AI 与自带密钥（BYOK）支持表

Lumi 同时支持开箱即用的托管服务与本地直连的 BYOK 模式（API Key 仅保存在浏览器本地，**走 BYOK 路径时消耗 Lumi 平台额度为 0**）：

| 服务商 / 模式 | 支持能力范围 | Lumi 平台额度消耗 | 配置说明 |
| :--- | :--- | :--- | :--- |
| **Lumi AI（免费注册）** | 双语字幕、智能断句、视频总结、问答 | 一次性赠送 **200,000 Token** + 7 天 Lite Pro | [定价与额度说明](https://islumi.com/zh-CN/pricing) |
| **Lumi AI（Pro 会员）** | 全套 AI 能力 + 网页 AI 精翻 + 跨端云同步 + 共享 ASR 免额度复用 | 每自然月 **10,000,000 Token** | [定价与额度说明](https://islumi.com/zh-CN/pricing) |
| **DeepSeek（BYOK）** | 字幕翻译、字幕智能精修、视频总结、视频问答、网页翻译 | **0 Token**（厂商独立计费） | [DeepSeek 配置指南](https://islumi.com/zh-CN/docs#deepseek) · [详细步骤](./docs/byok-setup-guide.md) |
| **OpenAI 及兼容接口（BYOK）** | 全套文本生成与双语翻译能力 | **0 Token** | [OpenAI 配置指南](https://islumi.com/zh-CN/docs#openai) |
| **Anthropic Claude（BYOK）** | 全套文本生成与双语翻译能力 | **0 Token** | [Claude 配置指南](https://islumi.com/zh-CN/docs#anthropic) |
| **阿里云百炼 Paraformer / DashScope ASR** | 无字幕视频语音转写 | **0 平台额度**（完整转写可贡献共享字幕池） | [Paraformer 配置指南](https://islumi.com/zh-CN/docs#paraformer) |
| **豆包 Seed Flash ASR** | 无字幕视频语音转写 | **0 平台额度**（完整转写可贡献共享字幕池） | [豆包 ASR 配置指南](https://islumi.com/zh-CN/docs#doubao) |

---

## 公开课双语精读案例与工具对比

- **精选公开课双语精读库**：[https://islumi.com/zh-CN/explore](https://islumi.com/zh-CN/explore)
  - [Andrej Karpathy《大语言模型入门 1 小时讲座》双语字幕与章节精读](https://islumi.com/zh-CN/explore/karpathy-intro-to-llms)
  - [B站英文访谈《大胆尝试，让自己有失败的勇气和能力》双语字幕与精读笔记](https://islumi.com/zh-CN/explore/bilibili-courage-to-try)
- **视频学习插件客观对比（Lumi vs 沉浸式翻译 vs Monica vs Glarity）**：[https://islumi.com/zh-CN/compare/video-learning-extensions](https://islumi.com/zh-CN/compare/video-learning-extensions)
- **下载与安装**：
  - [官网下载页](https://islumi.com/zh-CN/download)
  - [Edge 插件官方 ZIP 离线包手动安装指南](https://islumi.com/zh-CN/edge/manual-install)
  - [支持与问题排查中心](https://islumi.com/zh-CN/support)

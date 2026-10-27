# Subtitle Refinement & Playback-First Scheduling Architecture

Live interactive reference: **[https://islumi.com/en/features/youtube-subtitle-refinement](https://islumi.com/en/features/youtube-subtitle-refinement)** | **[https://islumi.com/zh-CN/features/youtube-subtitle-refinement](https://islumi.com/zh-CN/features/youtube-subtitle-refinement)**

---

## 1. Deterministic Subtitle Chunks vs. Playback-First Refinement Windows

Lumi separates ordinary subtitle translation from context-aware **Subtitle Refinement**:

1. **Deterministic Subtitle Chunk (Ordinary Translation)**:
   - Splits an ordered subtitle track deterministically from the beginning of the video: at most **10 cues** and **2,000 source characters** per chunk.
   - Each source cue maps 1-to-1 to a translated cue.
   - Playhead position does not alter chunk boundaries, enabling deterministic cross-user caching via **Shared AI Artifacts**.
2. **Playback-First Refinement Window (Smart Segmentation & Translation)**:
   - Auto-generated captions on YouTube frequently split a single clause across 3–5 short cues.
   - **Subtitle Refinement** inspects neighboring cues to resegment them into complete thoughts before translating and applying **Segmentation Post-processing** for on-video readability.
   - Rather than processing a 1-hour lecture sequentially from `00:00`, the **Playback-first Refinement Window** prioritizes the time window surrounding the viewer's current playhead. When you seek to a new section, Lumi schedules that window first.

---

## 2. Progressive Managed ASR for Uncaptioned Videos

Details: **[https://islumi.com/en/features/bilibili-ai-subtitles](https://islumi.com/en/features/bilibili-ai-subtitles)**

- **Stable Audio Identity**: Identified by platform parameters (e.g., Bilibili `platform + bvid + cid + audioStreamId` or PGC `epId + cid`) rather than ephemeral signed media URLs.
- **Preview Segment**: The first **ASR Segment** covers up to the opening **5 minutes** of a video so bilingual subtitles appear quickly while a durable queue processes the remaining 1-hour segments sequentially.
- **Shared ASR Transcript**: Once all segments complete and pass coverage verification, Pro members watching the same audio identity can reuse the transcript immediately without deducting ASR duration quota.

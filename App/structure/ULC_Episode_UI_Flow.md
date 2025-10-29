# ULC Episode — In‑App UI Flow & Wireframes

This document shows how a **UkrainianLessons.com** (ULC) podcast episode appears inside **[YourApp]** as an interactive, culture-first lesson.

> **Preview diagrams:** Use VS Code with the **Markdown Preview Mermaid Support** extension.  
> **Export:** `npm i -g @mermaid-js/mermaid-cli` → `mmdc -i ULC_Episode_UI_Flow.md -o ULC_Episode_UI_Flow.svg`.

---

## 1) User Flow (Mermaid)

```mermaid
flowchart TD
  A[Home] --> B[ULC Channel Tile<br/>“Powered by UkrainianLessons.com”]
  B --> C[Channel Landing<br/>Featured episodes · Levels · Search]
  C --> D[Episode Card<br/>Title · Level · Length · Topics]
  D --> E[Episode Detail Screen]
  E -->|Play| F[Audio Player<br/>Play/Pause · 15s +/- · Speed]
  E --> G[Transcript Pane<br/>UA/EN toggle · auto-scroll]
  G --> H{Tap a word?}
  H -->|Yes| I[Tooltip: definition · add to deck · hear word]
  H -->|No| F
  E --> J[Quick Quiz (3–5 Qs)]
  J --> K[Results + Explanations<br/>Weak topics surfaced]
  K --> L[Shadowing Practice<br/>Record & score · feedback]
  L --> M[SRS Review Deck<br/>Words & phrases from episode]
  E --> N[CTA: “Full catalog on UkrainianLessons.com”]
  M --> O[Return to Channel or Next Episode]
```

---

## 2) Screen Wireframe (ASCII)

```
┌──────────────────────────────────────────────────────────────┐
│  Episode Detail – ULC #37: At the Café          [A2]  12:34  │
│  Powered by UkrainianLessons.com (logo + host avatar)        │
├──────────────────────────────────────────────────────────────┤
│  ▶︎ 00:12 / 12:34   [⏪15] [⏯] [⏩15]  Speed: 0.8× 1.0× 1.2×   │
├──────────────────────────────────────────────────────────────┤
│  Transcript  [UA ▾]  [EN]   Auto‑scroll: ON                  │
│  — Привіт! Що ви будете замовляти сьогодні?                  │
│    Hi! What will you order today?                            │
│     (Tap word → tooltip: definition · add to deck · play)    │
├──────────────────────────────────────────────────────────────┤
│  Culture Note: Café etiquette (ordering, please/thank you)   │
├──────────────────────────────────────────────────────────────┤
│  Practice                                                     │
│  [Quick Quiz 5Q]   [Shadowing]   [Save All New Words (8)]     │
├──────────────────────────────────────────────────────────────┤
│  CTA: Like this lesson? Explore the full catalog on ULC →     │
└──────────────────────────────────────────────────────────────┘
```

---

## 3) Component Specs

### Audio Player
- Play/Pause, ±15s skip, speed (0.8×–1.5×), background audio, remember position.

### Transcript Pane
- Time‑synced lines; **UA/EN toggle**; auto‑scroll; tap‑to‑define; add‑to‑deck; inline audio for words/lines.

### Culture Note
- 120–180 words; etiquette/context; links to related holiday or symbol; vetted by ULC.

### Quick Quiz (3–5 questions)
- Mix of **cloze**, **MCQ**, **ordering**. Immediate explanations; show weak areas.

### Shadowing
- Line-by-line **record → compare → score** (intelligibility and timing). Retry loop.

### SRS Deck
- Auto-generated deck from the episode’s glossary; spaced intervals; daily reminders.

### CTA to ULC
- End-of-lesson CTA with **UTM/referral** back to UkrainianLessons.com.


---

## 4) Data & Telemetry

**Events**
- `episode_viewed`  
- `episode_listened_seconds`  
- `transcript_toggle` (UA↔EN)  
- `word_lookup`, `add_to_deck`  
- `quiz_started`, `quiz_completed`, `quiz_score`  
- `shadowing_started`, `shadowing_minutes`, `shadowing_score`  
- `srs_items_reviewed`  
- `cta_ulc_clicked`, `ulc_conversion` (via referral callback)

**Key Metrics**
- Listen completion %, Quiz avg %, Words saved/episode, Shadowing minutes, SRS retention %, CTA CTR, ULC conversion %.

---

## 5) Content & Level Tagging

| Field | Examples |
|---|---|
| Level | A1, A2, B1 |
| Topic | Café, Family, Holidays |
| Skills | Listening, Pronunciation, Culture |
| Duration | 8–15 min |
| Keywords | etiquette, ordering, greetings |

---

## 6) QA Checklist (excerpt)

- Audio clear; speeds function; background play OK.  
- Transcript time-sync accuracy ±300 ms.  
- UA/EN toggle safe for beginners (default UA with line-by-line EN).  
- Quiz explanations correct; no ambiguous distractors.  
- Shadowing mic permissions + latency acceptable; scores reproducible.  
- CTA deep links track UTMs; attribution verified end-to-end.

---

## 7) Accessibility

- Full keyboard control; captions; transcript readable at 200% zoom.  
- Color contrast ≥ WCAG AA; avoid color-only cues.  
- Provide **download transcript** for screen-readers where licensing allows.

---

## 8) Strings (copy suggestions)

- “**Culture Note**: What’s polite to say when ordering in Ukraine?”  
- “**Shadowing**: Record the line, then match the rhythm.”  
- “**Save all 8 new words** to your review deck.”

---

## 9) Implementation Tasks (tracker-ready)

- [ ] Content ingest pipeline (RSS/audio + transcript parser)  
- [ ] Player + transcript sync component  
- [ ] Dictionary + add-to-deck service  
- [ ] Quiz generator + reviewer  
- [ ] Shadowing (ASR/scoring) module  
- [ ] SRS deck + notifications  
- [ ] ULC attribution & CTA with referrals  
- [ ] Analytics events + dashboard  
- [ ] QA checklist sign-off

---

## 10) Future Enhancements

- Episode **collections** by theme (Holidays, Café, Family).  
- **Creator Q&A** episodes with the host.  
- **Live challenges** (weekly listening party + quiz).  
- **Dialect variants** exposure for advanced learners.

# Spaced Repetition Flashcards PWA

A standalone, offline-first Progressive Web App (PWA) delivering a spaced repetition flashcard engine. Built in pure HTML5, CSS3, and modern vanilla JavaScript with no external dependencies or build pipelines.

---

## Core Architecture

- **Single-File Execution:** Complete UI, styles, logic, service worker registration, and procedural SVG media assets contained within a single `index.html`.
- **Offline & Standalone Operation:** Service Worker registration via inline Blob URL caching assets for air-gapped usability; configured with full PWA web manifest metadata.
- **Adaptive Display Engine:** Dynamic layout handling portrait orientation lock overlays, device safe areas (`env(safe-area-inset-*)`), and procedural category-specific vector backgrounds.
- **Touch Gesture System:** Hardware-accelerated 3D card physics using pointer and touch event listeners with directional swipe resolution, damping, and tactile haptic feedback.
- **Speech Synthesis:** Integrated Web Speech API (`SpeechSynthesisUtterance`) support for automated read-aloud functionality across British English and standard system voices.

---

## Spaced Repetition Algorithm

The retention scheduling engine implements a modified SuperMemo SM-2 algorithm:

1. **Repetition Progression:**
   - **Repetition 0:** Initial review schedule set to 1 day.
   - **Repetition 1:** Second successful graduation step set to 6 days.
   - **Repetition $\ge 2$:** Interval scales exponentially:
     $$I(n) = \text{round}(I(n - 1) \times EF)$$
2. **Easiness Factor (EF):**
   - Base initial factor: `2.5`
   - **Easy Review:** Increments EF by `+0.1` and advances repetition count.
   - **Hard Review (Lapse):** Resets repetition count to `0`, sets interval to `1`, penalizes EF by `-0.2` (bounded at a minimum floor of `1.3`), and re-queues the card for a 10-minute retry interval.
3. **Progressive Program Unlocking:**
   - Cards map to sequential `day` properties.
   - Content unlocks relative to a configurable program start date stored in local persistence:
     $$\text{Program Day} = \max\left(1, \left\lfloor \frac{\text{Current Date} - \text{Start Date}}{86,400,000} \right\rfloor + 1\right)$$

---

## Question Bank Schema

Custom question sets can be imported via JSON using either a raw array or a container object (`questions` or `deck` key):

```json
[
  {
    "id": "gen_custom_01",
    "cat": "General",
    "day": 1,
    "q": "What is the capital of France?",
    "a": "Paris",
    "interval": 0,
    "reps": 0,
    "efactor": 2.5,
    "dueDate": 0
  }
]

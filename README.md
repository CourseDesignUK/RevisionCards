# Firefighter Spaced Repetition (Flashcards SR)

A standalone, mobile-first Progressive Web App (PWA) designed for high-retention technical study across critical operational firefighting disciplines. The application executes a modified SuperMemo SM-2 algorithmic scheduling model directly in the browser with zero external dependencies.

---

## Features

- **Algorithmic Spaced Repetition:** Dynamic SM-2 scheduling engine adjusting intervals and Easiness Factors ($EF$) based on binary active recall outcomes (`Easy` vs. `Hard`).
- **Zero-Dependency Architecture:** Single-file distribution containing embedded SVG vector assets, base64 Web App Manifest, offline Service Worker, and styling.
- **Touch & Gesture Physics:** Multi-axis 3D card gestures supporting tilt dampening, threshold drag-to-rate swipes, and 3D card flipping.
- **Auditory Feedback & Speech Synthesis:** Web Speech API integration for automatic text-to-speech readouts and Web Audio API synthesized completion chimes.
- **Client-Side Persistence:** Instant synchronization to `localStorage` on every review, automated snapshot backups upon queue completion, and full JSON import/export routines.
- **Orientation Control:** Automatic lock to portrait viewport with an integrated screen-rotation safeguard.

---

## Core Architecture & Spaced Repetition Engine

The engine modifies the standard SuperMemo SM-2 algorithm to streamline reviews into a binary interface: **Hard** (Lapse/Fail) and **Easy** (Pass/Recall).

### State Model

Each flashcard maintains the following state schema:

```json
{
  "id": "arff_1",
  "cat": "ARFF",
  "q": "Question prompt text",
  "a": "Answer verification text",
  "interval": 0,
  "reps": 0,
  "efactor": 2.5,
  "dueDate": 0
}

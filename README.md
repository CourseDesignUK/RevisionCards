# Firefighter Spaced Repetition

A single-file Progressive Web Application (PWA) designed for high-retention spaced repetition training. Engineered for firefighting disciplines including ARFF, Breathing Apparatus (BA), General Operations, Road Traffic Collisions (RTC), and Structural Firefighting.

## Core Features

*   **Progressive 100-Day Curriculum:** Cards are mapped to specific days (1 to 100). The user sets a program start date on initial launch; the system calculates the current day and selectively unlocks new material daily.
*   **Spaced Repetition Engine:** Built on a modified SuperMemo-2 (SM-2) algorithm. Recall quality dictates future intervals (base steps of 1 day and 6 days, scaling dynamically via an evolving Easiness Factor).
*   **Gesture-Based Interface:** Hardware-accelerated swipe mechanics. Swipe right for "Easy" (graduates card) or swipe left for "Hard" (resets interval to a 10-minute penalty queue).
*   **Text-to-Speech (TTS):** Integrated Web Speech API for automated read-aloud of questions and answers.
*   **Offline PWA Architecture:** Zero external dependencies. Embedded service worker and manifest allow native home-screen installation. State autosaves to local storage.
*   **Data Portability:** JSON import/export functionality for complete state backups, history restoration, and custom question bank injection.

## Usage Instructions

### Initialization
Load the `index.html` file in a modern browser. Add to the mobile home screen to enable standalone PWA mode. Upon first launch, the system prompts for a program start date. This establishes the baseline for the progressive daily unlock system.

### Controls
*   **Tap / Click Card:** Flips the card between question and answer faces.
*   **Swipe Right:** Logs "Easy". Extends the review interval.
*   **Swipe Left:** Logs "Hard". Drops the card into the immediate review queue.
*   **Category Bar:** Filters the active deck by subject matter.
*   **Practice Ahead (Cram Mode):** Bypasses the SM-2 interval timer to allow continuous review of unlocked cards without affecting future spaced repetition intervals.

### Data Management
Use the Title Screen to manage data:
*   **Export Data:** Downloads a JSON snapshot of the current deck, including SM-2 intervals and repetitions.
*   **Restore Data:** Overwrites the current state with a previously exported JSON backup.
*   **Load Question Bank:** Merges new questions into the existing deck without overwriting current progress.

## Custom Question Bank Format

To import custom question sets, format the JSON payload as an array of objects. Note the `day` integer parameter controls the progressive unlock schedule.

```json
[
  {
    "id": "custom_id_001",
    "cat": "ARFF",
    "day": 1,
    "q": "What is the maximum response time mandated by ICAO Annex 14?",
    "a": "Not exceeding 2 minutes in optimum conditions."
  },
  {
    "id": "custom_id_002",
    "cat": "Structural",
    "day": 2,
    "q": "Define the Neutral Plane.",
    "a": "The horizontal boundary separating the hot, pressurized upper layer of smoke from the lower layer of incoming cool air."
  }
]

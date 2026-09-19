# Firefighter Spaced Repetition (Flashcards SR)

A standalone, mobile-first Progressive Web App (PWA) built for high-retention firefighting revision. Uses a modified SuperMemo SM-2 algorithm to schedule reviews locally in the browser with zero external dependencies.

---

## Features

- **Spaced Repetition:** Automatic review scheduling based on recall difficulty.
- **Single-File Architecture:** HTML, CSS, JavaScript, manifest, and SVG assets in one file.
- **Gesture Controls:** Touch swipe (left for Hard, right for Easy) and 3D card flipping.
- **Speech & Audio:** Optional auto text-to-speech for cards and audio fanfare on queue completion.
- **Local Persistence:** Automatic saves to `localStorage` plus manual JSON backup/restore.
- **Portrait Enforced:** Built-in lock overlay for mobile displays.

---

## The Spaced Repetition Logic

Cards are rated using two options:

- **Easy (Pass):**  
  - Review 1: Due in **1 day**  
  - Review 2: Due in **6 days**  
  - Review 3+: Due in $\text{Previous Interval} \times \text{Easiness Factor}$ (days)  
  - Repetition counter increases; Easiness Factor increases by `0.1`.
- **Hard (Fail):**  
  - Resets repetitions to `0` and base interval to `1`.  
  - Easiness Factor decreases by `0.2` (minimum `1.3`).  
  - Scheduled for immediate review in **10 minutes**.

---

## Included Deck Categories

Pre-loaded with 50 operational cards:

- **ARFF:** Airport rescue, foam levels, aircraft hazards, and ICAO response rules.
- **BA:** Breathing apparatus procedures, turnaround limits, and guideline drills.
- **General:** Operational priorities, JESIP M/ETHANE, BLEVEs, and dynamic risk assessment.
- **RTC:** Airbag distances, EV isolation, stabilization, and hydraulic tool tactics.
- **Structural:** Flashover/backdraft indicators, CFBT gas cooling, and thermal balance.

---

## How to Use

1. **Start Drill:** Tap **Start** on the title screen.
2. **Select Discipline:** Filter cards via the top category bar or leave on **All**.
3. **Flip Card:** Tap the card body or the **Flip** button to see the answer.
4. **Rate Recall:**
   - Swipe **Right** or tap **Easy** if remembered.
   - Swipe **Left** or tap **Hard** to review again in 10 minutes.
5. **Clear Queue:** Practice until the queue is finished. Use **Practice Ahead (Cram Mode)** to keep reviewing ahead of schedule.

---

## Data & Question Banks

All options are on the title screen:

- **Load Question Bank:** Add custom questions via JSON format:
  ```json
  [
    {
      "cat": "ARFF",
      "q": "Question text here?",
      "a": "Answer text here."
    }
  ]

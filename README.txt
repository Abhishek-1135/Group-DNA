# GroupDNA — Hostel Friends Chat Analyzer

> Turning a raw WhatsApp `.txt` export into a full personality & activity report — using nothing but core Python and NumPy.

GroupDNA is a data analytics mini-project that parses an exported WhatsApp group chat and extracts communication patterns, activity trends, and per-member "personality archetypes" — all built from scratch, without `pandas` or `matplotlib`.

---

## ✨ Highlights

- **Zero dependencies beyond NumPy** — no `pandas`, no `matplotlib`. Parsing is done with plain string operations and dictionaries; visuals are rendered as text-based bar charts and heatmaps.
- **8 self-contained features**, each in its own notebook section, building up to a final auto-generated report.
- Works on any exported WhatsApp chat `.txt` file (no media, no personal data required beyond the export itself).

---

## 📊 Sample Output

Run on a sample chat (`hostel_friends_chat.txt` — 6 participants, 71-day export window):

```
============================================================
GROUPDNA REPORT — "Hostel Friends"
============================================================
40 days • 324 messages • 6 members
Period : 01 April 2024 to 10 May 2024
Busiest day : 01/04/24 (13 messages)
Busiest hour : 18:00 - 19:00

MESSAGES PER PERSON
Rahul      ████████████████████ 70 (21.6%)
Priya      ████████████████████ 70 (21.6%)
Aman       ██████████████████ 64 (19.8%)
Neha       ████████████████ 57 (17.6%)
Karan      ██████████████ 51 (15.7%)
Vikas      ███ 12 (3.7%)

ACTIVITY HEATMAP (hour of day, columns 00 to 23)
          00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23
Rahul      . . . . . . . ▒ ▒ ▒ ▒ . . ▒ ▒ . . ░ █ . . . ▒ .
Priya      . . . . . . . . ▒ ▒ █ ▒ █ . . . ▒ ░ . ▒ ▒ . . .
Aman       . . . . . . . . . . ▒ ▒ ▒ ▒ . . . ░ ▒ ▒ ▒ . ▒ ▒
Karan      . . . . . . . . . . . . █ . ▒ ▒ . ░ █ . ▒ . . .
Neha       . . . . . . . . . █ █ . . . . ▒ ▒ ░ . . . █ . .
Vikas      . . . . . . . ▒ . . . . . . . . . . . . . . . ░

THIS GROUP'S FAVOURITE WORDS
good         ████████████████████ 46
yes          ██████████████ 33
morning      ███████████ 26
guys         █████████ 22
anyone       ████████ 20

RESPONSE PATTERNS
Fastest replier : Karan (avg 135.8 minutes)
Slowest replier : Vikas (avg 7.7 hours)

LONGEST SILENT STREAKS
Vikas     : 5 days
Rahul     : 0 days
Priya     : 0 days
Aman      : 0 days
Karan     : 0 days
Neha      : 0 days

PERSONALITY ARCHETYPES
Rahul - THE QUESTION MASTER
Priya - THE GROUP MOM
Aman  - THE QUESTION MASTER
Karan - THE GROUP MOM
Neha  - THE GROUP MOM
Vikas - THE QUESTION MASTER
```

![GroupDNA poster](groupdna_poster_final.png)

---

## 🧩 Features

| # | Feature | What it does |
|---|---------|---------------|
| 1 | **Chat Parser** | Reads the raw `.txt` export, separates real messages from system notices, media-omitted lines, and deleted messages. |
| 2 | **Group Overview** | Total messages, participant count, chat duration, and a per-person message share. |
| 3 | **Most Active Day & Hour** | Finds the single busiest calendar day and the busiest hour-of-day across the whole chat. |
| 4 | **Activity Heatmap (NumPy)** | Builds a participant × hour-of-day matrix with `numpy.zeros` and renders it as a `. ░ ▒ █` intensity heatmap. |
| 5 | **Top Words** | Tokenizes and cleans message text (stop-words removed) to surface the group's most-used words. |
| 6 | **Response Speed & Silent Streaks** | Calculates average reply time per person and the longest stretch of consecutive silent days. |
| 7 | **Personality Archetype Detection** | Scores every member against 8 behavioural archetypes (Spammer, Group Mom, Night Owl, Storyteller, Drama Queen, Ghost, Comedian, Question Master) and assigns the strongest match. |
| 8 | **Final Report Generator** | Combines every feature above into one formatted, terminal-style summary report. |

### Personality Archetypes

| Archetype | Signal |
|---|---|
| 🕵️ The Spammer | Long streaks of consecutive back-to-back messages |
| 🤱 The Group Mom | Frequent caring/check-in keywords ("take care", "eat", "please", etc.) |
| 🌙 The Night Owl | High share of messages sent between 11 PM – 4 AM |
| 📖 The Storyteller | High average word count per message |
| 🎭 The Drama Queen | Frequent ALL-CAPS or multi-exclamation messages |
| 👻 The Ghost | Silent for a large share of the chat's active days |
| 😂 The Comedian | Frequent "lol / lmao / haha" style messages |
| ❓ The Question Master | High share of messages ending in "?" |

---

## 🛠️ Tech Stack

- **Python 3** — core logic, string parsing, dictionaries
- **NumPy** — the activity heatmap matrix
- **datetime** — timestamp parsing and response-time / silent-streak calculations
- ❌ No `pandas` — every aggregation is done with native dicts and loops
- ❌ No `matplotlib` — every chart is rendered as text (block characters `█ ▒ ░ .`)

---

## 🚀 Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/<your-username>/GroupDNA.git
cd GroupDNA
```

### 2. Export your WhatsApp chat
On WhatsApp: open the group → **⋮ More → Export chat → Without media**. Save the `.txt` file into the project folder.

### 3. Update the file path
In the notebook, set:
```python
file_path = "/content/your_chat_export.txt"
```

### 4. Run all cells
Open `Abhishek_Kr_Minor_Project_1.ipynb` in Jupyter / Google Colab and run the cells top to bottom — each feature prints its own output, and the final cell prints the combined report shown above.

**Requirements:**
```
numpy
```
(everything else is Python standard library)

---

## 📁 Project Structure

```
GroupDNA/
├── Abhishek_Kr_Minor_Project_1.ipynb   # main notebook — all 8 features
├── hostel_friends_chat.txt             # sample exported chat used for this README
├── groupdna_poster_final.png           # project poster
└── README.md
```

---

## 📌 Notes & Limitations

- The parser expects the standard WhatsApp export format: `DD/MM/YY, HH:MM - Sender: Message`. Exports from iOS vs Android sometimes differ slightly in punctuation and may need a small tweak to the split logic.
- Media, deleted, and system messages are detected and excluded from analysis, not deleted from the source file.
- Personality archetypes are simple rule-based heuristics for fun/insight — not a validated psychological assessment.

---

## 🙌 Acknowledgements

Built as a minor project to practice raw data-wrangling in Python — parsing, aggregation, and reporting — without leaning on higher-level data libraries.

# 🦊 FlashPal

> A whimsical Anki clone — plant a card, water it daily, watch it bloom. 🌱

FlashPal is a spaced-repetition flashcard app with a soft, playful "memory garden"
aesthetic. It's a **single self-contained HTML file** — no build step, no
dependencies, no server. Just open it and study.

## ✨ Features

- **Real spaced repetition** — an SM-2-style scheduler tracks each card's ease,
  interval and reps. Grade a card *Again / Hard / Good / Easy* and FlashPal shows
  the next review interval right on the button (`<10m`, `1d`, `3d`, months, years…).
- **Decks & cards** — create decks with a mascot emoji, add / **edit** / delete
  cards, see per-deck "due" counts at a glance.
- **Cloze deletions** — wrap any word in `{{double braces}}` and FlashPal blanks
  it on the front, revealing it on the back. Multiple blanks per card supported.
- **Bulk import** — paste many cards at once, split by **Tab**, `|`, or comma
  (cloze lines need no separator).
- **Study sessions** — shuffled due queue, *Again* cards loop back within the
  session, a progress bar, and "Study everything due" across all decks at once.
- **Stats panel** — due / new / learning / mature counts, today's reviews, and a
  7-day "reviews due" forecast chart.
- **Backup & restore** — export your whole garden to a JSON file and import it
  back on any device. No account, no cloud, no tracking.
- **Dark mode** — a soft "night garden" theme, remembered across visits.
- **Local persistence** — everything is saved to `localStorage`; your garden
  survives reloads.
- **Whimsy** — a 🦊 mascot that bounces when you grade, drifting background
  doodles, 3D card flips, confetti on *Easy* and on finishing, and a daily ⚡
  streak counter.

## ⌨️ Keyboard shortcuts

| Key | Action |
|-----|--------|
| `Space` | Flip the current card |
| `1` `2` `3` `4` | Grade **Again / Hard / Good / Easy** |
| `Esc` | Close a dialog |
| `Enter` | Save in the new-card / new-deck dialog |

## 🚀 Run it

Just open the file:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
```

…or serve it locally if your browser is strict about `file://`:

```bash
python3 -m http.server 4173
# then visit http://localhost:4173
```

It ships with two demo decks (World Capitals, Fun Facts) so it's alive on first open.

## 🧠 How the scheduler works

Each card stores `ease` (default 2.5), `interval` (days) and `reps`. On review:

- **Again** → reps reset, interval → ~10 min, ease drops a little.
- **Hard / Good / Easy** → reps increment; early reps step `1d → 3d`, then
  `interval × ease` (nudged down for Hard, up for Easy). Ease floors at 1.3.

Due cards are anything whose `due` timestamp is in the past. Simple, transparent,
and entirely in `index.html` — read it, tweak it, make it yours.

## 📄 License

MIT — see [LICENSE](LICENSE).

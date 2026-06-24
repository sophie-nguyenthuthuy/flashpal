# 🦊 FlashPal

> A whimsical Anki clone — plant a card, water it daily, watch it bloom. 🌱

FlashPal is a spaced-repetition flashcard app with a soft, playful "memory garden"
aesthetic. It's a **single self-contained HTML file** — no build step, no
dependencies, no server. Just open it and study.

## ✨ Features

- **Two schedulers** — modern **FSRS-4.5** (stability/difficulty model with a
  tunable target-retention slider) or classic **SM-2**, switchable in Settings.
  Either way the next interval is previewed on each grade button.
- **Decks & sub-decks** — create decks with a mascot emoji; name one
  `Spanish::Verbs` and it nests under a **Spanish** group with an aggregate
  "study all" button.
- **Cards** — add / **edit** / delete, with **images & audio** (pick a file or
  paste `![](url)` / `@[audio](url)`) and **tags** (filter the deck by tag, or
  study just one tag).
- **Cloze deletions** — wrap any word in `{{double braces}}` and FlashPal blanks
  it on the front, revealing it on the back. Multiple blanks per card supported.
- **Anki `.apkg` import** — drop in a real Anki export and FlashPal reads the
  notes into a new deck, **inlining packaged images & audio** as data URLs
  (unzip + SQLite parsed in-browser; needs a connection).
- **Leech detection** — cards you keep failing are auto-flagged `🪤 leech` and
  suspended after N lapses (threshold in Settings; 0 disables).
- **Suspend / resume** any card (⏸️/▶️) to take it out of rotation.
- **Card info** — an ℹ️ popup per card: stability/difficulty/retrievability (or
  ease/reps under SM-2), lapses, next-due, and a sparkline of recent grades.
- **Custom study** — extra practice that won't disturb your schedule: *study
  ahead* (pull in cards due soon — these do reschedule), *cram all*, or
  *practice lapsed & leeches* (the last two are peek-only).
- **Text-to-speech** — speak the current side aloud (🔊 / press `S`), with an
  optional auto-speak setting that reads the front on show and answer on flip.
- **Keyboard shortcuts** — `Space` flip · `1-4` grade · `S` speak · `U` undo ·
  `?` cheatsheet. Press `?` any time for the full list.
- **Search everything** — fuzzy search front/back/`#tag` across all decks; click
  a result to jump straight into editing it.
- **Undo** — take back the last review mid-session (`u` or ⌘/Ctrl-Z); it restores
  the card's schedule, the queue, and your streak.
- **Growth calendar** — a GitHub-style activity heatmap of the last 18 weeks in
  the stats panel, so you can watch your streak bloom.
- **Manage** — rename decks (add `::` to nest them), move a card to another deck,
  filter a deck by tag.
- **Typed-answer mode** — per deck, type the answer and FlashPal checks it
  (case-, accent- and punctuation-insensitive), then suggests a grade.
- **Reverse cards** — per deck, add a back → front review for each basic card,
  scheduled independently from the forward direction.
- **Per-deck options** — a new-cards-per-day limit (so big decks don't bury you),
  plus the typed and reverse toggles, all under ⚙️ Options.
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

Pick your algorithm in **Settings**:

- **FSRS-4.5** (default) — each card carries a memory **stability** `S` and
  **difficulty** `D`. After a review FSRS estimates your recall probability and
  picks the next interval so it lands at your **target retention** (default 90%;
  raise it for more frequent reviews). This is the same model modern Anki uses.
- **SM-2** (classic) — each card stores `ease` (2.5), `interval` and `reps`;
  *Again* resets, *Hard/Good/Easy* step `1d → 3d → interval × ease`.

Reverse cards keep a **separate** schedule per direction. Due cards are anything
whose `due` timestamp has passed (capped by each deck's new-cards-per-day limit).
It's all plain JS in `index.html` — read it, tweak it, make it yours.

## 📄 License

MIT — see [LICENSE](LICENSE).

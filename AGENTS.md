# AGENTS.md

## Cursor Cloud specific instructions

This is the **tutorials** repo (`aiccmaster79/tutorials`): a static catalog
(`index.html`) plus self-contained HTML tutorials. There is no backend, package
manager, build step, or test suite. Do not add build tooling or new CDN
libraries (fonts named by a chosen visual direction are allowed). Design rules
live in [`instructions/00-shared-spec.md`](instructions/00-shared-spec.md).

**Default delivery is an explainer-style tutorial**, not a widget-heavy workshop.
Do not add interactives, activities, a quiz, speaker notes, or a colour system
until the author has answered the questions in [Ask before you build](#ask-before-you-build).

Do **not** apply these structure changes to the sibling `presentations` repo.

### Running it

- Serve the folder over HTTP, e.g. `python3 -m http.server 8080` then
  `http://localhost:8080/index.html`. Use HTTP (not `file://`).
- There is nothing to install or build; editing an `.html` file and refreshing
  the browser is the whole dev loop.

### Gotchas

- **Outbound HTTPS is required at runtime** when a page pulls fonts or CDNs.
- Do not rename files that `index.html` already links to — those links are
  hand-maintained.

### Read these first

1. This file (defaults and questions).
2. [`instructions/00-shared-spec.md`](instructions/00-shared-spec.md) —
   constraints, explainer spine, optional activity/quiz slots, photos.
3. Any **course specs** in this repo (see [Course specs](#course-specs)).
4. A visual direction file in `instructions/` (`1a-ledger.md` … `1e-studio.md`)
   only after colour and layout are agreed.
5. [`instructions/PRESENTATION-UPGRADE-PLAN.md`](instructions/PRESENTATION-UPGRADE-PLAN.md)
   is **legacy inventory** (widget recipes, old slide counts). It is not the
   slide recipe and not a reason to add widgets.

---

## Ask before you build

Ask these questions **before** creating or rebuilding a tutorial. If the author
has not answered, ask — do not assume “yes”.

1. **Widgets?** Default **no**. “Do you want interactive widgets (drag-and-drop,
   simulators, click-to-reveal boards, and so on) in this tutorial? Default is
   an explainer with no widgets.”
2. **Activities and quiz?** Default **no**. “Do you need in-deck activities
   (tasks on a slide) and/or a scored quiz? Default is explainer only: concept,
   example, takeaways, close.”
3. **Colour?** No default until they pick. “Should this use **white text on a
   black background**, or **college brand colours** (orange `#F7931E`, purple
   `#8A2BE2`, teal `#00BDA5`)?” College mark lives in [`logos/`](logos/):
   `src_logo.svg` / `src_logo.png` (brand letters, black wordmark for light
   grounds), `src_logo_on_black.svg` (white wordmark for dark grounds),
   `src_logo_mobile.svg` (letters only).
4. **Speaker notes?** Default **no**. “Do you need `aside.notes` on slides for
   presenter view (S key)?”

Do not invent a third colour system unless they name one. If they want both a
dark classroom look and brand accents, confirm that explicitly (for example
white-on-black with brand used only for rules, labels, and highlights).

---

## Course specs

Content must be **relatable to any course spec provided in this repo**.

Before writing slides:

1. Search `instructions/`, `photos/`, unit outlines, assessment criteria,
   learning outcomes, schemes of work, `*spec*`, qualification markdown, PDFs,
   and [`instructions/PRESENTATION-IDEAS.md`](instructions/PRESENTATION-IDEAS.md)
   “Assessment fit” notes.
2. Map each teaching slide to a named outcome, assessment criterion, or unit
   heading from those files. Use the spec’s wording where it helps learners and
   assessors recognise the work.
3. Prefer classroom and workplace examples that match the spec’s level and
   context. **Files in this repo win** over any assumed OCN NI Level 2 default.
4. If no spec is present, say so, then write an explainer that still uses
   concrete, checkable language (what the learner can do, not a slogan). Do not
   pad with career-pathways or generic “Thank You” slides.

---

## Teaching structure

### Default — explainer tutorial

Use this spine unless the author asked for activities or a quiz.

| # | Slide |
| --- | --- |
| 1 | Title — topic, level/unit from the spec if known |
| 2 | The hook — one real consequence of getting this wrong |
| 3 | Objectives — max 4, verb-led, mapped to the spec |
| 4 | Core concept — the diagram or ladder the deck hangs on |
| 5–7 | One slide per part of the concept |
| 8 | Worked example — named, relatable to the spec’s setting |
| 9 | Trade-offs or limits |
| 10 | Common faults — symptom → likely cause → fix (table, not a widget) |
| 11 | Key takeaways — max 4 |
| 12 | Close — one instruction for what to do next |

Cut unless the topic truly needs them: “How to use this deck”, keyboard hints,
glossary slide, deck map, career pathways, stats-bar, “Thank You”.

Searchable jargon, if needed, is a `?` overlay, not a slide.

### If they asked for activities

Insert after the concept parts: **Activity 1** (signature task), keep the
worked example, then **Activity 2** (applied scenario). Keep activities as
plain steps and success criteria unless they also asked for widgets.

### If they asked for a quiz

Add a short scored quiz (4–6 questions) and a results slide that says what a
wrong answer means. Skip quiz and results when they said no.

### If they asked for widgets

Follow widget conventions in
[`instructions/00-shared-spec.md`](instructions/00-shared-spec.md):
`Reveal.on('ready')`, click/tap/keyboard, `aria-live="polite"` on scores, wrong
answers explain **why**. Do not copy widgets “because other decks have them”.

Broadcast direction (`1c`) may use more slides (one idea per slide). Other
directions stay on the explainer spine or the agreed activity/quiz extras.

---

## Must / must not

**Must**

- Never rename a file that `index.html` already links.
- Min type size **24px** at 1920×1080 when authoring a reveal.js deck;
  `width: 1920, height: 1080`, `margin: 0.04`.
- `.back-to-index` pill and `.site-credit` line on catalog-linked decks.
- Absolute `px` type on reveal decks, not `em` relative to reveal’s root.
- Tie examples and objectives to provided course specs.
- Apply the colour choice they confirmed (white-on-black **or** brand triad).

**Must not**

- Add widgets, activities, quiz, or speaker notes unless they asked.
- Edit the sibling `presentations` repo for this structure work.
- `.animated-gradient` headings.
- `backdrop-filter` glass cards as the default container.
- Decorative Font Awesome that repeats the heading word.
- `grid-template-columns: repeat(auto-fit, minmax(240px, 1fr))` as the universal layout.
- Generated SVG illustration; photos are author-supplied plates when used
  (`photos/` in this repo).
- Treat particle canvas or a 26–34 slide count as required.
- Add new CDNs except fonts the chosen direction already names.

---

## Verifying a change

Open the affected page over HTTP, check the browser console is clean, and
confirm the explainer spine (or the extras they requested) with no cut-list
slides.

Also check, **when they asked for them**:

- widgets: exercise each one
- quiz: run through to results
- speaker notes: press **S**
- colour: white-on-black **or** brand, matching the answer (and scheme toggle
  only if they asked for both)

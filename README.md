# Line 3: Reading the Weekly Numbers

An interactive learning activity that helps production workers read a weekly production sheet with
confidence and question what it does and does not tell them.

Built for the Gordon TAFE Learning Experience Design candidate task *Read the Numbers*.

## What it is

A ten step, self contained activity of about 15 to 20 minutes. The learner reads a fictional
manufacturer's weekly figures for Line 3, investigates a week that looks wrong, builds two charts
that tell opposite stories from the same numbers, works out which questions the sheet cannot answer,
and writes a short note for a team meeting that they can print.

Nothing is scored, marked or saved. There are no accounts and no backend.

## Running it

The activity is a single file with no dependencies, no build step and no framework.

- **Locally:** open `public/index.html` in any modern browser. No server is required.
- **Hosted:** publish the `public/` directory as the site root.

> **Deployment note.** Publish `public/` only, never the repository root. Set the output or publish
> directory to `public` in your host's settings. Everything in `Resources/` is working material:
> the candidate brief, private project notes and three independent review reports. None of it
> should be reachable from the public activity.

## Repository layout

```
public/index.html                  the activity, the only file that gets deployed
README.md                          this file
Resources/
  Candidate_Brief_Read_the_Numbers.docx    the original task brief
  Init-Project-Notes.md                    the candidate's own planning notes
  Admin/
    proposed-approach.md                   the approach agreed before any code
    design-decisions.md                    design decisions, rejected options, future work
    review-findings.md                     feedback received and how each item was handled
    testing-results.md                     testing performed on every version
    prompt-history.md                      full prompt history, including discarded approaches
    Line_3_Independent_Data_Audit.html     independent data audit (ChatGPT), unedited
    Line_3_Final_Regression_Audit - GPT.html  independent regression audit (ChatGPT), unedited
    Gemini_Audit.md                        independent instructional design review (Gemini), unedited
```

## Design Lens

A reviewer feature, off by default and separate from the learner's journey.

The glasses icon in the top right turns it on. Marked areas of the page then carry a small purple
marker; hovering over the area, or selecting the marker with keyboard or touch, shows a short note
explaining why that part was built the way it was. Press Escape or the icon again to turn it off.

It exists so an interview panel can see the reasoning behind the design without reading the project
documentation. The notes restate decisions already recorded in `Resources/Admin/design-decisions.md`
and the review history. Where no reason was recorded, nothing is marked.

A disclaimer sits under the header whenever it is on: the explanations were written with AI from the
developer's notes and development discussions, and may not capture every decision made along the
way. Design Lens never prints, does not change the activity, and does not affect progress.

## Learning outcomes

The brief sets three. After completing the activity a worker can:

1. **Read a simple table and chart and say in plain words what they show.** Taught in steps 2 and 3,
   and evidenced by matching three notes to weeks and by which week they choose to investigate.
2. **Spot at least two ways a table or chart can give a misleading impression.** Five are covered:
   a scale that does not start at zero, showing only part of the period, an average pulled by one
   unusual week, a percentage that hides a count, and a measure recorded differently from week 10.
   Evidenced by the learner building both misleading charts themselves in steps 4 and 5.
3. **Decide what question they would ask before acting on the numbers.** Taught in steps 3, 7 and 8,
   and evidenced by which measures they choose to reveal and by the note they write.

## How it works

Ten steps, each with one idea and one thing to do. Difficulty builds from reading a figure, to
judging what is unusual, to seeing presentation mislead, to seeing measurement mislead when nothing
looks wrong, to deciding.

There are no multiple-choice questions. Each step uses a different interaction: matching notes to
weeks, switching measures, setting chart controls, choosing which columns to reveal, selecting weeks
in two linked charts, and completing a part-written note. Feedback explains the reasoning rather
than marking an answer right or wrong.

Everything is computed at runtime from a single `DATA` array, so no figure on screen can drift from
the figures in the brief.

## Accessibility

Keyboard navigable throughout, with focus returned to the control used after every redraw. Every
chart has a table equivalent, and charts that are not interactive are not focusable. Live regions
announce feedback. Colour is never the only signal. All motion is behind `prefers-reduced-motion`.

**Not yet verified:** no screen reader or other assistive technology testing has been carried out on
any version. The accessibility work above has been checked structurally and programmatically, which
is not the same thing.

## Data

The twelve weeks of figures and both supervisor notes are reproduced exactly as supplied in the
brief and are not altered anywhere in the activity. Averages, the median and the estimated scrap
parts are calculated at runtime from those figures rather than typed in.

Ridgeway Components and Line 3 are fictional.

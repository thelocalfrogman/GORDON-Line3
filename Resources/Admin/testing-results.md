
# CLAUDE

> **Documentation phase closed.** This file is complete as of the README work below. At the
> candidate's direction, it will not be updated automatically in later sessions.

## Version 8 &mdash; README and assets, 2026-10-11

Presentation-layer work only. The learner-facing application was not modified: `public/index.html`
is byte-identical to the version tested under Version 7.

| Check | Result |
|---|---|
| Every relative image and link path resolves | 18 of 18, no broken references |
| No `<style>`, `<script>`, `class`, `id`, inline `style`, inline `<svg>` or event handlers | Pass |
| All HTML tags used are GitHub-allowed | Pass |
| Alternative text on every image | 11 of 11, all descriptive rather than a filename |
| Light and dark variants on every `<picture>` | 4 of 4 |
| Rendered at 1100px, light theme | Pass, screenshotted and reviewed |
| Rendered at 1100px, dark theme with `prefers-color-scheme` emulated | Pass, dark asset variants confirmed swapping |
| Rendered at 390px | Pass, horizontal overflow measured at 0 |
| Total asset weight | 876 KB across 18 files; largest single asset is the 133 KB GIF |
| Animated content has a static alternative | Yes, behind a disclosure |
| README assets excluded from the deploy directory | Yes, `docs/` sits outside `public/` |

The rendering checks used a local CommonMark-ish renderer plus headless Chromium, which approximates
GitHub but is not GitHub. Markdown nested inside HTML blocks was rewritten as explicit HTML so the
result does not depend on that approximation being exact.

---

## Version 7 &mdash; Design Lens and release, 2026-10-11

### Design Lens

All checks below are source-level or browser-rendered in headless Chromium. No assistive technology
was used.

| Check | Desktop 1280&times;900 | Phone 360&times;740 |
|---|---|---|
| Off by default: no marks, no outlines, no body class | Pass | Pass |
| Toggle on sets `aria-pressed`, shows the disclaimer, adds markers | Pass | Pass |
| Markers carry their own accessible name | Pass | Pass |
| Mouse hover shows the explanation and highlights the area | Pass | Pass |
| Keyboard focus on the marker shows it; blur hides it | Pass | Pass |
| Touch or click on the marker shows it | Pass | Pass |
| Escape hides the panel | Pass | Pass |
| Panel never covers the area it describes | Pass | Pass, area scrolled clear |
| Panel stays inside the viewport and clear of the navigation | Pass | Pass |
| Nothing is outlined until hovered or focused | Pass | Pass |
| Highlighting does not repaint the element's own background | Pass | Pass |
| Annotations follow the current screen | 2 to 7 per screen | 2 to 7 per screen |
| Nothing is marked where no reason is recorded | Pass | Pass |
| Toggling off removes every marker, attribute and inline style | Pass | Pass |
| Learner controls still work while the lens is on | Pass | Pass |
| Page-level horizontal overflow, all ten screens, lens on | 0 | 0 at 360 and 320 |
| Reduced motion: markers and panel work, animations at 1ms | Pass | Pass |
| Design Lens does not appear in the printout | Pass | Pass |

The layout sweep with the lens on reports its markers as parent overflow, because each marker
deliberately overhangs its corner by 11px into existing padding. Page-level overflow is zero at
every screen and width, no elements overlap, and the same sweep with the lens off is completely
clean at 1280, 853, 640, 360 and 320px.

### Regression after Design Lens

- Complete ten-screen journey run twice, once with the lens off and once with it on, at desktop and
  phone widths. Identical results. No errors, no duplicate ids, no inert controls.
- Data unchanged: total 58,130, mean 4,844, mean without week 7 4,953, median 4,920, and all twelve
  scrap estimates (101, 98, 107, 94, 115, 90, 142, 102, 99, 97, 117, 134).
- Print: three A4 pages, the three note sections present and in order, and no Design Lens content.
- Layout sweep with the lens off: clean at all five widths including 150% and 200% zoom.

### Release checks

| Check | Result |
|---|---|
| Single file, no dependencies | Pass: zero external script, stylesheet or import references |
| `public/` contains only the application | Pass: `index.html` and nothing else |
| Private material reachable from the deploy root | No: serving `public/` returns 404 for the brief, the project notes and every Admin file |
| Debug statements, TODOs, placeholders | None |
| No AI product named in the activity | Pass |
| Design Lens off by default | Pass |

### Still not tested, after everything

- **No screen reader or assistive technology testing, on any version, by anyone.** This now also
  covers Design Lens: its markers, labels and live region were verified programmatically only.
- Design Lens has not been opened by hand in Firefox or Safari, or on a real phone.
- No testing with anyone from the intended audience.

---

## Version 6 &mdash; second audit round and release preparation, 2026-10-11

### Version checked before any change

The regression report describes 1,666 lines and 87,456 bytes; the working file matched both exactly.
The brief hash it quotes matched this repository's brief. Both reviews therefore applied to the
current build.

### A caching fault in my own harness

The first verification run after these edits reported every correction as missing. The file on disk
and the file served by the local server were both correct: headless Chromium had cached the page
across two edits made inside the same second. All three harness scripts now append a cache-busting
query and launch with caching disabled. Every result below was produced after that fix.

### Corrections verified

| Item | Verification | Result |
|---|---|---|
| REG-001 | Clicking the already-selected "Include week 7" leaves the gate closed and Continue disabled | Pass |
| REG-001 | Selecting "Leave week 7 out" opens the gate and the mean line moves to 4,953 | Pass |
| REG-001 | Returning to "Include week 7" keeps the gate open and the mean returns to 4,844 | Pass |
| REG-001 | Hint names the control to use | Pass |
| Spoken scrap wording | Announcement reads "gives an estimated 134 parts, on the assumption stated above" | Pass |
| F-01 examples | Zero example buttons remain; three read-only list items per gap | Pass |
| F-01 prompt | Finishing with all three gaps empty stays on the screen and shows the prompt | Pass |
| F-01 prompt | A second Continue proceeds; the explicit skip button also proceeds and records the choice | Pass |
| F-01 prompt | Writing in any gap bypasses the prompt entirely | Pass |
| F-01 printout | Three labelled sections: "Written by me", "What I did in the activity", "Supplied with the activity, for reference" | Pass |
| F-01 printout | Supplied section states it is not the learner's own work; a blank note prints as a choice, not an omission | Pass |
| F-02 | Column tinted, bar ringed in focus colour, single outline, and it beats the dashed picking outline | Pass |
| F-02 | No `overflow:hidden` ancestor above any bar: the claimed clipping does not occur | Confirmed not a defect |
| F-03 | `aria-expanded` present and correct in both states, with `aria-controls` | Pass |
| F-04 | Hint, edge shadow and keyboard-reachable region appear only on tables that actually overflow | Pass |
| F-04 | No hints at desktop width; no duplicates after repeated redraws; stage 8's split tables need none | Pass |
| F-05 | "7 fewer calls, a drop of about a third" | Pass |
| F-06 | Task strip names the navigation control; still zero in-page buttons on that screen | Pass as decided |
| F-07 | Confetti retained, still suppressed under reduced motion | Pass as decided |

### Regression

- Complete ten-screen journey at 1280&times;900 and 360&times;740, including the matching task, the
  investigation gate, both challenges, all three comparison views, the average, all three column
  reveals, both linked scrap charts and the written note. No errors, no duplicate ids, no inert
  controls, no horizontal overflow.
- Back through all ten screens and forward again without redoing anything: every answer preserved.
- All ten screens re-rendered individually without error.
- Data integrity: 12 rows, total 58,130, mean 4,844, mean without week 7 4,953, median 4,920 from
  4,910 and 4,930, target 5,000, and all twelve scrap estimates unchanged
  (101, 98, 107, 94, 115, 90, 142, 102, 99, 97, 117, 134). Both supervisor notes verbatim.
- Trend arrows unchanged: week 8 none, weeks 9 and 10 all down, week 11 down/down/up, week 12
  none/down/up.
- The deliberately misleading charts still behave as designed, including the clipped week 7 stub.
- Layout swept at 1280&times;900, 853&times;640 (150% zoom), 640&times;480 (200% zoom), 360&times;740
  and 320&times;650: no clipped text, no overlaps, no horizontal overflow, nothing under the fixed
  navigation.
- Reduced motion: confetti not created, animations and transitions at 1ms, and the keyboard focus
  ring still renders (it is state, not decoration).
- Print: three A4 pages. The three card sections print in order, the figures table is complete and
  correct, and the navigation, confetti and action buttons are absent. The third page carries the
  table alone, which is tidy but not dense; no content is lost or clipped.
- No AI product named anywhere; no em dash anywhere in the rendered page.

### Release preparation

| Check | Result |
|---|---|
| Runs as a single file with no dependencies | Pass: zero script, stylesheet or `@import` references |
| Runs from `file://` with no server | Pass |
| Private material reachable from the deploy root | **No.** The application moved to `public/index.html`. Serving `public/` and requesting the brief, the project notes and the Admin files returns 404 for each |
| Debugging statements, TODOs, placeholders | None. The only two matches for "brief" are source comments |
| Dead code | Removed the CSS for the example buttons that F-01 deleted |
| README | Written from empty: what the activity is, how to run it locally and hosted, an explicit warning to publish `public/` only, the repository layout, the accessibility position including what is not verified, and a statement that the data is unaltered and the company fictional |

### Outstanding after this pass

- **No screen reader or assistive technology testing has been carried out by anyone, on any
  version.** The `aria-expanded`, live region, focus and table-region work added here was verified
  programmatically, which is not the same as listening to it.
- Firefox and Safari have not been retested since these corrections. The candidate tested across
  browsers at version 4.
- No testing with anyone from the intended audience, so Gemini's suggestion that the activity may
  run long for less confident learners is unmeasured either way.
- The deploy directory is correct, but the host's output directory must still be set to `public`
  at deployment time. That is a configuration step, not something the repository can enforce.

---

## Version 5 &mdash; independent audit correction pass, 2026-10-11

### What kind of testing each result came from

Three different things are reported below and they are not interchangeable:

- **Source-level tests.** The application's own JavaScript executed in headless Chromium with the
  real DOM, state driven directly, assertions on generated output.
- **Browser tests.** The same engine rendering the page, with geometry measured from the rendered
  result, plus print rendered to PDF. Earlier in this session the candidate's own Chrome was driven
  through the browser extension; it disconnected part way through this pass, so the post-correction
  visual checks were run in headless Chromium instead. Same rendering engine, not the same browser
  install, and not Firefox or Safari.
- **Not tested.** Screen readers and other assistive technology, real phones and tablets, Firefox,
  Safari, and printing on a physical printer.

The independent audit's 320 assertions were a Node harness with a stubbed DOM. They are source-level
evidence only and are not counted as browser testing here.

### Version check

The audit quotes SHA-256 `bd8ee199…0280d6`. The working file hashed identically, so every finding
applied to the current code.

### Each finding re-verified after the corrections

Source-level unless marked otherwise.

| Finding | Verification | Result |
|---|---|---|
| DATA-001 | Assumption panel present and positioned above the charts on first render, before any estimate | Pass (browser geometry) |
| DATA-001 | First selection of any week reads "an estimated N parts" | Pass |
| DATA-001 | Chart titles read "Scrap percentage, as recorded on the sheet" and "Estimated scrap parts" | Pass |
| DATA-001 | Table headers read "Estimated scrap parts" in all three tables that carry the column | Pass |
| DATA-001 | No "differ slightly" claim anywhere; the rounding caveat is present | Pass |
| DATA-001 | Weeks 7 and 12 comparison is conditional on the stated assumption | Pass |
| DATA-001 | Weeks 5 and 11 comparison states the estimates could fall either way | Pass |
| DATA-001 | Estimates still arithmetically correct: 101, 115, 142, 117, 134 | Pass |
| DATA-002 | Screen, spoken feedback and printout all describe the sort and the two middle figures | Pass |
| DATA-002 | No week in the data equals 4,920 | Pass |
| DATA-002 | 4,910 and 4,930 derived from the sorted data, not typed | Pass |
| DATA-003 | Week 5 + "no", week 5 + "yes", week 7 + "no", week 1 + "yes", and no answer at all | Pass, all five |
| DATA-004 | Corrected starter offered, and reproduced in the printed note | Pass |
| DATA-005 | Arrows across weeks 8 to 12: week 8 none, weeks 9 and 10 all down, week 11 down/down/up, week 12 none/down/up | Pass |
| DATA-005 | Caption states the comparison basis | Pass (browser) |
| DATA-006 | Answer labels and the shared feedback no longer treat the note as a full account | Pass |
| DATA-007 | Rank wording no longer contradicts the table | Pass |
| DATA-008 | Welcome screen says example figures, not a real quarter | Pass |
| INFO-001 | The stub is identified as not being week 7's value, pointing to the table | Pass |
| INFO-002 | Comparison counter starts at 1 of 3; average screen gated on one toggle | Pass |
| INFO-003 | Invented workplace history removed | Pass |

### Data integrity after the corrections

- All 12 rows and all 60 measure cells re-parsed from the candidate brief's Word document and
  compared with the code: **no mismatches**. Target still stored once as 5,000.
- Both supervisor notes still quoted verbatim.
- Total 58,130; mean 4,844; mean without week 7 4,953; median 4,920 from 4,910 and 4,930.
- Scrap estimates unchanged for every week: 101, 98, 107, 94, 115, 90, 142, 102, 99, 97, 117, 134.
- No calculation was changed. Only the words around them.

### Regression

- Full walkthrough of all ten screens end to end, plus awkward click orders, back through every
  screen and forward again. No errors, no duplicate ids, no inert controls, state preserved.
- All ten screens re-rendered individually without error.
- The deliberately misleading charts still behave as designed, including the clipped week 7 stub.
- Layout swept at 1280&times;900, 853&times;640 (150% zoom), 640&times;480 (200% zoom), 360&times;740
  and 320&times;650: no clipped text, no overlapping elements, no horizontal overflow, and nothing
  sitting under the fixed navigation on any screen. (Browser geometry.)
- Print rendered to A4 PDF: two pages. The investigated week and the week 7 decision appear as
  separate records, the median line reads correctly, and the scrap line no longer claims parts were
  actually scrapped. A print rule was added so a term is not orphaned from its text at the page
  break. (Browser rendering, not a physical printer.)
- No AI product named anywhere; no em dash anywhere in the rendered page.

### Outstanding after this pass

- **No screen reader or assistive technology testing has been carried out by anyone.** The structural
  work is unchanged and still verified programmatically, which is not the same thing.
- Firefox and Safari have not been retested since these corrections; the candidate tested version 4
  across browsers before the audit.
- No testing with anyone from the intended audience.
- The scrap figures remain estimates by design. The activity now states the assumption before use
  rather than resolving it, because the brief does not define the denominator.

---

## Version 4 &mdash; final refinements, 2026-10-11

### Manual testing by the candidate (version 3)

Tested across devices and browsers with no issues found. Screen reader testing was again not
possible, so it remains outstanding.

### Method

The visual review was run in the candidate's own Chrome through the browser extension, screen by
screen and state by state, with the headless harness used for the checks that need repeating at
several viewport sizes.

### Issues found and fixed

1. **A tooltip hung 70px outside its chart.** On the last bar of a twelve bar chart the tooltip was
   centred on the bar with no horizontal limit, so it extended past the plot's right edge. It is now
   measured and clamped inside the plot. Verified on the first, middle and last bar of both linked
   charts: the worst case is now 1px.
2. **Match badges outgrew their column on narrow screens.** "Example" needed 62px in a 43px slot at
   360px wide, and at 320px the week numbers overflowed too. Badges now carry a short form ("Ex",
   "A", "B", "C") that is used below 760px, and the chart gutter is tightened below 400px.
3. **Opening the table on the matching step pushed the feedback below it.** Showing the sheet by
   default was the right call, but inside the chart component it separated the learner's action from
   its response by six table rows. The table moved to full width underneath the activity, which also
   fixed it being clipped by a narrower grid track.
4. **Two identical Start buttons were visible at once** on the new welcome screen, one in the page
   and one in the fixed navigation. The navigation is hidden on that screen.
5. **The scrap step's instruction did not match its completion logic.** It asked for weeks 7 and 12
   but accepted any two weeks. The logic now requires both, and both the task line and the
   navigation hint name whichever is still missing.

### Checks run

| Check | Result |
|---|---|
| Clipped text in buttons, tasks, chart titles, legends, badges, captions, headers and bar labels | None, at 320, 360, 540, 853, 1280 and 1440px |
| Overlapping task strips, buttons, panels, slots, legends, badges and the average label | None, at every width |
| Horizontal overflow | None, at every width |
| Fixed navigation obscuring content, all ten screens | Nothing underneath it, at 1280&times;900, 1440&times;760, 853&times;640 (150% zoom) and 640&times;480 (200% zoom) |
| Tooltip containment, first, middle and last bar of both linked charts | Within 1px of the plot edge |
| Duplicate element ids, and focusable controls with no handler | None, on every screen |

Zoom was tested by emulating the viewport a given zoom level produces: 853&times;640 is 150% of a
1280&times;960 window, and 640&times;480 is 200%.

### Re-verified after the changes

- **Every figure checked against the brief itself**, parsed out of the Word document rather than
  retyped. All twelve rows and both supervisor notes reproduce exactly. The derived figures are
  unchanged: average 4,844, average without week 7 4,953, typical week 4,920, and scrap in parts
  from about 90 to about 142.
- Full walkthrough with awkward click orders, including the new navigation path through challenge 2
  and the tightened scrap gate. No errors, no duplicate ids, no inert controls, all state preserved
  going back through all ten screens and forward again.
- No AI product named anywhere; no em dash anywhere in the rendered page.
- Print: two A4 pages. The completed note renders as prose with full stops. Confetti, navigation and
  both action buttons correctly absent.

---

## Version 3 &mdash; copywriting, density and layout, 2026-10-11

### Manual testing by the candidate (version 2)

Firefox, Chrome and Safari, desktop and mobile. No issues found. Screen reader testing was again not
possible, so it remains outstanding.

### Structure

Split from seven screens to ten, so each screen carries one idea:

| | Screen | Purpose |
|---|---|---|
| 1 | Line 3 and the weekly numbers | Context and the sheet, full width |
| 2 | Reading the sheet | Match three notes to weeks |
| 3 | Finding the week that stands out | Explore four measures, commit to a week, then the note |
| 4 | Making the chart tell a different story | Two challenges, one at a time |
| 5 | Comparing the two versions | Each change isolated behind its own button |
| 6 | What an average can hide | One toggle, one moving average line |
| 7 | The last five weeks | Reveal the other measures, then the week 10 context |
| 8 | Scrap as a share, and scrap as parts | Two linked charts and one calculation |
| 9 | Your note for the team meeting | The part-written document |
| 10 | Your completed notes | The printable record |

### Length

| | Total words | Prose only | Prose at 130 wpm |
|---|---|---|---|
| Version 2 | 1,808 | about 1,500 | 12 min |
| Version 3, first draft | 2,807 | 2,240 | 17 min |
| Version 3, after a tightening pass | 2,586 | 2,064 | 16 min |

"Prose only" excludes table cells, axis labels and collapsed disclosures, which are scanned rather
than read. Of the 2,064, about 260 is the printable summary, which is a take-away rather than
something read in sequence, and about 390 is the note document, which is filled in rather than read
straight through. The linear reading load is therefore closer to 1,400 words, or about 11 minutes at
a slow pace, which leaves room for roughly 35 interactions inside the 20 minute ceiling.

The tightening pass removed repetition only. No teaching point was dropped.

### Faults found and fixed in version 3

1. **The x-axis labels stopped lining up with the bars.** Capping the plot width for charts of seven
   bars or fewer left the axis row at full width, so the week numbers drifted away from the bars they
   label. This is precisely the risk the bar-width change introduced. Fixed, and a test now measures
   the centre offset between every bar and its label on every chart in the activity; the worst case
   is 1px.
2. **The target line and the average line collided** on the average screen. They sit 156 units apart
   on a 5,500 scale, about 5px, and the average legend had displaced the target legend so the dashed
   line was unlabelled. The target line is now suppressed on that screen, which also keeps it to one
   idea.
3. **Completed sentences in the printed note had no full stop**, because the learner's own text
   rarely ends with one. A full stop is now appended when the text does not already end in
   punctuation.
4. **The scrap calculation was announced twice** to a screen reader: once from the visible text and
   once from a hidden equivalent that duplicated it.
5. Mobile heights needed trimming across the board after the copy pass; charts, chart headings, axis
   notes, control labels and feedback slots were all reduced on small screens.
6. The scrap readout and its two charts overflowed a phone screen by 69px once a week was selected.
   Resolved by shortening the comparison line and the small charts.

### Layout, measured

Every stage measured at the moment the learner is operating a control, from the top of the control to
the bottom of the feedback it produces, against the height left after the sticky header and the fixed
navigation bar (783px on desktop, 616 to 628px on the phone).

Desktop, 1280&times;900: every stage fits, the largest being 630px.

Phone, 360&times;740: every control-to-chart and chart-to-feedback pair fits. The one span that does
not is the four note cards plus the chart on the matching screen, at 765px against 628px. That is
inherent to having four cards and a chart on a small screen, and is handled by scrolling the chart
into view when a note is selected. No horizontal overflow at any step, and no table scrolls
horizontally on the phone.

### Motion

Verified by emulating `prefers-reduced-motion: reduce`: the confetti is not created at all, and every
animation and transition collapses to 1ms. With motion allowed, bar growth runs at 340ms, feedback
transitions at 140ms, the task strip flash at 620ms and the completion tick at 460ms.

### Re-verified

- Every figure recomputed from the supplied data and compared against the text: unchanged and correct.
- Full walkthrough with awkward click orders: selecting and deselecting notes, clicking a week before
  picking a note, clicking a week before exploring all four measures, revealing columns out of order,
  setting the challenge controls backwards, changing a committed answer, switching between both
  decision answers, and going back through all ten screens and forward again. No errors, no duplicate
  ids, no focusable control without a handler, all state preserved.
- Focus scoping by chart id still holds with two linked charts on one screen.
- No AI product named anywhere, and no em dash anywhere in the rendered page.
- Print: two A4 pages. The completed note renders as prose with the learner's words inside the
  supplied sentences. Confetti, navigation and both action buttons correctly absent.

---

## Version 2 &mdash; interaction and layout rebuild, 2026-10-11

### Manual testing by the candidate (version 1)

Firefox and Chrome, desktop and mobile. Everything tested worked as expected. No screen reader
testing was possible for this demonstration, so that remains outstanding &mdash; see the limitations
at the end of this file.

### New: layout regression test

Every test written for version 1 reads state. The candidate's complaint about version 2's
predecessor was spatial, so a test was added that measures `getBoundingClientRect()` on the current
task, its control group, the chart and the feedback slot, and asserts they fall inside one viewport.

Results, after fixes, with no horizontal overflow at any step or either width. Each row measures
the moment the learner is operating a control, from the top of the current task or control group to
the bottom of the feedback it produces.

| Step | 1280&times;900 | 360&times;740 |
|---|---|---|
| 1 &mdash; matching: chart to feedback | 383px | 310px |
| 2 &mdash; investigate: while exploring the measures | 310px | 545px |
| 2 &mdash; investigate: at the moment of choosing a week | 313px | 575px |
| 3 &mdash; challenge: controls, chart, caption | 459px | 650px |
| 4 &mdash; columns: task, control, feedback | 293px | 383px |
| 4 &mdash; scrap: task to linked-chart readout | 429px | 536px |
| 5 &mdash; writing: a field with its starters | 257px | 278px |

Usable height after the sticky header and the fixed nav bar is 783px on desktop and 629px on the
phone. One state exceeds it: challenge 1 on a 360px phone with the caption wrapped to three lines,
at 650px, so about 20px of scroll. Everything else fits with room.

The end state of a stage, once the learner has finished operating it and is reading a conclusion,
is longer than these figures &mdash; stage 2 fully revealed runs to about 1,040px on a phone. That
is a page to read rather than a control-and-response loop, so it is not held to the same measure.

### Faults found and fixed in version 2

1. **A grid overflow made the whole page shrink-to-fit on a phone.** Grid children default to
   `min-width:auto` and would not shrink below a `white-space:nowrap` table, so Chrome zoomed the
   entire page out to 553 CSS pixels. Every mobile measurement taken before this was fixed was
   meaningless. Fixed with `min-width:0` on grid children.
2. **Completed column buttons were white text on a pale green background.** A revealed column
   carries both `aria-pressed="true"` and `disabled`; the pressed rule was painting the text white
   while the disabled rule repainted the background pale green.
3. **The weeks 8&ndash;12 table was clipped** by a grid track too narrow for five columns.
4. **Solving challenge 2 skipped its own win feedback** and jumped straight to the side-by-side
   comparison, because the comparison was gated on both challenges being complete rather than on the
   learner asking to see it.
5. **Duplicate `plot` element id** on the side-by-side view, where two charts both took the default.
6. Both challenges announced "Challenge done." rather than naming which one.
7. A CSS selector meant to compact small charts never matched, because the class it targeted sits on
   an element with no sibling of the type the selector expected.
8. The mobile reorder that puts the reference sheet above the writing was applied to every stage,
   which pushed the chart above the controls everywhere. Scoped to the one stage that wants it.
9. The 12-week scrap table duplicated what the two linked charts already showed; collapsed into a
   disclosure so it remains the charts' table twin without lengthening the page.
10. **Focus landed on the wrong chart.** The two linked scrap charts carry identical `data-week`
    values, and focus restoration used an unscoped selector, so clicking a week in the right-hand
    parts chart returned focus to the same week in the left-hand percentage chart. State was correct
    either way, so only a keyboard user would have hit it. Selectors are now scoped by chart id, and
    the test was changed to report which chart holds focus rather than only which week.
11. **Stage 4 asserted something it no longer showed.** The stage opens by saying weeks 10, 11 and 12
    all beat target, but the rebuilt table had no target column. Restored, so the learner can check
    the claim rather than take it on trust &mdash; on the one stage that is about not taking claims
    on trust.
12. A tooltip on a near-full-height bar rendered above the plot and over the chart title. It now
    flips inside the bar when there is no room above it.

### Re-verified after the rebuild

- All arithmetic re-checked against the supplied figures: unchanged and correct.
- Full walkthrough with deliberately awkward click orders: selecting and deselecting notes, clicking
  a week before picking a note, clicking a week before exploring the measures, revealing columns out
  of order, setting the challenge controls backwards, changing a committed answer, clicking a chip
  twice, going back through all seven screens and forward again. No errors, no duplicate ids, no
  focusable control without a handler, and all state preserved.
- Focus restoration and the live region: every interaction on all seven screens still returns focus
  to the control used and announces the right text.
- Reduced motion: emulated `prefers-reduced-motion: reduce` and confirmed confetti is not created at
  all, and transitions and animations collapse to 1ms.
- Print: regenerated the A4 PDF. Two pages, confetti and both action buttons correctly absent.
- Length: 1,808 words, down from 2,073, with more interaction rather than less content.

### The new investigation stage

The rebuilt step 3 rests on a property of the supplied data that was verified before it was written:
every measure ranks weeks 1&ndash;7 in almost the same order (identical on three of the four), and
week 5 is second worst on all four. So "week 7 is worst at everything" is true but is not what makes
it the story &mdash; week 5 is bad at everything too. The gap is: week 5 is 40 units below week 1,
week 7 is 1,130 below week 5.

---

## Version 1 &mdash; first build, 2026-10-11

## Method

No manual browser testing had been done at this point. The Chrome extension was not connected, so
testing was automated: headless Chromium driven over the Chrome DevTools Protocol, with the file
served from a local HTTP server. Two scripted walkthroughs, one at desktop width and one at an
emulated 360&times;740 phone viewport, plus a separate arithmetic check of every figure the activity
states on screen.

Scripts are in the session scratchpad and are not part of the deliverable. **This does not replace
testing by hand on real devices** &mdash; see "Still to do" below.

## Arithmetic check

Every figure the activity asserts was recomputed from the supplied data and compared against the
text. All passed.

| Claim on screen | Checked |
|---|---|
| Mean 4,844 / mean without week 7 4,953 / middle week 4,920 | 4844.17, 4952.73, 4920 |
| "Averaging under 4,850" is true | true |
| Scrap in parts: week 7 ~142, week 12 ~134, week 11 ~117, week 5 ~115 | 142, 134, 117, 115 |
| Week 11 has a lower scrap % than week 5 but more parts | 2.3% / 117 against 2.4% / 115 |
| Week 7 is worst on all four measures | true |
| Weeks 10, 11, 12 all beat target | true |
| 2.6% is the highest scrap of any week except week 7 | true |
| Stage 1 note A (180 short) matches exactly one week in 1&ndash;6 | week 1 only |
| Stage 1 note B (fewest units and most downtime) matches exactly one week | week 5 only |
| Stage 1 note C (10 short and least scrap) matches exactly one week | week 6 only |
| Worked example: week 3 is 130 short with 13 hours down | true |
| No bar height exceeds 100% or goes negative on any measure or scale | true |

## Walkthrough

Full click-through of all seven screens: every stage gated and ungated correctly, every piece of
feedback fired, no JavaScript errors, no duplicate element IDs on any screen.

Unexpected orders and awkward paths checked:

- Clicking a week in stage 1 with no note selected &mdash; returns that week's figures rather than failing silently.
- Three wrong matches in a row &mdash; triggers the pointer to the table view.
- Revealing stage 4 columns in a different order (scrap first) &mdash; feedback still correct, order recorded correctly on the summary card.
- Stage 3 controls set in the wrong order (week range before scale) &mdash; nudge text adapts.
- Backwards through every screen and forwards again &mdash; all answers preserved: matched notes, selected week, read notes, both solved tasks, revealed columns, parts view, typed text.
- Changing a stage 3 control after both tasks are solved &mdash; tasks stay solved, caption updates.
- Leaving a stage 5 field blank &mdash; the blank stem is omitted from the summary card rather than printed empty.
- Clicking a chip twice &mdash; appends rather than overwrites.

## Accessibility

| Check | Result |
|---|---|
| Bars that respond to clicks are real `<button>` elements | pass |
| Bars that do nothing are not focusable | **failed, then fixed** &mdash; stages 3 and 4 rendered 12 and 17 focusable buttons with no handler |
| Accessible name on each interactive bar | pass, e.g. "Week 7, 3,650 units, target 5,000" |
| Static charts carry `role="img"` and point to the table | pass |
| Control groups have `role="group"` and a resolvable `aria-labelledby` | pass |
| Table row headers carry `scope="row"` | pass |
| Live region on every feedback area | **failed, then fixed** &mdash; see below |
| Minimum control height | 48px |
| Interactive bar hit area | full column height (192px), independent of bar height |
| `lang` attribute | `en-AU` |
| Colour never the only signal | pass &mdash; matched notes carry a week number and a tick, selected bars carry `aria-pressed` and an inset outline |
| Text contrast on completed items | **failed, then fixed** &mdash; disabled buttons greyed out their own text |
| Feedback is actually announced | **failed, then fixed** &mdash; verified by reading the live region after each interaction |
| Focus survives a re-render | **failed, then fixed** &mdash; verified by reading `document.activeElement` after each interaction |
| No AI product named anywhere | pass |

## Print

The summary card was rendered to A4 PDF through the same headless browser. Two pages: the card and
its sentences on page 1, the twelve supplied rows on page 2. No blank leading page. The navigation,
header and "Start again" button are correctly suppressed. The first attempt orphaned the table header
at the foot of page 1; fixed.

## Length

Measured at 2,062 words with every stage fully revealed. That is roughly 16 minutes of reading at a
slow pace and 11 at a brisk one, before interaction time, though about 310 of those words are the
summary card and data table, which are scanned rather than read. The on-screen estimate was changed
from "about 15 minutes" to "about 15 to 20 minutes" to match. The brief allows 10&ndash;20 minutes, so
a slow reader sits at the top of that range. A prose-tightening pass recovered only 64 words, so the
length is structural: cutting further would mean dropping a teaching point, which is a content
decision rather than an editing one.

## Mobile, 360&times;740 emulated

No horizontal page overflow on any of the seven screens, including with every data table expanded.
Control groups wrap to two rows. The side-by-side comparison in stage 3 stacks. Chips wrap. Text
areas fit the column.

One compromise: at 360px the twelve bars are about 24px wide each. The hit area is the full column
height so the target is large vertically, and those charts are not clickable anyway, but the bars
themselves are narrow. The table toggle is the fallback.

## Faults found and fixed

1. Stages 3 and 4 rendered bar `<button>` elements with no click handler &mdash; focusable controls that did nothing. Now rendered as `<div>` with `role="img"` on the chart.
2. Completed match cards and revealed column buttons greyed out their own text, well below readable contrast. Disabled here means "already done", so the text colour is now preserved.
3. The disabled Continue button was too faint to read (about 2.4:1). Darkened.
4. Stage 1's chart could not answer its own question &mdash; from a zero baseline, six weeks within 210 units of each other are visually identical, so "our lowest week so far" was unfindable on the chart. Values are now printed on the bars where they fit and the scale is honest.
5. Same problem on the weeks 8&ndash;12 chart: "weeks 10, 11 and 12 all beat target" was not visible. Values added.
6. Dead empty readout paragraphs on two stages, left over from an earlier layout.
7. Stage 2 could be passed after viewing only one extra measure, when the text claims the learner checked several. Gate raised to three.
8. The closing takeaway was outside the printable card and marked `noprint`, so it would not have appeared on the printout. Moved inside.
9. **The selected-bar outline drew around the whole column**, including the empty space above a short bar, which looked like a rendering fault. The marker now sits on the bar.
10. **None of the feedback would have been announced to a screen reader.** The live regions existed, which is what the structural check saw, but `draw()` replaces the whole panel, and a freshly inserted region that already contains text does not fire. Every piece of teaching feedback on stages 2 and 4 would have been silent. Fixed with one persistent visually-hidden region outside the panel that every handler writes to.
11. **Focus fell to `<body>` after every interaction.** Stage 1 takes six interactions and stage 4 takes five, so a keyboard user would have re-tabbed from the top of the document eleven times. The earlier tab-order check read DOM order, which did not catch it. `draw()` now restores focus to the control that was used, moves to the next undone control when that one becomes disabled, and lands on the new heading on a stage change.
12. HTML entities were stripped out of the announced text, so "5,000 &minus; 4,820" was read aloud as "5,000 4,820". Entities now map to words.
13. The printed figures table orphaned its header row at the foot of page 1. Print break rules added.

## Still to do

- **Real devices and real browsers.** The candidate tested version 1 in Firefox and Chrome, and version 2 in Firefox, Chrome and Safari, on desktop and mobile, with no issues found. Version 3 has not been opened by hand. iOS Safari and Android Chrome remain untested on real hardware.
- **Real screen reader, the largest outstanding limitation.** No screen reader testing has been carried out by anyone, and none has been possible for this demonstration, across any version. What has been verified is structural and programmatic: the live region receives the correct text after every interaction, focus lands on the right control after every re-render, every interactive bar has an accessible name, static charts carry `role="img"` and point to a table twin, and control groups resolve their `aria-labelledby`. None of that is the same as listening to it. NVDA or VoiceOver remains the test that counts, particularly whether announcements interrupt one another on the stages that now announce more, and whether the two linked scrap charts read sensibly as a pair.
- **Keyboard-only run by a person.** Focus is now restored programmatically and verified after every interaction on all seven screens, but nobody has driven it by hand.
- **Someone from the actual audience.** None of the above tells us whether the language is plain enough or the tasks make sense to a machine operator.

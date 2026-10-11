
# CLAUDE

Decisions recorded as they were made during the build on 2026-10-11. Candidate decisions are
marked as such; everything else was an assistant decision taken under the brief and the project
notes, and is open to being overridden.

## Scope

| Decision | Reason |
|---|---|
| Single `index.html`, no libraries, no build step, no backend | Brief asks for a standalone browser interactive and 1&ndash;3 hours of effort. Nothing here needs a dependency. |
| No saved progress, no accounts | Candidate decision. The brief names shared computers; saved answers would be visible to the next worker. A visible "Start again from the beginning" covers restarts. |
| Help wizard dropped | Candidate decision for this demo, noted as a possible future addition. For low-confidence users a wizard is an extra interface to learn before starting, and it was the most expensive item in the project notes. |
| Seven screens, ~15 minutes | Brief specifies 10&ndash;20 minutes. |

## Learning design

| Decision | Reason |
|---|---|
| Activity walks forward in time (weeks 1&ndash;6, then week 7 arrives, then the full quarter) | Removes the artificiality of hiding data from the learner. Week 7 arriving is an event rather than a withheld answer, and it gives the week-range control in stage 3 a narrative meaning. |
| No multiple-choice items anywhere | Candidate requirement, and the brief requires more than a quiz. Each stage uses a different manipulation: matching, measure switching, control state, column choice, sentence completion. |
| Stage 1 is a matching task, not a reading task | Candidate request. Matching a plain-words note to a week forces reading across two columns and doing the comparison, rather than copying a figure out of a cell. |
| Stage 3 asks the learner to build the misleading chart | Watching a chart mislead teaches less than causing it. Control state is also the hardest answer in the activity to produce by accident. |
| Stage 3 uses nudges, not a pass/fail gate | Each nudge names what the current setting is already doing, so a partly-correct attempt teaches. Candidate asked that the stage explain *why* the presentations mislead, not just permit the manipulation. |
| Stage 4 reveals columns one at a time | Choosing which evidence to look at is learning outcome 3 performed rather than described. The order is recorded and reflected back on the summary card. |
| Stage 5 uses sentence stems with unfinished fragments | Candidate request for structure over a blank box. Fragments stop before the point ("how many hours&hellip;") so they scaffold rather than supply an answer. |
| One free-text stage only, at the end | Three typing tasks is a lot for a time-poor learner on a phone. Typing only happens where it produces the take-away card. |
| Feedback explains reasoning for wrong answers using that week's own figures | Project notes. A wrong match returns the figures for the week that was clicked, so a mistake still teaches the table. |
| No causal claims about weeks 10&ndash;12 | Project notes, and it is the pedagogical point. The activity states that three things changed at once and that the sheet cannot separate them. |

## Technical

| Decision | Reason |
|---|---|
| Bars are HTML `<button>` elements with CSS heights, not SVG | Native focus, keyboard and touch behaviour for free, and less code than an accessible SVG chart would need. |
| Bars are rendered as `<div>` where clicking does nothing (stages 3, 4) | A focusable control that does nothing is worse than no control. Those charts carry `role="img"` and point to the table instead. Found during testing; see testing-results.md. |
| Value printed on the bar when the scale starts at zero and there are 7 bars or fewer | From zero, weeks that differ by 3% are visually identical, so the chart could not answer the question being asked of it. Suppressed on the 12-week charts (no room) and on the truncated-scale chart (bars too short, and the distortion is the point). Found during testing. |
| Every measure carries its own direction label | Units is good-high; downtime, fault calls and scrap are good-low. A bar chart where tall means good on one measure and bad on the next would mis-train the reader. |
| Stage 2's axis is locked to zero | A learner stumbling onto a truncated scale before stage 3 names it would spend the reveal. |
| Every chart has a "Show these numbers as a table" toggle | Accessibility, and the table is genuinely better for the comparisons stage 1 asks for. |
| Averages and scrap-in-parts computed from the data at runtime, never hardcoded | The figures cannot drift from the supplied data if they are derived from it. |
| Single `DATA` array as the only source of truth | Project notes. Charts, tables, feedback strings and the summary card all read from it. |
| One persistent visually-hidden live region outside the panel | The panel is replaced on every redraw, and a newly inserted live region that already holds text is not announced. Every handler writes the spoken copy of its feedback there. Found during testing. |
| `draw()` restores focus to the control that was used | Without it, focus drops to `<body>` after every interaction &mdash; eleven times across stages 1 and 4. Where the control has just become disabled, focus moves to the next undone one; on a stage change it lands on the new heading. Found during testing. |

## Data handling

The twelve rows and both supervisor notes are reproduced exactly as supplied. No figure is altered.

Two derived presentations are used, both shown with their arithmetic on screen so the learner can see
where the number came from:

- **Averages.** 4,844 across all twelve weeks, 4,953 with week 7 removed, 4,920 for the middle week.
- **Scrap in parts.** Units produced &times; scrap %, rounded, and labelled "about". The brief does not
  say whether "units produced" is counted before or after scrap is removed, so the figures are described
  as approximate and that ambiguity is offered to the learner as something worth asking about.

## Version 2 &mdash; interaction and layout

| Decision | Reason |
|---|---|
| Fixed feedback slot per stage, sized even when empty | The candidate's main complaint was clicking, scrolling down to read a result, then scrolling back. A reserved slot next to the control means the result appears where the learner is already looking, and nothing shifts when it fills |
| Controls and chart side by side above 860px | Puts the thing you click and the thing that changes in the same glance. Single column below that, with the chart scrolled into view when a note is selected |
| One challenge at a time on the two-stories stage | The two tasks were previously below the chart and could be completed by accident while experimenting. The current challenge is now the first thing on the stage, and completing it replaces it rather than adding below it |
| Investigation before explanation on the week 7 stage | Candidate request. The learner explores all four measures, commits to a week, and only then is anything explained. The explanation is the one the data supports: every measure ranks the weeks almost identically and week 5 is second worst on all four, so being worst is not the story &mdash; the size of the gap is |
| An explicit reconsider step after the supervisor's note | Candidate request. Two defensible answers, both given reasoning, so it reads as a judgement rather than a test |
| Two linked scrap charts instead of a percentage/parts toggle | Candidate asked for the difference to be more visually obvious. Clicking a week highlights it in both charts and shows the share and the parts count in one sentence |
| Revealed columns highlight in place, with trend colours and a rule at week 10 | The significance was previously carried by a paragraph underneath. It is now in the table the learner just changed |
| The data sheet travels to the writing stage | Candidate spotted that learners were being asked to write about figures they could no longer see. Beside the writing on desktop, above it and collapsed on a phone |
| Progress dots instead of "Step 3 of 7" text | Gives a sense of distance at a glance; the text label is kept for wide screens and the accessible name always states the step |
| Gridlines, y-axis ticks, and the target as a legend above the plot | From the `dataviz` skill. The target label was previously inside the plot and became unreadable when the scale started at 4,600, which the candidate flagged |
| Tooltips on the twelve-bar charts only | Labels carry the charts of seven bars or fewer; tooltips carry the ones where labels do not fit. Keyboard focus shows the same content as hover |
| Week 7 clips quietly at the 4,600 baseline, and is explained afterwards | A silently clipped bar is a worse deception than a truncated axis, and worth teaching. Marking it loudly during the challenge would defuse the deception the learner is being asked to build |
| Motion: 140ms feedback, 220ms state, 320ms reveal, `cubic-bezier(0.16,1,0.3,1)` | From the `impeccable` motion guidance for Operate-mode surfaces. All of it behind `prefers-reduced-motion`, which also suppresses the confetti entirely |
| The render model was left alone | The first plan was to update slots individually rather than re-render the panel. Focus restoration and the live region are both built on the whole-panel re-render and were verified empirically; the complaint was about layout, not rendering |

## Version 3 &mdash; copywriting, density and layout

| Decision | Reason |
|---|---|
| Ten screens, one idea each | Candidate asked for density to come down and was willing to add screens. The two-stories stage became three and the good-news stage became two. Each screen now has a single purpose that can be named in its heading |
| Register rewritten throughout | Candidate asked for complete, natural sentences, professional but not overly formal, and for feedback that does not assume what the learner should do. Headings became statements rather than captions, and both answers to the week 7 decision now share one response |
| No em dashes | Candidate request. Verified in the source and in the rendered text |
| Each chart manipulation isolated behind its own button | Candidate wanted learners to understand the two methods rather than remember which buttons they pressed. Switching between the honest chart, the cut scale and the hidden weeks shows each change on its own, with the bars animating between states |
| Bars grow from the baseline when the data changes | The strongest available signal that switching a control changed the data rather than the page. Replayed only when the measure, scale or week range actually changes, not on every unrelated redraw |
| Bar width capped at 42px | From the `dataviz` mark specs. At full width a twelve bar chart gives 78px slots, and filling them produces exactly the heavy blocks the skill warns about. The clickable area stays the full column |
| Target line suppressed on the average screen | It sits 156 units from the average line, about 5px, and the average legend displaced its label. One idea per screen |
| Match badges moved below the axis | Candidate reported the target line overlapping the A, B and C labels above the bars. Below the axis, no chart line can cross them |
| Reference data under the note at full width, with jump links | Candidate disliked the collapsible panel. Three narrower tables on small screens rather than one wide one |
| The printed note renders as prose | The learner's words now sit inside the supplied sentences, so the output reads as a workplace note rather than three answers |

## Version 4 &mdash; final refinements

| Decision | Reason |
|---|---|
| A welcome screen rather than a first activity screen | Candidate request. It covers what the activity is about, what the learner will do, what they should get out of it, and how long it takes, so the resource reads as complete rather than opening part way in |
| The weekly figures moved off the welcome screen | A landing page that opens with a data table is not an introduction. The sheet now appears on the matching step, where the notes actually require downtime and scrap, at full width underneath the activity |
| Activity navigation hidden on the welcome screen | With a prominent start block on the page and a Start button in the fixed bar, two identical buttons were on screen at once. It also removes a Back button that could never be used |
| Challenge 2 reached through the main Continue button | Candidate asked for the same navigation approach as the rest of the activity. The engine now lets a stage supply its own button label and handle its own advance, so there is one forward control throughout |
| Bar width capped, tooltips clamped inside the plot | A tooltip on the last bar of a twelve bar chart hung 70px past the chart's edge. Found only by looking at it in a browser |
| Short badge forms below 760px | "Example" needed 62px in a 43px column on a phone |
| The scrap step requires weeks 7 and 12 | Candidate spotted that the instruction asked for both while the logic accepted any two. The task line and the navigation hint now name whichever is still missing |

## Version 5 &mdash; corrections from the independent audit

| Decision | Reason |
|---|---|
| The scrap assumption is stated once, above the charts, before any estimate | The audit's highest finding. One clear statement at the point of use, rather than warnings scattered through the activity, which is what the candidate asked for. The exercise itself is unchanged because it is the strongest teaching moment in the data |
| "Estimated scrap parts" used consistently in charts, tables and the note | The figures are conditional on an assumption the brief does not confirm. The label should say so wherever the number appears |
| The claim that real counts would differ only slightly was removed | One alternative definition happens to differ by about six parts, but nothing on the sheet constrains the others. Replaced with the rounding caveat, which is supportable: percentages recorded to one decimal place leave the weeks 11 and 5 estimates in either order |
| The median explanation names the sort and the two middle figures | Twelve values have no middle one. The previous wording taught the wrong definition and implied a week that does not exist |
| The investigated week and the week 7 decision are separate records on the printout | They were adjacent, so investigating week 5 and declining to raise week 7 printed as though the storm explained week 5 |
| Trend arrows compare with the week above and show nothing when unchanged | The previous rule was positional, so it marked week 12's unchanged 8 hours as a reduction and was right on the other measures only by coincidence. The table now states the comparison basis |
| The storm note is context, not a full account | The brief gives no outage duration, no output rate and no breakdown of the 1,350 unit shortfall. Both learner answers remain valid and neither is treated as correct |
| The comparison counter starts at 1 of 3, and the average screen is gated on one toggle | Both were statements the activity made about the learner that were not true: a view counted as unseen while on screen, and an instruction the learner could skip |
| No new completion tracking was added | The candidate asked that informational observations not become new functionality. The optional note stays optional and is still reported honestly when left blank |

## Version 6 &mdash; second audit round and release

| Decision | Reason |
|---|---|
| The average gate records seeing the excluded state only | Clicking the already-selected button satisfied the old flag without showing the learner anything new. The included state is what the screen opens on, so the excluded one is the half worth gating. The flag was renamed `sawExcluded` so its name matches what it means |
| Examples became a read-only list instead of one-click inserts | The candidate wanted learners encouraged to formulate a question themselves. A button that pastes a finished expert sentence does the thinking for them. The examples remain, as examples |
| Finishing with all three gaps empty prompts once, then lets the learner through | The activity is ungraded and aimed at people with low literacy and digital confidence, so a hard requirement was rejected. A single gentle prompt with an explicit "Continue without writing anything" respects both the learning intent and the learner |
| The printout is three labelled sections | Previously the learner's words and the supplied lesson summary sat in one card, so a printed note could imply the learner authored conclusions the activity handed them. Now: what they wrote, what they did, and what was supplied |
| Focus tints the column and rings the bar | The focusable control is the full-height column, so the hit area still needs showing, but a ring around empty space does not say which value is focused. One ring, on the bar |
| Scroll hints only on tables that actually overflow | Added at runtime by measuring, so nothing appears on a desktop. Stages 1 and 2 keep a single table because splitting them would separate figures the learner has to compare, which the candidate warned against |
| An inline challenge button was not re-added | It existed, and was removed one iteration earlier at the candidate's request for a single forward control. The task strip now names the control instead |
| The confetti stays | Asked for by the candidate, and already suppressed under reduced motion |
| The application moved to `public/index.html` | Deploying the repository root would have published the candidate brief, the private project notes and all three audit reports. A dedicated deploy directory makes that structurally impossible rather than a matter of remembering |

## Version 7 &mdash; Design Lens

A reviewer feature added at the candidate's request so an interview panel can explore the reasoning
behind the build without reading this documentation.

| Decision | Reason |
|---|---|
| Off by default, behind a small glasses icon in the header | It is not part of the learner's journey and must not compete with the activity. Nothing is marked, outlined or focusable until it is switched on |
| Annotations are attached after each render, not written into the stage code | The candidate asked that the learning activities not be modified to accommodate it. The stages are untouched: a list of selectors is matched against the rendered page and cleaned off again when the feature is turned off |
| Every explanation restates a decision already recorded | The candidate asked for no invented reasons and no decisions attributed to them that they did not make. Each note maps to a row in this file or to a finding in review-findings.md. Where nothing was recorded, nothing is marked, which is why the welcome screen carries two notes and other screens carry six or seven |
| Nineteen annotations, on regions rather than individual controls | Annotating every button would be noise, and marking a control would risk interfering with it. The marked areas are containers, so pressing a marker never triggers a learner action |
| A small marker button on each marked area, not just hover | Hover alone would make it a desktop-only feature. The marker is a real button, so it works with keyboard focus and touch, and carries its own accessible name |
| The explanation panel docks above the navigation rather than floating beside the element | A floating box next to a full-width element always covers whatever is beneath it. A fixed corner never covers the thing it describes, and on a phone the marked area is scrolled clear of the panel. Found by looking at the first build, where the panel sat over the measure buttons |
| Highlighting uses an outline only, never a background | The first attempt repainted the highlighted element's background, which washed out the white text on the dark task strip |
| Nothing is marked until hovered or focused | The first attempt outlined every marked area the whole time, which competed with the activity and looked like the chart's own "choose a week" affordance |
| The disclaimer sits inside the sticky header | It stays visible for as long as the feature is on, and putting it inside the header avoids a gap appearing between the two when the header height changes at small sizes |
| Design Lens never prints | It is reviewer scaffolding, not part of the learner's record |

## Version 8 &mdash; README showcase

| Decision | Reason |
|---|---|
| Assets live in `docs/assets/`, outside `public/` | The deploy directory must contain only the activity. README imagery is development material and has no place on a learner-facing site |
| Screenshots captured from the running build, not mocked up | The brief's accuracy rules apply to the repository as much as the activity. Every screen shown is the real thing in a real state |
| Diagrams hand-authored as SVG from a script, in the application's palette | They stay consistent with the product, stay small (4 to 8 KB each), scale cleanly, and a light and dark variant can be generated from one source |
| One animation only, of the chart manipulation | It is the strongest moment in the activity and the one that is genuinely hard to convey in words. A static three-panel alternative sits behind a disclosure for anyone who cannot use it |
| Explicit HTML wherever Markdown sits inside an HTML block | GitHub's handling depends on CommonMark's blank-line rule. Writing those fragments as HTML removes the dependency entirely |
| No badges, no emoji, no invented metrics | The README states what the project is and what was actually verified. There are no user numbers, completion rates, testimonials or certifications because none exist |
| Limitations given their own section | A resource about questioning evidence should be straightforward about the gaps in its own |

## Risks recorded, not acted on

- **Completion time for less confident learners.** The Gemini review suggests the activity may run
  considerably longer than the stated 15 to 20 minutes for this audience. The measured prose load
  supports the stated range for an average reader, but nobody from the intended audience has been
  timed. Recorded as a risk. Redesigning around an unmeasured estimate was explicitly ruled out, and
  the honest resolution is learner testing rather than more guessing.

## If this were taken further

Recorded at the candidate's request. None of this is built, and none of it is needed for the
demonstration.

- **Testing with the actual audience.** Nothing here has been in front of a machine operator, a
  packer or a maintenance assistant. The design rests on a reading of the brief and on published
  research about data and digital confidence, not on watching anyone use it. That is the single
  biggest gap, and it would almost certainly change things: where people hesitate, which
  instructions are unclear, and whether the language is genuinely plain enough.
- **Accessibility testing with real assistive technology.** Accessibility has been designed in from
  the first version and verified structurally and programmatically throughout, but no screen reader
  has been used. That testing is what would turn a well-built guess into a verified result.
- **The optional guided walkthrough.** Dropped in the first version as too expensive for a
  demonstration, and that still looks right. For learners with low confidence navigating online
  learning it could be genuinely useful, and it would be worth building once there is real evidence
  about where people get stuck rather than guessing at it now.
- **Iterating on learner feedback rather than on further ideas.** The candidate's position, and the
  right one: development from here should be driven by observed problems, not by additional
  features. The build is at the point where more ideas would cost more than they return.

## Known limitations of the current build

- Design Lens explanations were written with AI from the project's own records. They are accurate
  summaries of recorded decisions, but they are summaries, and the activity states this on screen
  whenever the feature is on.

- The scrap-in-parts figures are estimates that depend on an assumption the brief does not confirm.
  The activity states this before the learner uses them rather than resolving it, because it cannot
  be resolved from the supplied data.

- No screen reader testing has been carried out by anyone, across any version.
- No testing with anyone from the intended audience.
- iOS Safari and Android Chrome have not been tested on real hardware.
- At 360px the matching step is taller than one screen. The chart is scrolled into view when a note
  is selected, but the whole task is not visible at once.
- Reading time sits near the top of the brief's 10 to 20 minute allowance for a slow reader.

## Considered and cut

| Idea | Why it was cut |
|---|---|
| Comparing units minus scrap across weeks 10 and 12 | Net output is nearly identical, which is a real finding but too subtle to land in 15 minutes. |
| A third stage 3 task: "set the view this quoted email is based on" | The two challenges already do that work. Cut to protect the time budget. |
| Scrap %/parts toggle shown on weeks 8&ndash;12 only | Output barely moves across those weeks, so percentage and parts rise together and the toggle teaches nothing. The reveal needs weeks with different output in frame, so it runs across all twelve with week 7 visible. |
| `localStorage` resume | See scope table. |
| Per-measure "pick the worst week" loop on the investigation stage | Week 7 is the answer on all four measures, so it is one click repeated four times. Free exploration followed by a single commitment instead. |
| Updating individual slots instead of re-rendering the panel | Would have put the verified focus restoration and live region at risk to solve a layout problem. |
| Removing the on-bar value labels in favour of axis ticks and tooltips, per the `dataviz` anti-pattern | From a zero baseline a 4% spread is visually identical, and a tooltip cannot answer "which is lowest?" without hovering every bar. Labels kept where they fit; tooltips added where they do not. |
| Reworking the 4px left borders and the tick glyph, per the `impeccable` craft floor | The candidate pinned the look and asked for no design changes made for their own sake. The skill states a pinned brief overrides it. |
| Moving value labels above the bar cap, with a headroom factor in the chart geometry, per the `dataviz` label spec | It would have changed bar, gridline, target line, average line and axis positioning together, in service of a spec rather than any feedback given. Both "use the space" complaints were about tables. Capping bar width achieves the same visual result in one declaration. |
| The `display:block` responsive table pattern for the data sheet on small screens | It strips a table's implicit ARIA role in Chrome and Safari. With screen reader testing already the largest untested risk, that is the wrong place to take an unverified bet. Three narrower tables instead. |
| Clipboard copy on the summary card | Candidate decision: print only. |

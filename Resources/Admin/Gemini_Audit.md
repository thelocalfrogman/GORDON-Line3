# Independent Instructional Design and Learning Experience Quality Assurance Review

**Resource Reviewed:** *Line 3: Reading the Weekly Numbers* (Standalone Browser Interactive `index.html`)

**Evaluation Benchmark:** Candidate Practical Task Brief (*Read the Numbers* — The Gordon TAFE)

**Audience Profile:** Manufacturing personnel (machine operators, packers, maintenance assistants) at Ridgeway Components; varying digital confidence, no formal data/statistics training, accessing via phones or shared PCs during short workplace breaks.

---

## 1. Executive Summary

*Line 3: Reading the Weekly Numbers* is an exceptionally well-conceived, highly disciplined adult learning activity that squarely meets its learning brief. Built as a self-contained, lightweight single-file HTML/JS web application without external libraries or tracking overhead, it runs reliably in any browser on both mobile and desktop screens.

Educationally, the resource avoids the standard corporate compliance trap of passive text presentation followed by token multiple-choice quizzes. Instead, it employs guided inquiry, authentic workplace friction, and purposeful manipulation. Rather than simply telling learners that charts can deceive, it puts them in the driver's seat to manipulate scale baselines and sample ranges to intentionally engineer two conflicting narratives from identical numbers (Stage 3), followed immediately by structured deconstruction (Stage 4). It treats the workplace audience respectfully: language is unpretentious and grounded in production realities, mathematical terminology (such as median vs mean) is explained intuitively without statistical jargon, and ambiguity is validated rather than artificially flattened.

The design's primary pedagogical vulnerability lies in its final assessment handover. While the journey systematically guides the learner through reading numbers, spotting deceptive formats, and identifying hidden variables, the culminating workplace artifact (Stage 8, completed in Stage 9) allows learners to bypass active synthesis entirely. Learners can click pre-written prompt chips or leave textareas empty and still proceed to print an artifact that backfills comprehensive expert answers into a summary list. Consequently, while the resource **introduces**, **teaches**, and **practices** all three core outcomes, **independent demonstration** of critical questioning is partially scaffolded away at the final hurdle.

---

## 2. Requirements Alignment

| Requirement (Candidate Brief) | Implementation Status | Supporting Evidence & Analysis |
| --- | --- | --- |
| **Duration (10–20 minutes)**<br> | **Met** | 10 distinct, tightly scoped stages. Linear flow with clear progress counters; concise text designed for rapid scannability on workplace shifts.

 |
| **Standalone Browser Interactive (Single HTML file, No SCORM)**<br> | **Met** | Completely self-contained in a single lightweight HTML document (`index.html`) using vanilla ES6 JavaScript and CSS; zero external dependencies, web fonts, or CDN assets.

 |
| **Actions change what learner sees/hears (More than a quiz)**<br> | **Met** | Dynamic DOM rendering adjusts bar chart baselines ($0$ vs $4,600$), switches data metrics, reveals multi-column tables, updates trend indicators, links dual scatter/bar plots, and generates customized printable summaries.

 |
| **Progressive Difficulty**<br> | **Met** | Well-scaffolded progression: starts with concrete 1-to-1 data matching (Stage 1), moves to multi-metric exploration (Stage 2), chart manipulation (Stages 3–4), statistical nuance (Stage 5), compounding workplace variables (Stage 6), rate vs volume denominator traps (Stage 7), and open inquiry synthesis (Stages 8–9).

 |
| **Unchanged Dataset (Line 3, Weeks 1–12)**<br> | **Met** | Full 12-week dataset hardcoded in JavaScript matches the brief exactly across all 5 variables (Units, Target, Downtime, Fault Calls, Scrap %) and both supervisor notes.

 |
| **No AI Naming or Promotion**<br> | **Met** | Source code and learner-facing UI inspected: zero mention of AI, LLMs, machine learning, or generative tools.

 |
| **Plain Language & Worked Examples**<br> | **Met** | Stage 1 provides a fully solved worked example card ("Example: Week 3") before requiring interaction. Clear, conversational workplace register used throughout.

 |
| **Accessible & Non-Specialist**<br> | **Met** | Standard keyboard navigation, live region screen reader announcements (`aria-live="polite"`), high-contrast elements, touch targets $\ge 48\text{px}$, and responsive CSS flexbox/grid layout.

 |

---

## 3. Learning Outcome Evaluation

### Learning Outcome 1: Read simple charts and tables and explain what they show in plain language

.

* **Introduced:** Stage 0 (Welcome) and Stage 1 (Reading the sheet).


* **Taught:** Stage 1 uses a concrete worked example (Week 3: $4,870$ units vs $5,000$ target $= 130$ short, $13\text{h}$ downtime). It teaches that a single figure has little meaning until anchored against a benchmark target or peer weeks.


* **Practised:** Stage 1 requires matching three real workplace statements to chart columns and data table cells. Stage 2 requires toggling across four distinct operational metrics (units, downtime, fault calls, scrap %).


* **Demonstrated:** Stage 1 forces correct pairing of all cards before progression is unlocked. Stage 8 prompt `a` invites learners to state a visible trend in their own words.


* **Evidence & Limitations:** Evidence in Stage 1 is strong for reading and extracting values. Stage 8, however, allows pre-written text chips to be inserted, which allows learners to bypass explaining trends in their own words.


* **Rating:** **Adequately Addressed**

### Learning Outcome 2: Recognise at least two ways a graph or chart can mislead

.

* **Introduced:** Stage 0 lede ("Occasionally it gives an impression that the figures underneath do not quite support").


* **Taught:** Stage 3 and Stage 4 directly teach two classical data distortions: (1) truncated vertical axes ($y$-axis baseline elevated to $4,600$), which magnifies small normal variance into severe drops and visually clips Week 7 off the bottom of the chart; and (2) selective timeframe reporting ("cherry-picking" Weeks 1–7 vs Weeks 8–12). Stages 5 and 7 add two further distortions: mean distortion caused by single-event outliers, and percentage-versus-absolute volume illusions.


* **Practised:** Stage 3 tasks the learner with purposefully constructing two deceptive charts using baseline and range toggles. Stage 4 isolates these two variables side-by-side.


* **Demonstrated:** Learners must successfully configure both misleading views to proceed through Stage 3. Stage 4 requires inspecting both mechanisms before the navigation button activates.


* **Evidence & Limitations:** Pedagogically outstanding. Forcing the learner to act as the "deceiver" creates deeper metacognitive awareness than passive exposure.


* **Rating:** **Strongly Addressed**

### Learning Outcome 3: Formulate questions to ask before acting on data

.

* **Introduced:** Stage 2 (Investigating Week 7) and Stage 6 (The last five weeks).


* **Taught:** Stage 2 teaches that external contextual factors (severe storm) explain disruption but do not automatically account for total production variances. Stage 6 explicitly highlights unmeasured variables: increased unit output coincided with Saturday overtime shifts (hours worked is omitted), and reduced fault calls coincided with a revised logging form. Stage 7 teaches that scrap percentage cannot be converted into part volumes without clarifying the denominator.


* **Practised:** Stage 2 asks learners to make a subjective judgment on whether to raise Week 7 with their supervisor. Stage 8 prompt `b` ("From these figures alone I cannot tell...") and prompt `c` ("Before we act on these numbers, the question I would like to raise is...") prompt question formulation.


* **Demonstrated:** Stage 8 textarea input.


* **Evidence & Limitations:** Stage 8 text fields are entirely optional and can be submitted completely blank. Furthermore, one-click starter chips allow learners to adopt pre-formulated questions rather than constructing their own. If a learner enters nothing, Stage 9 prints out expert summary takeaways anyway.


* **Rating:** **Partially Addressed**

---

## 4. Full Learner Journey Review

```
[Stage 0: Welcome / Orientation]
               │
               ▼
[Stage 1: Guided Data Matching (Worked Example + Cards)]
               │
               ▼
[Stage 2: Multi-Metric Investigation (Week 7 Outlier & Supervisor Note)]
               │
               ▼
[Stage 3: Guided Manipulation (Engineer "Trouble" & "Success" Views)]
               │
               ▼
[Stage 4: Analytical Deconstruction (Truncated Axis vs Cherry-Picking)]
               │
               ▼
[Stage 5: Statistical Distortion (Mean vs Median & Outlier Impact)]
               │
               ▼
[Stage 6: Confounding Operational Variables (Saturday Overtime & New Log Forms)]
               │
               ▼
[Stage 7: Denominator Ambiguity (Scrap % vs Absolute Bin Count)]
               │
               ▼
[Stage 8: Synthesis Scaffold (Drafting the Team Meeting Note)]
               │
               ▼
[Stage 9: Artifact Export (Printable Workplace Note & Debrief)]

```

### Stage 0: Welcome (`ST[0]`)



* **What the learner does:** Reads the orientation screen outlining the scenario at Ridgeway Components, the purpose of the 12-week review, time expectations ($15\text{–}20$ mins), and clicks "Start the activity".


* **Educational intent:** Establish psychological safety (reassuring learners that nothing is scored, tested, or transmitted) and set context.


* **What works:** Clear, non-academic tone; upfront explanation of session scope and persistence limitations (no progress saved on close).


* **Friction / Cognitive load:** Text is somewhat panel-heavy for mobile displays, but clean typography mitigates fatigue.


* **Justification:** Essential for adult learners who may feel anxious about formal testing.



### Stage 1: Reading the Sheet (`ST[1]`)



* **What the learner does:** Reviews a persistent worked example card (Week 3), then clicks one of three prompt cards (Note A, B, or C) and selects the corresponding bar/table row for Weeks 1–6.


* **Educational intent:** Ground learners in reading coordinates, benchmarks, and multi-column tables.


* **What works:** Excellent instructional scaffolding. If a learner clicks a column before selecting a note card, an informative message guides them without penalisation. Immediate, contextual feedback explains why an answer is correct or incorrect using exact figures. If a user fails three times, an automated hint points them to the comparative table below.


* **Friction / Cognitive load:** On mobile screens, the sticky column layout stacks, requiring the learner to scroll between cards above and the chart/feedback slot below.


* **Justification:** Justified; builds baseline competence before introducing complexity.



### Stage 2: Finding the Week That Stands Out (`ST[2]`)



* **What the learner does:** Cycles through four metric buttons (Units, Downtime, Fault Calls, Scrap %), selects the week they believe stands out, reviews an automated ranking table, reads the supervisor's storm note, and chooses whether they would raise Week 7.


* **Educational intent:** Demonstrate that focusing on a single measure gives an incomplete picture, and introduce qualitative context (supervisor notes).


* **What works:** The application requires the learner to view all four metrics before unlocking the chart selection. Both "Yes" and "No" answers to the supervisor question are affirmed as reasonable, explaining that operational context does not necessarily explain the entire variance.


* **Friction / Cognitive load:** High informational density once the ranking table, note card, and decision buttons simultaneously appear on screen.


* **Justification:** Strong bridge between raw numbers and workplace inquiry.



### Stage 3: Two Stories (`ST[3]`)



* **What the learner does:** Uses segmented button controls to toggle chart baseline ($0$ vs $4,600$) and range (All 12, Weeks 1–7, Weeks 8–12) to solve two challenges: make Line 3 look in crisis, then make it look like a roaring success.


* **Educational intent:** Active discovery of axis truncation and timeframe selection.


* **What works:** Dynamic chart recalculation with nudging feedback when near the correct combination. Learners directly experience how easy it is to visually manipulate data without altering underlying facts.


* **Friction / Cognitive load:** The transition between Challenge 1 and Challenge 2 occurs via the bottom sticky navigation button rather than within the card itself. This is manageable but can briefly disorient a novice user.


* **Justification:** The pedagogical core of the application; exceptionally effective.



### Stage 4: What Changed (`ST[4]`)



* **What the learner does:** Examines three isolated views: "The full picture", "Change 1: cut the scale", and "Change 2: hide some weeks".


* **Educational intent:** Isolate the two variables manipulated in Stage 3 so learners understand the underlying mechanisms rather than just the button combinations.


* **What works:** Explicitly highlights the visual clipping of Week 7 when baseline is $4,600$ ("Week 7 has fallen off the bottom").


* **Friction / Cognitive load:** Low cognitive load; provides essential consolidation.


* **Justification:** Critical debrief step preventing the "gaming the buttons" failure mode.



### Stage 5: The Average (`ST[5]`)



* **What the learner does:** Toggles a single button to include or exclude Week 7 (storm week) from the 12-week mean production line.


* **Educational intent:** Teach how extreme outliers skew arithmetic means, and contrast mean against median.


* **What works:** Clean, intuitive visualization: a horizontal reference line drops from $4,953$ to $4,844$ units with Week 7 included, visually explaining how an email summary ("averaged under 4,850") can distort perceptions of an otherwise strong run. Median is defined simply as the middle value without intimidating statistical notation.


* **Friction / Cognitive load:** Minimal. One clear idea executed cleanly.


* **Justification:** Highly applicable to everyday workplace communication.



### Stage 6: The Last Five Weeks (`ST[6]`)



* **What the learner does:** Progressively reveals columns (Downtime, Fault Calls, Scrap %) for Weeks 8–12, observes directional trend arrows, reads the Week 10 supervisor note, and reviews two analytical panels.


* **Educational intent:** Teach learners to spot conflicting metrics and recognize confounding real-world variables (overtime shifts and administrative changes to log forms).


* **What works:** Highlighted directional arrows visually emphasize that while downtime and fault calls improved, scrap percentage deteriorated. The commentary explicitly warns that output gains might reflect Saturday overtime hours rather than line efficiency.


* **Friction / Cognitive load:** Requires reading two separate analytical callout panels at the bottom of the screen.


* **Justification:** Outstanding authentic workplace data literacy.



### Stage 7: Share or Parts (`ST[7]`)



* **What the learner does:** Selects weeks on two synchronized side-by-side charts—one showing Scrap % and the other showing estimated Scrap Parts—specifically comparing Week 7 against Week 12.


* **Educational intent:** Teach the mathematical impact of changing baselines/denominators (a smaller percentage of a larger production run can equal more scrap parts than a high percentage of a low run).


* **What works:** Direct juxtaposition of Week 7 ($3.9\%$ of $3,650 = 142$ parts) versus Week 12 ($2.6\%$ of $5,150 = 134$ parts). Makes an abstract mathematical principle visually concrete.


* **Friction / Cognitive load:** Moderately high. Learners must grasp that scrap parts are modeled estimates based on an unverified operational assumption.


* **Justification:** Essential critical data competency for industrial line workers.



### Stage 8: Your Note (`ST[8]`)



* **What the learner does:** Completes three sentence stems for an upcoming team meeting note, with the option to click starter chips or scroll down to full data tables.


* **Educational intent:** Synthesise learning into workplace communication.


* **What works:** Non-threatening scaffold using sentence starters; jump links allow fast navigation between the form and reference tables.


* **Friction / Cognitive load:** High literacy hurdle. Learners who struggle with written English or typing may experience friction, leading them to click chips passively or skip fields.


* **Justification:** Authentic vocational synthesis, though let down by passive bypass options.



### Stage 9: Your Notes / Summary (`ST[9]`)



* **What the learner does:** Reviews their generated note along with an automated audit log of their decisions, views a data table, triggers browser print, or resets the activity.


* **Educational intent:** Provide a permanent take-away artifact and positive closure.


* **What works:** Elegant CSS print stylesheet hides navigation bars and formats a clean one-page memo for the noticeboard or meeting.


* **Friction / Cognitive load:** If the learner skipped typing in Stage 8, the card shows a passive placeholder message ("You did not fill in the note. The record of what you did is below").


* **Justification:** Solid capstone for workplace training.



---

## 5. Interaction Quality

| Interaction | Cognitive Task | Learner Autonomy | Learning Value Assessment |
| --- | --- | --- | --- |
| **Card Matching (Stage 1)**<br> | Information retrieval, cross-referencing multi-variable tables and charts.

 | High within bounded options (can pick any card in any sequence).

 | **Substantive.** Forces active scanning of chart axes and data columns; far superior to standard 4-option multiple-choice.

 |
| **Metric Exploration & Decision (Stage 2)**<br> | Comparative ranking, multi-metric evaluation, qualitative contextual judgment.

 | High exploration, open qualitative choice.

 | **Substantive.** Unlocks deep appreciation of how single-metric views mislead.

 |
| **Chart Manipulation (Stage 3)**<br> | Hypothesis testing, goal-directed manipulation, reverse-engineering visual bias.

 | High (combinatorial: $2 \times 3$ matrix).

 | **Exemplary.** Puts the learner in active control of visual framing.

 |
| **Deconstruction (Stage 4)**<br> | Controlled variable comparison.

 | Guided switching.

 | **Moderate to High.** Reinforces the specific mechanisms behind the Stage 3 manipulation.

 |
| **Outlier Toggle (Stage 5)**<br> | Sensitivity analysis.

 | Single toggle.

 | **Moderate.** While binary, the visual movement of the average line immediately demystifies outlier distortion.

 |
| **Metric Reveal (Stage 6)**<br> | Pattern recognition across time-series data.

 | Unconstrained reveal sequence.

 | **Moderate.** Progressive unmasking manages cognitive load while building an increasingly complex picture.

 |
| **Dual Chart Comparison (Stage 7)**<br> | Proportional reasoning, distinguishing rates from absolute counts.

 | Interactive bar exploration across 12 weeks.

 | **Exemplary.** Solves a notoriously difficult mathematical trap using paired, interactive visual feedback.

 |
| **Meeting Note Drafting (Stage 8)**<br> | Synthesis, contextual questioning, self-expression.

 | Complete open-text freedom, but with bypass risk.

 | **Mixed.** Excellent structure, but one-click starter chips reduce active synthesis to mechanical assembly.

 |

---

## 6. Audience Suitability

### Plain Language and Workplace Register

The copywriting strikes an ideal adult vocational tone: respectful, practical, and devoid of condescension. Jargon is systematically eliminated:

* Instead of *“$y$-axis truncation”*, it uses *“cutting the bottom off the scale”*.


* Instead of *“cherry-picking longitudinal cohorts”*, it uses *“choosing which weeks to show”*.


* Instead of *“parametric sensitivity to extreme skewness”*, it explains *“one week in twelve moves the figure by more than 100 units a week, making the other eleven look worse than they were”*.


* Instead of *“rate vs volume denominator divergence”*, it frames the issue as *“scrap as a share, and scrap as parts”*.



### Respect for Workplace Experience

The resource assumes learners are skilled, intelligent operators who know their line intimately. Rather than treating workers as mathematically deficient, it validates common shopfloor instincts: it acknowledges that when Saturday overtime starts, output naturally rises without line productivity necessarily improving. It similarly validates workers' healthy skepticism when administrative reporting forms change.

### Cognitive Load Management

The application structure is disciplined. Visual elements are strictly coordinated:

1. Chart components and data tables use matching colour variables (`--bar`, `--bar-sel`, `--bar-match`, `--warn-bg`).


2. Feedback panels are anchored in fixed-height layout slots (`.slot`), preventing sudden layout shifts that disorient novice users.


3. Progressive disclosure is used effectively: tables on complex screens default to collapsed accordions (`<details>`), preventing visual overwhelm.


4. Complex concepts are isolated into dedicated steps rather than combined into a single dashboard.



---

## 7. Accessibility and Usability

*Note: Evaluation conducted via comprehensive source-code structural inspection, DOM keyboard interaction validation, and simulated viewport/media query testing. Assistive technology testing was limited to automated ARIA live-region audit and DOM accessibility tree inspection.*

### Confirmed Strengths

* **Keyboard Navigation:** Every interactive element is a native `<button>` or `<textarea>` element. Tab order is logical and strictly vertical/horizontal through component groups.


* **Focus Management:** The custom JavaScript engine includes a dedicated `focusKey()` and `restoreFocus()` routine. In dynamic single-page applications where the root container is replaced via `innerHTML`, browser focus frequently resets to `<body>`, stranding keyboard users. This script explicitly stores the active control's data attributes and restores focus to the corresponding control post-render.


* **Screen Reader Architecture:** A persistent, visually hidden live region (`#live.sr[role="status"][aria-live="polite"]`) is embedded outside the dynamic `#main` container. Dynamic feedback, note reveals, and metric changes are scrubbed of HTML tags and announced cleanly.


* **Hit Targets:** Buttons adhere to minimum touch standards (min-height $48\text{px}$, segmented buttons $48\text{px}$, textareas large and accessible). Chart columns use full-height hit areas so that short bars remain easy targets on touchscreens.


* **Reduced Motion:** A comprehensive `@media (prefers-reduced-motion: reduce)` media query neutralises bar grow animations, pulse transitions, and disables confetti.



### Identified Accessibility & Usability Defects

1. **Interactive Chart Columns Lack Visible Focus Rings in Dynamic States:** While `:focus-visible` is styled globally (`3px solid var(--focus)`), chart columns (`.col`) rely partly on internal bar brightness filters and box shadows. In high-contrast ambient workplace lighting, the focus state on a single narrow bar inside a 12-bar plot can be difficult to track.


2. **Missing `aria-expanded` on Dynamic Collapsibles:** The examples drawer in Stage 8 uses a custom class toggle (`.hidden`) controlled by a button, but lacks an `aria-expanded="false|true"` attribute to communicate state changes to screen readers.


3. **Table Horizontal Overflow on Mobile:** On viewports under $400\text{px}$, the wide 6-column data tables in Stages 1 and 2 rely on `.tablewrap` horizontal scroll. While functional, users with low digital literacy frequently do not realize that tables can be scrolled sideways, potentially missing the downtime and scrap columns.



---

## 8. Time and Completion Estimate

Target duration in Candidate Brief: **10 to 20 minutes**.

| Phase / Screen | Learner Profile A<br>

<br>*(Digitally comfortable, new to data)* | Learner Profile B<br>

<br>*(Low digital confidence, slower reading pace, mobile device)* |
| --- | --- | --- |
| **Stage 0: Welcome**<br> | 1.0 min | 2.5 mins |
| **Stage 1: Reading Sheet (Matching)**<br> | 1.5 mins | 3.5 mins (includes 1–2 incorrect attempts) |
| **Stage 2: Investigating Week 7**<br> | 1.5 mins | 3.0 mins |
| **Stage 3: Two Misleading Charts**<br> | 2.0 mins | 4.0 mins (requires trial-and-error toggling) |
| **Stage 4: Isolating the Changes**<br> | 1.0 min | 2.0 mins |
| **Stage 5: The Average & Median**<br> | 1.0 min | 2.0 mins |
| **Stage 6: Confounding Factors**<br> | 1.5 mins | 2.5 mins |
| **Stage 7: Scrap % vs Parts**<br> | 2.0 mins | 3.5 mins |
| **Stage 8: Drafting Meeting Note**<br> | 2.5 mins (types brief responses) | 3.5 mins (clicks chips or writes single words) |
| **Stage 9: Review & Print**<br> | 1.0 min | 1.5 mins |
| **Total Estimated Time** | **15.0 minutes** | **28.0 minutes** |

### Assessment

The activity comfortably fits within the 10–20 minute window for digitally confident learners (Profile A). However, for learners with low digital confidence and slower reading speeds (Profile B)—especially when accessing the resource on a mobile phone during a shift break—completion will likely take $25\text{–}30$ minutes. This extended duration is driven by the density of the 10-stage progression and the amount of explanatory prose across Stages 6–8. While entirely manageable in a structured training setting, learners completing it in short, fragmented breaks may struggle to finish in one sitting.

---

## 9. Detailed Findings Register

```
FINDING REGISTER SUMMARY:
├── CRITICAL    : 0 findings
├── HIGH        : 1 finding   (F-01: Blank Submission / Bypass)
├── MEDIUM      : 3 findings  (F-02: Chart Focus Visibility; F-03: aria-expanded; F-04: Mobile Table Overflow)
├── LOW         : 2 findings  (F-05: Missing Units Label; F-06: Stage 3 Nav Confusion)
└── INFORMATIONAL: 1 finding  (F-07: Confetti Execution)

```

### Finding F-01: Assessment Bypass and Unearned Synthesis in Final Workplace Note

* **Severity:** **High**
* **Location:** Stage 8 (`ST[8]`) & Stage 9 (`ST[9]`)


* **Behaviour/Wording:** Textareas for stems `a`, `b`, and `c` have no validation checks (`ok: () => true`). A learner can leave all three boxes blank and proceed directly to Stage 9. Furthermore, clicking a "starter chip" instantly pastes a fully formed expert insight into the textarea. In Stage 9, the resulting card presents a complete expert debrief ("Ways the same figures can give a misleading impression", "Three questions worth asking...") regardless of the learner's actual input.


* **Educational Impact:** Compromises Learning Outcome 3. While this is an ungraded learning activity, allowing a completely blank submission without a gentle nudge or confirmation check undermines the synthesis stage. It enables passive clicking instead of prompting workers to formulate their own questions.


* **Evidence:** Source inspection lines 559–564 (`ok: () => true`) and lines 597–616 (static pre-rendered summary definition list).


* **Recommended Correction:** Require at least one sentence stem to be engaged before enabling progression, or introduce a soft confirmation modal if all three fields are blank: *"You haven't added any notes. Do you want to write a quick thought, or continue to the summary?"* If chips are clicked, append them as editable prompts that require the learner to add their own reason.


* **Confidence Level:** High (directly verified via source code analysis).

### Finding F-02: Keyboard Focus Visibility on Small Dynamic Bar Columns

* **Severity:** **Medium**
* **Location:** CSS `.col` and JavaScript `chart()` function


* **Behaviour/Wording:** When navigating chart bars via keyboard `Tab`, focus is applied to `.col`, which triggers an outline on the parent container. However, the actual visual bar is a child element (`.bar`), which applies `filter: brightness(1.18)` on hover, but on keyboard focus relies on `:focus-visible` offset outlines that can visually clip against neighboring chart gridlines.


* **Educational Impact:** Low-confidence digital users navigating via keyboard or switch devices on factory terminals may lose track of which week they have selected.


* **Evidence:** CSS inspection lines 122–142.


* **Recommended Correction:** Add an explicit `.col:focus-visible .bar { outline: 3px solid var(--focus); outline-offset: 3px; }` rule to ensure high-contrast focus rings around the active bar element.


* **Confidence Level:** High.

### Finding F-03: Missing `aria-expanded` and Broken State Contract on Starter Chips

* **Severity:** **Medium**
* **Location:** Stage 8, line 548 (`<button type="button" class="starter" data-open="${b.k}">`)


* **Behaviour/Wording:** The toggle button dynamically reveals `#chips_${b.k}` by removing the `.hidden` class, but lacks an `aria-expanded` attribute.


* **Educational Impact:** Screen reader users receive no spoken confirmation that an interactive tray of examples has expanded below the field.


* **Evidence:** Code inspection lines 548 and 570–576.


* **Recommended Correction:** Add `aria-expanded="false"` to the button by default, and toggle it to `"true"` dynamically in the click handler.


* **Confidence Level:** High.

### Finding F-04: Undisclosed Table Scrolling on Small Mobile Screens

* **Severity:** **Medium**
* **Location:** CSS `.tablewrap` and Stage 1/Stage 2 data tables


* **Behaviour/Wording:** Six-column tables overflow horizontally on screens under $420\text{px}$. While `overflow-x: auto` allows scrolling, there is no visual indicator or text hint that off-screen columns exist.


* **Educational Impact:** Operators using smaller smartphones may only see "Week" and "Units produced", missing the Downtime, Fault Calls, and Scrap columns needed to answer questions in Stage 1 and Stage 2.


* **Evidence:** Rendered mobile viewport testing ($375\text{px}$ width). Stage 8 includes responsive stacked tables (`.only-narrow`), but Stages 1 and 2 retain the full 6-column table.


* **Recommended Correction:** Apply the responsive split-table pattern used in Stage 8 to Stage 1 and Stage 2, or add a subtle prompt: *"Swipe table to view downtime and scrap columns"*.


* **Confidence Level:** High.

### Finding F-05: Unclear Units on Fault Call Rate Feedback

* **Severity:** **Low**
* **Location:** Stage 6, `COLFB.fc`

* **Behaviour/Wording:** Line 446: *"Fault calls fell from 20 in week 8 to 13 in week 12. That is a drop of about a third. Looked at on its own, that is also an improvement."*

* **Educational Impact:** Minor precision issue. While $(20 - 13) / 20 = 35\%$, calling it *"a drop of about a third"* is good plain language, but combining unit counts and proportions can momentarily confuse learners who struggle with fractions.


* **Evidence:** Code inspection line 446.


* **Recommended Correction:** Retain current wording, but add the absolute number in parentheses: *"a drop of 7 calls (about a third)"*.


* **Confidence Level:** Low.

### Finding F-06: Navigation Location Disconnect Between Challenge Steps

* **Severity:** **Low**
* **Location:** Stage 3 (`ST[3]`)


* **Behaviour/Wording:** Completing Challenge 1 enables the primary "Go to challenge 2" button located in the fixed bottom navigation bar at the bottom of the viewport, rather than near the feedback card where the learner's attention is focused.


* **Educational Impact:** Learners with low digital confidence often look near the completed card for a "Next" button. When the feedback says "Challenge 1 complete", some may pause, unsure how to proceed until they notice the bottom bar.


* **Evidence:** Code inspection line 386–396.


* **Recommended Correction:** Add an inline primary button inside the feedback slot when solved: `<button class="btn">Continue to Challenge 2</button>` that hooks into `onNext()`.


* **Confidence Level:** Medium.

### Finding F-07: Confetti Animation on Completion

* **Severity:** **Informational**
* **Location:** Stage 9 (`confetti()`)


* **Behaviour/Wording:** Completing the activity triggers a falling confetti animation across the viewport for $3.4\text{ seconds}$.


* **Educational Impact:** While celebratory, adult manufacturing workers often perceive confetti as childish or patronising. On older, shared workplace PCs with low hardware specs, un-accelerated DOM-node animations can also cause brief browser lag.


* **Evidence:** Code inspection lines 629–647.


* **Recommended Correction:** Remove the confetti effect entirely; rely on the clean, professional green checkmark hero banner already present on screen.


* **Confidence Level:** High.

---

## 10. Prioritised Recommendations

### Must Fix Before Submission

1. **Prevent Blank Pass-Through on Final Note (F-01):** Update `ST[8].ok` so that the learner cannot advance without entering some text or explicitly acknowledging that they are skipping the step. If they choose to skip, present a soft prompt encouraging them to try one sentence stem.


2. **Add `aria-expanded` and Accessible Controls to Example Trays (F-03):** Update the button markup in Stage 8 to include `aria-expanded="false"` and `aria-controls="chips_a"`, updating the attribute dynamically in JavaScript.


3. **Resolve Mobile Data Table Overflow in Stages 1 & 2 (F-04):** Port the responsive `.only-narrow` split-table pattern developed for Stage 8 into Stages 1 and 2 so mobile operators do not have to scroll sideways off-screen to find downtime and scrap figures.



### Worth Improving If Time Permits

1. **Add Inline Progression Buttons in Stage 3 (F-06):** Place a prominent "Start Challenge 2" button directly inside the positive feedback panel on Stage 3, reducing eye travel to the fixed bottom navigation bar.


2. **Enhance Focused Bar Visuals for Keyboard Navigation (F-02):** Add a high-contrast `:focus-visible` outline to chart bars to make keyboard navigation clearer on low-contrast monitors.


3. **Remove Confetti Animation (F-07):** Remove the decorative DOM confetti animation to keep the visual tone professional, workplace-focused, and performant on shared workplace hardware.



### Future Development (Post-Recruitment / Production Scope)

1. **Local Storage / Session State Recovery:** Implement lightweight `localStorage` caching so shift workers can close their browser during an unexpected operational interruption and resume without losing their place.


2. **Real-User Assistive Technology & Device Testing:** Conduct field validation with workers using NVDA, JAWS, and TalkBack on shared factory kiosks and low-cost Android mobile devices.


3. **Supervisor Facilitation Guide:** Create a one-page companion guide for line supervisors to help them facilitate a 5-minute toolbox discussion based on the printed notes produced in Stage 9.



---

## 11. Final Verdict

### **Verdict:** **READY WITH QUALIFICATIONS**

**Rationale:**

The submission meets the instructional design brief. It builds an interactive learning activity using the supplied data, respects workplace constraints, avoids jargon, and engages learners in critical thinking. The interactive chart manipulation in Stages 3 and 4 is an effective example of discovery learning.

The qualification is pedagogical rather than functional: the final note-writing activity in Stage 8 allows learners to bypass active synthesis by clicking pre-written chips or submitting blank fields, weakening the evidence for Learning Outcome 3. Addressing this minor gap along with the few identified accessibility/mobile table improvements will ensure the resource is ready for deployment.

---

## Panel Interview Defense Questions

### 1. If you were on the interview panel, would this resource demonstrate sound instructional design judgement?

**Yes.** The candidate demonstrates sound instructional design instincts for adult vocational learners. They avoided typical e-learning conventions—such as multi-paragraph introductions, locked linear slides, and multiple-choice quizzes. The design shows that the candidate understands their audience: it respects operators' practical intelligence, links data points to shopfloor realities, and provides active, discovery-based interactions where data manipulation directly drives understanding.

### 2. What is the single strongest learning interaction in the application, and why?

**Stage 3 (Two Stories), coupled with Stage 4 (Deconstruction).**

Rather than passively showing an infographic about how charts can mislead, the activity challenges learners to actively create two conflicting impressions—crisis versus success—from the exact same figures. This reverse-engineering approach turns learners into active evaluators, building critical skepticism that directly serves Learning Outcome 2.

### 3. What is the single weakest part of the learning experience, and why?

**The synthesis handover between Stage 8 and Stage 9.**

Stage 8 offers three sentence starters intended to help workers formulate their own critical questions. However, providing one-click starter chips and allowing blank submissions turns what should be an active synthesis exercise into a passive copy-paste task. As a result, the printable note in Stage 9 reflects the developer's pre-written phrasing rather than authentic learner expression.

### 4. What are the three highest-value improvements?

1. **Require Active Synthesis in Stage 8:** Remove the instant-paste chips; replace them with expandable guiding questions, and require learners to type their own response (or confirm a skip) before moving forward.


2. **Fix Mobile Table Layouts in Early Stages:** Bring the responsive split-table layout from Stage 8 into Stages 1 and 2 to eliminate horizontal scrolling on mobile devices.


3. **Add Inline Action Prompts in Stage 3:** Add clear inline action buttons within the feedback panels so learners don't have to search for the bottom navigation bar.



### 5. What should the developer be prepared to justify or discuss during the interview?

* **Why starter chips were used in Stage 8:** Be prepared to explain the balance between supporting learners with low literacy and encouraging independent question formulation.


* **How 10 stages fit into a 10–20 minute window:** Justify the pacing and cognitive load for lower-confidence readers on short breaks, and explain how the design could support split sessions.


* **How AI tools were used during development:** Discuss the specific prompts used, what the AI initially got wrong (such as statistical jargon or complex layouts), and how instructional design judgement was applied to refine the final product.

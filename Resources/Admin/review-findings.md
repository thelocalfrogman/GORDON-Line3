
# CLAUDE

> **Documentation phase closed.** This file is complete as of 11 October 2026. At the candidate's
> direction, it will not be updated automatically in later sessions.

Review of the brief and project notes before building, 2026-10-11.

## Requirements traced to the build

| Brief requirement | Where it is met |
|---|---|
| 10&ndash;20 minutes of learner time | Seven screens, about 15 minutes |
| Standalone browser interactive, single HTML file, no SCORM | `index.html`, no dependencies, no build step |
| Learner actions change what they see | Every stage; no stage is read-and-continue |
| More than a quiz | No multiple-choice items at all |
| Difficulty progresses | Read &rarr; spot a break &rarr; presentation tricks &rarr; measurement tricks &rarr; decide |
| Figures must not be changed | Twelve rows and both notes reproduced exactly; derived figures shown with their arithmetic |
| Do not name or promote any AI product | No AI mention anywhere in the activity |
| Worked example before practice | Stage 1 opens with a completed match and its arithmetic |
| Expected effort 1&ndash;3 hours | See scope decisions |
| Weblink to the interactive | Outstanding &mdash; not yet hosted |
| Full prompt history including failed and discarded prompts | `prompt-history.md` |

## Learning outcomes

**"Read a simple table and chart and say in plain words what they show."**
Taught in stage 1 (worked example, then matching plain-words notes to weeks) and stage 2 (describing
the shape of a run of weeks). Evidenced by the three matches and by which week is selected in stage 2.

**"Spot at least two ways a table or chart can give a misleading impression."**
Five are covered, split across charts and tables. Presentation: a scale that does not start at zero;
choosing which weeks appear; an average pulled by one unusual week. Measurement: a percentage of a
larger number hiding a larger count; a measure whose definition changed partway through. Evidenced by
the learner constructing both misleading charts themselves in stage 3.

**"Decide what question they would ask before acting on the numbers."**
Taught in stage 2 (a reason is not the whole story), stage 4 (overtime and the new form), and stage 5.
Evidenced by which columns the learner chooses to open in stage 4 and in what order, and by the
sentences on the summary card.

## Points raised against the project notes

| Point | Outcome |
|---|---|
| The notes as written describe roughly 25&ndash;30 minutes of learner time and well over three hours of build | Pruned to the week 7 arc, the manipulation lab, the weeks 10&ndash;12 arc and the final decision |
| An always-available help wizard is expensive, and for low-confidence users it is another interface to learn first | Dropped for this demo by candidate decision; noted as a future addition |
| "Let them change the scale or which weeks are shown" risks pleasant fiddling with nothing learned | Turned into two challenges, so the learner commits the deception rather than observing it |
| "Not too focused on reading graphs" sits against learning outcome 1, which requires reading a chart and a table | Clarified by the candidate: reading is the floor, not the goal. Stage 1 stays, as a matching task |
| The notes' weeks 10&ndash;12 arc rests on overtime and the form change, and does not mention scrap | Scrap moved to the centre of that stage. It is the strongest thing in the supplied data |
| Saved progress conflicts with the shared computers the brief names | Dropped by candidate decision |
| Stages still felt like read-and-click after the first proposal | Candidate feedback. Each stage now has one manipulation that produces a conclusion |

## Learning moments identified in the supplied data

- **Week 7 is a break; week 5 is a wobble.** 3,650 against a 4,780&ndash;4,990 run. Week 5 earns its place precisely because it is the plausible wrong answer.
- **One bad week moves the average.** 4,844 against 4,953 without week 7, and a middle week of 4,920. "We averaged under 4,850" is accurate and misleading at the same time.
- **A scrap percentage hides scrap parts.** Week 12 is the best week on the sheet for units and binned about 134 parts; the storm week binned about 142 at 3.9%. Week 11 binned about 117 parts at 2.3% while week 5 binned about 115 at 2.4% &mdash; lower percentage, more parts.
- **Fault calls stopped being comparable at week 10.** New form, same week the numbers improved.
- **Output rose when hours rose.** Saturday overtime began in week 10 and hours are not on the sheet, so the learner can discover that a necessary figure is missing.
- **Scrap rose while everything else improved.** Three measures out of four tell a success story.

## Candidate feedback on version 1, and what was done

Tested manually in Firefox and Chrome, desktop and mobile. Function was fine; the issue was that the
activity was static, and each interaction meant scrolling down to read a result and back up again.

| Feedback | What changed |
|---|---|
| Keep the current task, the control and the feedback together on screen | Every stage reserves a fixed feedback slot beside or directly under the control that fills it, sized even when empty so nothing shifts. Controls and chart sit side by side above 860px. Measured: every stage now fits one viewport at 1280&times;900 and at 360&times;740 |
| Avoid adding content underneath on every click | One challenge at a time on the two-stories stage, replacing rather than appending. Revealed columns go into the table they belong to. One observation slot that is replaced, not stacked |
| More doing and discovering, less reading explanations | Word count fell from 2,073 to 1,808 while interactions increased. The investigation stage now has the learner reach the conclusion before anything is explained |
| Keep the colour scheme, add personality | Same palette. Added gridlines, axis ticks, tooltips, matched-bar colouring, in-table highlighting and trend arrows, progress dots, and 140&ndash;320ms transitions |
| Respect reduced motion; do not break keyboard or screen reader | All motion behind `prefers-reduced-motion`, verified by emulating the media feature. Focus restoration and the live region are unchanged and retested |
| Step 1: more visual interest, keep it obvious how to start | Sheet presented as a noticeboard panel beside the introduction |
| Step 2: matching is not obviously one activity; connection between note and chart unclear | Notes and chart side by side. Selecting a note puts the chart into a visible "choose a week" state with dashed outlines, and the task strip changes to name the note being placed. Matched weeks keep a green bar with the note's badge above it. Feedback sits under the chart |
| Step 3: let them investigate rather than being told week 7 is worst | Rebuilt. Free exploration of all four measures, gated on seeing all four, then one question: which week would you raise. Feedback, then the note, then an explicit reconsider step with two defensible answers |
| Step 4: target label hard to see at 4,600; check week 7 below baseline; tasks buried below the chart | Target moved to a legend above the plot. Week 7 clips at the baseline with a dashed cut edge, explained afterwards. One challenge at a time in the task strip above the controls |
| Step 4: explanations too text-heavy | Split into two short side-by-side panels and a hero average figure that changes when the toggle moves |
| Step 5: communicate the significance; highlight cells; explain week 10 clearly | Revealed cells highlight on arrival and carry trend colours and arrows. A rule marks week 10 in the table. Two short panels name the two confounds |
| Step 5: make the percentage versus parts difference more visually obvious | Replaced the toggle with two linked charts side by side. Clicking a week highlights it in both and shows the share and the parts count together |
| Step 6: learners cannot see the data while writing about it | The full sheet, including approximate scrap parts and both supervisor notes, sits beside the writing on desktop and above it on mobile, open by default on a wide screen and collapsed on a phone |
| Step 7: add a completion message, brief confetti, two large buttons, keep confetti off the printout | All four done. Confetti is suppressed entirely under reduced motion and excluded from print |

## Candidate feedback on version 2, and what was done

Tested manually in Firefox, Chrome and Safari, desktop and mobile. Interactions were working. The
issues were register, information density and use of screen space.

### General

| Feedback | What changed |
|---|---|
| Copywriting across the whole activity: complete, natural sentences, professional but not overly formal | Every heading, task, piece of feedback and explanation rewritten. "The week 7 sheet goes up" became "Finding the week that stands out". "So, on Monday?" became "Would you raise week 7 with your supervisor?". "That's the lot. Nicely done." became "You have completed the activity" |
| Feedback should not assume what the learner ought to do | The two answers on the week 7 decision now receive one shared response that sets out what the note does and does not establish, rather than a different verdict for each. No answer is treated as the better one |
| Cut the em dashes | Zero remain. Verified both in the source and in the rendered page text |
| More animation where it communicates something | Bars grow from the baseline with a staggered delay whenever the data behind a chart changes, which makes switching measures feel like data arriving. A matched note and its bar complete together. The task strip flashes when the stage moves to a new phase. Revealed panels rise in. The average line slides when the toggle moves. Progress dots animate |
| Keep it simple | No animation was added that does not mark a state change. Durations are 140ms for feedback, 230ms for state, 340ms for reveals |
| Use the available screen space | Steps 1, 3, 6 and 9 are now full width. The step 3 ranking table and the step 9 document and data both use the full column |
| Information density | Split from seven screens to ten. The two-stories stage became three screens, and the good-news stage became two |
| Split across more screens if it helps | Done, and the activity still measures inside the time allowance |
| Keep the accessibility work | Focus restoration, the persistent live region, chart-scoped focus keys, table twins and reduced-motion support all carried forward and retested |

### Step by step

| Feedback | What changed |
|---|---|
| Step 1: half the page empty while the table needed horizontal scrolling | Introduction and explanation at the top, table full width underneath |
| Step 1: separate the general explanation from what the learner does next | An "About this activity" panel covers the activity; a separate task strip states the next step and what the next screen will ask |
| Step 2: cannot see which bar the worked example matches | Week 3 now carries an "Example" badge on the chart, matching the card |
| Step 2: two overlapping dotted outlines when a note is selected | One dashed outline, offset from the bar. The inner white ring was removed |
| Step 2: target line overlaps the A, B and C labels | Match badges moved below the axis, under the week number, where no chart line can cross them |
| Step 2: make matching feel more satisfying | The card and its bar complete together: the card pulses, the bar pulses, and the badge drops in |
| Step 2: indicators must not rely on colour alone | Every badge carries text, selected bars carry `aria-pressed` and an inset ring, and the dashed outline is a shape change |
| Step 3: y-axis numbers overlap the chart heading on downtime and fault calls | Fixed. Measured clearance on every measure, currently 10 to 28px |
| Step 3: not obvious that you should now pick a week | Viewing the fourth measure changes the task strip, flashes it, turns the bars into visibly selectable targets, and announces the change |
| Step 3: ranking table squeezed into the right column | Full width, and expanded to show worst, second, third and best |
| Step 3: "So, on Monday?" | Now "Would you raise week 7 with your supervisor?" |
| Step 3: keep the feedback neutral whichever answer is chosen | One shared response, stating that both answers are reasonable |
| Step 3: stop moving the learner left and right | Single column, full width, top to bottom |
| Step 4: the side-by-side view becomes very busy | Split into three screens: the two challenges, then the comparison, then the average |
| Step 4: show the differences visually rather than in paragraphs | The comparison screen isolates each change behind its own button. The learner switches between the honest chart, the cut scale and the hidden weeks, and the bars animate between them |
| Step 4: figures outside the chart scale must be handled clearly | Selecting the cut-scale view highlights week 7 and raises a callout explaining that it produced 3,650, which is below the 4,600 baseline, so almost no bar is drawn and the chart gives no warning |
| Step 4: learners should understand the two methods, not just the button presses | Each change is now demonstrated on its own before being named |
| Step 5: same overload problem | Split into two screens |
| Step 5: keep the column reveal | Kept, with the target column restored so the claim about beating target can be checked |
| Step 5: scrap comparison as its own activity | Its own screen, with nothing above it |
| Step 5: make the relationship immediately obvious | Selecting a week shows the calculation on one line: the percentage, of the units produced, equals the approximate parts, with both charts highlighting that week |
| Step 5: keep the limitations clear | A panel states that parts are units multiplied by the percentage, that the sheet does not say how the percentage was worked out or whether units produced already excludes scrap, and that the figures are therefore approximate |
| Step 5: be careful about the fault form | Reworded. The activity now says only that the form changed and that the sheet does not say whether the new form records the same things, so nobody can yet know whether the counts are comparable. It no longer implies the counting method changed |
| Step 6: make it a part-written workplace note | Rebuilt as one document with a heading, a subject line, three part-written sentences each with a gap, and a closing line. Full width |
| Step 6: optional starters without three assessment questions | Each gap has one quiet "Show some examples" link that reveals three fragments |
| Step 6: keep the data accessible, not in a collapsible panel | The full dataset sits underneath the document at full width, with jump links both ways. Text is kept as it is typed |
| Step 6: readable figures on small screens without horizontal scrolling | Three narrower tables on small screens instead of one wide one. The `display:block` responsive pattern was rejected because it strips table semantics |
| Step 6: answers must flow into the printed notes | The printed card now renders the completed note as prose, with the learner's words inside the supplied sentences |
| Step 7: keep the completion animation and the two buttons | Kept, and the new note flows through to the printout |

## Candidate feedback on version 3, and what was done

Tested manually across devices and browsers with no issues found. Three specific changes requested,
plus a visual review.

| Feedback | What changed |
|---|---|
| Step 1 should feel like a proper landing page | Rebuilt as a welcome screen: what the activity is about, what you will do in five numbered steps, what you should get out of it, and how long it takes |
| Make the start obvious and visually separate | A bordered start block sits below the introduction with its own heading and a large button. The activity navigation is hidden on this screen, so there is exactly one way forward |
| Decide where the weekly figures belong | Moved off the welcome screen. A landing page that opens with a data table is not an introduction. The sheet now appears on the matching step, at full width underneath the activity, where the notes actually require downtime and scrap |
| Step 4: the "Go to challenge 2" button is not obvious enough | Removed from the page body. Challenge 2 is now reached through the main Continue button, which changes its label to "Go to challenge 2". One forward control for the whole activity, always in the same place |
| Instructions must match the completion logic | The scrap step asked for weeks 7 and 12 but accepted any two. It now requires both, and the task line and the navigation hint both name whichever is still missing |
| Visual review for overlaps, clipped text and tooltips | Carried out in the candidate's own browser and repeated at six viewport sizes. Five issues found and fixed |
| Check the fixed navigation is not obscuring anything | Checked on all ten screens at four viewport and zoom combinations. Nothing sits under it |
| No major changes without an actual issue | Every change above is either a direct request or a defect found by the review |

## Independent audit by ChatGPT, 11 October 2026

Commissioned by the candidate as a final data accuracy and quality assurance pass. The report is
preserved unchanged at `Line_3_Independent_Data_Audit.html`. It was supplied as `index(4).html` and
quotes SHA-256 `bd8ee199…0280d6`; that hash matches the working file byte for byte, so every finding
applied to the live code and none were stale.

The audit confirmed all 60 source values and the target against the brief, confirmed the arithmetic
(total 58,130; mean 4,844.1667; mean without week 7 4,952.7273; median 4,920; all twelve scrap
estimates), and raised 8 defects and 3 informational observations. It ran 320 assertions in a Node
harness with a stubbed DOM. That is a source-level test, not a browser test, and nothing in this
section treats it as one.

### Assessment of each finding

| ID | Audit severity | My assessment | Action |
|---|---|---|---|
| DATA-001 Scrap estimates presented as counts before the assumption is given | High | **Accepted in full.** Reproduced: selecting week 1 shows "about 101 parts" with the caveat panel still hidden, because it was gated on weeks 7 and 12 both being picked. The lede asserted the denominator outright. The claim that real figures "will differ slightly" was unsupported: one alternative definition happens to differ by about 6 parts, but nothing on the sheet constrains the others | Assumption panel moved above the charts and shown from first render; wording changed to estimates throughout; both comparisons made conditional; the smallness claim removed and replaced with the rounding caveat |
| DATA-002 Median described as the middle week | Medium | **Accepted.** Verified: sorted positions 6 and 7 are 4,910 and 4,930, and no week produced 4,920. Chronological weeks 6 and 7 produced 4,990 and 3,650, so "middle week" was wrong twice over | Explanation now names the sort and the two middle figures. The two values are derived from the data, not typed |
| DATA-003 Printout attaches the week 7 decision to a different week | Medium | **Accepted.** Reproduced across all seven weeks and both answers. Investigating week 5 and answering "no" printed the storm sentence directly beneath the week 5 figures | Split into two records: the week investigated, and the decision about week 7, which now names week 7 |
| DATA-004 Suggested sentence says week 7 was below on every measure | Medium | **Accepted.** Week 7 has the lowest units but the highest downtime, fault calls and scrap percentage | Replaced with a sentence that states the direction correctly, and verified through to the printout |
| DATA-005 Downward arrow on unchanged week 12 downtime | Medium | **Accepted, with a wider fix.** Weeks 11 and 12 both recorded 8 hours. The logic was positional (`n >= 10`) rather than comparative, so it happened to be right for fault calls and scrap by coincidence | Arrows now compare each week with the one above, show nothing when unchanged, and the table says so |
| DATA-006 Storm note treated as a complete explanation | Medium | **Accepted.** "The note explains why the parts were not produced" and the label "No, the note explains it" both asserted more than the brief supports | Reworded to "may help explain", the shortfall of 1,350 units is named as unaccounted for, and the answer label is now "No, I would not raise it for now". Both answers remain valid |
| DATA-007 Rank explanation contradicts its own table | Low | **Partially accepted.** I do not accept the sentence was factually incorrect: "being worst on all four is not what separates week 7 from week 5" meant that being bad on every measure is a property both share. But it sat next to a table that ranks them differently, so it read as self-contradictory. The audit's point about clarity stands | Reworded to say the ranking gives the order but not the size of the gap |
| DATA-008 Fictional data described as a real quarter | Low | **Accepted.** The brief's Context section calls Ridgeway Components a fictional manufacturer | Now "12 weeks of example figures from that sheet" |

### Informational observations

| ID | Assessment | Action |
|---|---|---|
| INFO-001 The truncated chart and the week 7 stub | **Partially accepted.** The existing callout already said the chart gives no warning, but "Nothing has been removed" could be read as the encoding being faithful, and the stub was never identified as not being week 7's value | "All 12 weeks are still on the chart", and the callout now says the marker is not its value and points to the table showing 3,650 |
| INFO-002 Completion and exposure tracking | **Partially accepted.** The comparison counter said "0 of 3 versions" while the first version was on screen, which is a false statement about what the learner had seen. The average screen's own instruction asks the learner to switch week 7 in and out, but allowed Continue without it | Counter now starts at 1 and counts the view on screen. The average screen is gated on one toggle. No new tracking was added, and the optional note stays optional |
| INFO-003 Invented workplace history | **Accepted.** "Nobody has raised week 5" is not in the brief and the application cannot know it | Clause removed |

### Nothing rejected outright

Seven findings were accepted as stated, one (DATA-007) was accepted as a clarity problem while
disputing that it was factually incorrect, and the three informational observations were partly
acted on. No finding was dismissed.

## Second independent audit round, 11 October 2026

Two further independent reviews were commissioned by the candidate. Both reports are preserved
unedited: `Line_3_Final_Regression_Audit - GPT.html` and `Gemini_Audit.md`. Neither set of findings
is mine.

Both reviewed the same build: 1,666 lines and 87,456 bytes, matching the working file exactly, and
the regression audit's hash for the candidate brief (`098585a3…`) matched the brief in this
repository.

### ChatGPT regression audit: PASS WITH QUALIFICATIONS

Confirmed all eight earlier findings resolved, all 60 source values and the target preserved, and
all derived figures correct. Raised one new Low defect and one optional wording item.

| ID | Assessment | Action |
|---|---|---|
| REG-001 Average gate satisfied by clicking the already-selected button | **Accepted.** Reproduced: `toggled` was set unconditionally, so clicking "Include week 7" enabled Continue without the excluded average ever being displayed | The flag now only records seeing the excluded state, which is the half the learner has not been shown. Renamed `sawExcluded` so the name matches the meaning. Hint reworded to name the control |
| Spoken scrap wording out of step with the screen | **Accepted.** The announcement said "is about N parts" while the screen said "an estimated N parts" | Announcement now says "gives an estimated N parts, on the assumption stated above" |

The audit's other observations (precision wording, print pagination, generic chart wording) were
explicitly not confirmed defects and no change was made.

### Gemini instructional design review: READY WITH QUALIFICATIONS

| ID | Assessment | Action |
|---|---|---|
| F-01 Blank submission and unearned synthesis (High) | **Accepted, implemented to the candidate's brief rather than Gemini's.** Gemini proposed requiring text before progression. The activity is deliberately ungraded and aimed at people with low literacy and digital confidence, so a hard gate was rejected. Instead: the example chips no longer paste a finished sentence and are now a read-only list of examples; finishing with all three gaps empty prompts once, with an explicit "Continue without writing anything" control; and the printout is split into three labelled sections so the learner's own words are never confused with supplied content | Implemented |
| F-02 Keyboard focus on chart columns (Medium) | **Partially accepted.** The stated mechanism did not reproduce: there is no `overflow:hidden` ancestor anywhere above a bar, and the ring draws 4 to 5px outside the plot without being cut. Gridlines sit behind the focus ring, not over it. What is real is that the ring surrounded the full-height column, so on a short bar it did not show which value was focused | The column is now tinted to show the hit area and the bar itself carries the ring. One ring, not two. Verified it also beats the dashed "choose a week" outline when both apply |
| F-03 Missing `aria-expanded` (Medium) | **Accepted.** Confirmed: zero occurrences in the file | Added, with `aria-controls`, and toggled in the handler |
| F-04 Undisclosed mobile table scrolling (Medium) | **Accepted.** Confirmed: 226px of the six-column table was hidden at 360px with no indicator, and the scroll container was not keyboard reachable | Tables that actually overflow now get a visible hint, an edge shadow, and `role="region"` with a label and `tabindex="0"`. Applied only where a table really overflows, so nothing appears on desktop. The candidate's warning against splitting related figures was followed: stages 1 and 2 keep one table |
| F-05 Fault call units (Low) | **Accepted**, as the candidate allowed | Now "7 fewer calls, a drop of about a third" |
| F-06 Challenge navigation (Low) | **Not implemented.** Gemini proposes adding an inline button beside the feedback. That is exactly what was removed in the previous iteration at the candidate's request, who asked for one forward control and no duplicate navigation | Instead the task strip now names the control: "Select Go to challenge 2 at the bottom of the screen." No second button |
| F-07 Remove the confetti (Informational) | **Not implemented.** The candidate specifically asked for a brief completion animation and is happy with it. It is already suppressed entirely under `prefers-reduced-motion` | No change |

### Gemini's completion time estimate

Gemini suggests the activity may take considerably longer than 15 to 20 minutes for less confident
learners. That is plausible but is not based on measured testing with real learners, and the
candidate's instruction was not to redesign around it. Recorded as a risk in design-decisions.md.

## Independent verification, in summary

Three independent reviews were commissioned by the candidate within the time available for this
demonstration. All three reports are preserved unedited in this directory.

| Review | Tool | Shared conversation | Verdict | Outcome |
|---|---|---|---|---|
| Data and statistical accuracy | ChatGPT | https://chatgpt.com/share/6acb3271-30f8-83ec-8824-b7051e1fb2d3 | Revisions required: 1 High, 5 Medium, 2 Low, plus 3 informational | All 8 accepted, 1 of them partially. Corrected in version 5 |
| Final data regression | ChatGPT | https://chatgpt.com/share/6acb3271-30f8-83ec-8824-b7051e1fb2d3 | Pass with qualifications: all 8 earlier findings resolved, 1 new Low defect | Both items accepted and corrected in version 6 |
| Instructional design and learning experience | Gemini | https://share.gemini.google/CdfsaoNilIRA | Ready with qualifications: 1 High, 3 Medium, 2 Low, 1 informational | 4 accepted, 1 partially accepted, 2 not implemented with reasons recorded |

**These were AI-assisted reviews, not manual testing and not user testing.** Both ChatGPT audits ran
the application's JavaScript in a Node harness with a stubbed DOM; the second reported 887
assertions and 152 checks on generated output. Those are source-level checks. Neither audit opened a
browser, used assistive technology, or printed anything. The Gemini review was a source and rendered
inspection. The candidate separately carried out manual walkthroughs in Firefox, Chrome and Safari
on desktop and mobile, which is the only human testing this resource has had.

What the reviews did establish: all 60 supplied values and the target are preserved, the derived
figures are arithmetically correct, and the data-handling logic behaves correctly across the
combinations they exercised. What they did not and could not establish: screen reader behaviour,
real device behaviour, physical print output, or whether the activity works for its intended
audience.

## Open items

- The interactive is not yet hosted, so there is no weblink to submit.
- Version 1 was tested manually by the candidate in Firefox and Chrome, desktop and mobile. Version 2 was tested in Firefox, Chrome and Safari, desktop and mobile, with no issues found. Version 3 has not yet been tested by hand.
- **No screen reader testing has been carried out by anyone, and none has been possible for this demonstration.** This remains the largest outstanding limitation.
- Nobody from the target audience has tried it.

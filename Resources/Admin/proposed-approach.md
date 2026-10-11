# Line 3 — Proposed approach (pre-build)

Status: proposal for sign-off. No code written yet.
Source of truth: `Candidate_Brief_Read_the_Numbers.docx` (takes priority), then `Init-Project-Notes.md`.

## 1. Requirements check against the brief

| Brief requirement | Covered by |
|---|---|
| 10–20 min learner time | 7 short screens. Measured at 2,062 words; 15–20 minutes depending on reading speed |
| Standalone, runs in a browser, single HTML file, no SCORM | One `index.html`, inline CSS/JS/SVG, no build step, no libraries |
| Learner actions change what they see | Clicking bars, revealing columns, setting chart controls — all stages |
| More than a quiz | No multiple-choice items at all (see §4) |
| Difficulty must progress | Read → spot a break → presentation tricks → measurement tricks → decide |
| Tables or charts allowed, figures must not change | All 12 weeks exactly as supplied, held in one data object |
| Do not name or promote any AI product | No AI mention anywhere in the activity |
| 1–3 hours effort, clear thinking over polish | Scope cuts listed in §8 |
| Worked example before practice | Stage 1 shows a worked read-aloud before the learner tries one |
| Submit prompt history incl. failed/discarded prompts | `Admin/prompt-history.md` — currently empty, see §9 |

## 2. Designing for these learners

Experienced workers, low computer confidence, time-poor, possibly on a phone or a shared machine, some sceptical of training.

- **One interaction grammar, learned once.** The same chart component is reused in every stage; controls appear only when a stage needs them. Learners never have to work out a new interface mid-activity.
- **You always click the data.** Bars and columns are the primary input. No drag, no modals, no wizard.
- **One instruction visible at all times**, present tense, plain English, ~12 words. One primary button per screen.
- **Respects their expertise.** The framing is "you work on Line 3, here are your numbers" — the activity never explains manufacturing to them, only how numbers can mislead.
- **No scores, no badges, no streaks.** Final screen says plainly that nothing is graded.
- **Accessibility built in, not bolted on:** bars are real `<button>`s with accessible names ("Week 7, 3,650 units, target 5,000"), a table view of every chart, visible focus rings, 44px touch targets, `aria-live` for feedback, never colour alone (pattern + label), tested keyboard-only and at 360px wide.

## 3. Proposed flow

The activity walks forward in time, so the data arrives as it would on the noticeboard rather than all at once.

**Stage 0 — The noticeboard.** Weeks 1–6 as the supervisor posts them. Sets the scene, says nothing is scored or saved, one Start button.

**Stage 1 — What do the numbers say?** Weeks 1–6. A worked example is already matched for them (*"We finished 130 short, and the line was down 13 hours"* → week 3, with the subtraction shown). The learner then matches three more notes to weeks by clicking a note and clicking a week. Wrong matches reply with that week's own figures rather than "incorrect". No typing.

**Stage 2 — Week 7 is in.** Weeks 1–7. "Click the week you'd ask your supervisor about." Every week gets reasoned feedback. Then a measure switcher (units, downtime, fault calls, scrap) so the learner can check whether the week is bad on everything or just one thing — it is bad on everything, which is what makes it a real event. Axis stays locked at zero here. Then the storm note unlocks.

**Stage 3 — Same numbers, two stories.** All 12 weeks. Two controls: where the scale starts (0 or 4,600) and which weeks show (all / 1–7 / 8–12). Two challenges: *make this look like trouble*, then *make the same data look like a success*. A live caption under the chart names what the current settings are doing, at the moment the learner causes it. Then both versions side by side: "Same 12 numbers. Nothing was changed." The average lands here as a toggle — include week 7 or not — so the number changes on screen: 4,844 / 4,953, with the typical week at 4,920.

**Stage 4 — When the good news is the problem.** Weeks 8–12, units only. The learner clicks to add downtime, fault calls and scrap one at a time; each reveal gets its own feedback. Three measures improve, one gets worse. Then the week-10 note unlocks: Saturday overtime began, and fault calls moved to a new form. Then the scrap view widens to all 12 weeks with a % / parts toggle.

**Stage 5 — Monday morning.** Three optional sentence stems — what the numbers show, what the sheet can't tell you, what you'd ask before acting — each with fragment starters the learner finishes. Produces a printable card.

## 4. Meaningful interaction, with assessment

No multiple choice anywhere. Every stage has one real manipulation that produces a conclusion, rather than a click that produces an explanation:

1. **Match notes to weeks** (stage 1) — connects figures to meaning in both directions, and forces cross-column reading. Auto-checked, evidences LO1.
2. **Switch measures to test the break** (stage 2) — the learner cross-checks week 7 across all four measures and concludes it is real. Sets up stage 4, where the measures disagree.
3. **Construct the misleading chart** (stage 3) — to pass, the learner has to build it themselves. Hardest thing here to fake. Plus the average toggle, where removing one week moves the figure on screen.
4. **Change the unit** (stage 4) — choosing which columns to open, then flipping scrap from % to parts and watching the chart change shape.
5. **Finish the sentences** (stage 5) — scaffolded stems, not a blank box.

One free-text stage, at the end, where the typing produces something they keep. Never pretended to be marked. Stems come with sentence fragments to start from, deliberately unfinished so they are scaffolding and not answers in disguise.

## 5. Learning outcome map

| Outcome | Where it's taught | Where it's evidenced |
|---|---|---|
| Read a simple table and chart and say in plain words what they show | Stage 1 worked example; stage 2 describing the shape of 12 weeks | Stage 1 numeric gap; stage 2 week choice |
| Spot at least two ways a table or chart can give a misleading impression | Stage 3: cut-off scale, cherry-picked weeks, average vs typical week. Stage 4: a percentage of a bigger number, and a measure whose definition changed | Stage 3 both challenges completed by the learner; stage 4 column reveals |
| Decide what question they would ask before acting on the numbers | Stage 2 (a reason isn't the whole story); stage 4 (overtime and the new form); stage 5 | Stage 4 evidence choices; stage 5 note |

Three ways to mislead with presentation and two with measurement — comfortably past "at least two", and split across charts *and* tables.

## 6. The learning moments in the supplied data

- **Week 7 is a break, not a wobble.** 3,650 against a 4,780–5,150 spread, downtime 38 hrs against 8–16. Teaches signal vs noise.
- **Week 5 is a wobble.** 4,780 and 16 hrs downtime — the worst normal week. Useful precisely because it's *not* the answer in stage 2.
- **One bad week moves the average.** 4,844 mean, 4,920 median, 4,953 without week 7. A supervisor saying "we average under 4,850" is accurate and misleading at once.
- **Scrap percentage hides scrap parts.** Week 12 is the best week on the board for units and scrapped about 134 parts; the storm week scrapped about 142 at 3.9%. Week 11 scrapped about 117 parts at 2.3%, more than week 5 scrapped at 2.4% — a straight reversal. The percentage fell out of a bigger number. For people who think in parts rather than percentages this is the most transferable idea in the activity. Note that this only shows when weeks with different output are compared: across weeks 10–12 alone, output barely moves, so percentage and parts rise together and the comparison teaches nothing. The reveal therefore runs across all 12 weeks, with week 7 in frame.
- **Fault calls stopped being comparable at week 10.** New form, same week the numbers improved. You cannot compare across that line.
- **Output rose when hours rose.** Saturday overtime began week 10. Units per hour is not in the data — which makes "how many hours did we work?" a question the learner can genuinely discover is missing.
- **Scrap rose while everything else improved.** Weeks 10–12 look like a clean success story on three measures out of four.

On the "don't change the figures" rule: the scrap-in-parts moment shows the arithmetic on screen ("2.6% of 5,150 = about 134 parts"), so the same supplied figure is shown two ways rather than a new figure being invented. The "about" is honest — whether units produced is before or after scrap isn't stated in the brief, and that ambiguity is itself a fair question for a learner to raise.

## 7. Challenges to the notes

**The help wizard — dropped for this demo,** on the candidate's decision, with an optional guide noted as a possible future addition. For someone low in computer confidence a wizard is one more unfamiliar thing to learn before they can start, and it was the single most expensive item in the notes. Replaced by an interface that doesn't need explaining: one instruction on screen at all times, one primary button, the same click-the-data action throughout.

**The free-roam chart needs a task.** "Let them change the scale and the weeks shown" risks pleasant fiddling with nothing learned. Turning it into two challenges — *make it look bad, now make it look good* — means the learner commits the deception themselves, which is far stickier than watching it happen.

**"Not too focused on reading graphs."** Clarified by the candidate: the concern is that the activity shouldn't consist of looking at static charts, not that reading comes second. Reading accurately is the floor that interpreting and questioning stand on. Stage 1 therefore stays, but as a matching task rather than a reading task.

**The notes don't mention scrap in weeks 10–12.** The week 10–12 arc in the notes rests on overtime and the form change. Scrap climbing to its second-highest level across those same weeks is the strongest thing in the data and belongs at the centre of that stage.

**No saved progress.** The notes imply short sessions, but the brief also names shared computers. Saving answers means the next worker can see the last one's. A 15-minute activity doesn't need resume — a visible "Start again" is enough, and it's dev time back.

**Prune the activity list.** Taken together the notes describe roughly 25–30 minutes of learner time and well over three hours of build. The flow above keeps the week 7 arc, the manipulation lab, the week 10–12 arc and the final decision, and drops the wizard, saved progress and a separate free-explore mode.

## 8. Scope control

In: one HTML file, one data object, one reusable chart, six stages, inline SVG, no dependencies.
Out: saved progress, help wizard, animation beyond simple CSS transitions, chart library, scoring, any marking of prose, units-minus-scrap net-output comparison (considered and cut — too subtle for 15 minutes).

## 9. Assumptions and open questions

Australian English. Ridgeway Components / Line 3 as the only branding. Summary card is print-only (no clipboard, on the candidate's decision).

Resolved 2026-10-11:
1. One free-text box kept, at stage 5 only, producing the summary card. No typing anywhere earlier.
2. Admin files maintained alongside the build — prompt history, design decisions, testing results and review findings, including discarded approaches.

3. Admin files: anything added by the assistant sits under a `# CLAUDE` heading, factual, and is not written as the candidate's own reflections or decisions unless the candidate stated them.

## 10. Build decisions

- Bars are real HTML `<button>` elements with CSS-set heights, not SVG. Native focus, native keyboard handling, native touch targets, and less code. The clickable area is the full column height so it never falls below 44px regardless of bar height.
- One chart function handles measure, scale base, week range, unit (% or parts), and interactive vs static. Reused in every stage.
- Each measure carries a direction label ("Higher is better" / "Lower is better") that switches with it, because units is good-high while downtime, fault calls and scrap are good-low. Without it a bar chart would mis-train the reader.
- Stage 2's axis is locked to zero. A learner stumbling onto a truncated scale before stage 3 names it would spend the reveal.
- Every chart has a "Show as table" toggle.
- Cut from the plan: a third stage 3 task asking the learner to set the view a quoted email was based on. The two challenges already do that work.
- Cut and recorded: comparing units minus scrap across weeks 10 and 12. Too subtle for 15 minutes.

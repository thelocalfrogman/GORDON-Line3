
# CLAUDE

Prompt history for the Line 3 interactive. Session of 2026-10-11, Claude Opus 5 via Claude Code.

The brief asks for the full history including failed attempts and discarded prompts. This file
records the candidate's prompts verbatim, what the assistant did in response, and what was wrong
with the output. Approaches that were proposed and rejected are recorded here too, because the
rejections are part of the history.

---

## Prompt 1 &mdash; planning, no code

> Go through everything in /Resources, including the original project brief and my own project notes.
>
> I want to build this as a standalone interactive learning activity, keeping things fairly simple technically but making sure the actual learning experience is good.
>
> Before we start building anything, I want you to:
>
> - Go through the requirements and make sure we're not missing anything
> - Look at the audience and how we can make the activity as approachable as possible for them
> - Come up with a proposed flow for the activity, including what the learner actually does at each stage.
> - Think about how we can make the interactions meaningful (avoiding things like asking multiple-choice questions) while keeping some form of assessment of knowledge
> - Map out how we're meeting each of the three learning outcomes
> - Identify anything in the supplied data that would make a good learning moment
> - Flag anything in my notes that you think doesn't make sense or could be approached better
>
> Don't write any code yet.
>
> Give me your proposed approach and the reasoning behind it. I'm happy for you to challenge my ideas if there's a better way to achieve the learning outcomes. I expect you to come back to me with questions to clarify anything if needed.
>
> Keep in mind the expected 1&ndash;3 hours of development effort. I don't want to over-engineer this.

**Response:** read the brief and notes, wrote `proposed-approach.md` with a six-stage flow, an
outcome map, the learning moments in the data, and six challenges to the notes. Asked two questions
(free-text in or out; whether to maintain the Admin files).

**Problems with the first proposal, caught before it was sent:**

1. The scrap-in-parts moment &mdash; the strongest item in the dataset &mdash; was worked out and then
   dropped over an ambiguity about whether "units produced" is counted before or after scrap. Wrong
   call: the ambiguity is itself a good question to hand the learner. Promoted to the centre of stage 4.
2. Stage 4 was going to be a "pick two questions you'd ask" list. That is multiple choice with a
   different label, which is exactly what the candidate ruled out. Replaced with column-reveal, where
   the learner's choice of what evidence to look at *is* the answer.
3. Three free-text boxes were planned for a time-poor audience possibly working on a phone. Cut to one.
4. `localStorage` resume was planned despite the brief naming shared computers, which would leak one
   worker's answers to the next. Cut.
5. Six clarifying questions were drafted. Four had obvious defaults and did not need asking. Cut to two.

---

## Prompt 2 &mdash; revisions, then build

> Your proposal looks sensible overall. A few notes before we move into the build:
>
> The stages still feel a little too "read and click" in places. I want learners to actually interact with the data and come to conclusions, rather than just clicking something and reading an explanation. Particularly in Stage 1, instead of clicking a week and typing the gap to target, could we have them make a connection between the numbers? Maybe selecting matching figures or variations, something along those lines. Keep it simple and accessible though, no need to overcomplicate it with drag-and-drop if clicking two options achieves the same thing.
>
> I like the two controls in Stage 3. That sounds like exactly the kind of interaction I'm after. Just make sure we're not only letting people manipulate the chart, but also helping them understand why the different presentations can be misleading.
>
> For the Monday morning stage, I'd like to give learners a bit more structure rather than just leaving them with a blank text box. Maybe an optional fill-in-the-blank style card that guides them through what the numbers show, what context might be missing and what question they'd ask before making a decision.
>
> For this demo, I'll take your recommendation to drop the help wizard. I still think an optional guide could be useful in a future version for people who aren't confident navigating online learning, but I agree it's extra complexity we probably don't need right now.
>
> Agreed on LO1. My point about not focusing too heavily on reading graphs was just that I don't want every activity to consist of looking at static charts. There's no point moving into interpreting and questioning the data if the learner can't accurately read it first.
>
> No accounts or saved progress needed for this demo. Those are things we could consider if this were developed further or integrated into an LMS.
>
> For the final summary card, let's just make it printable.
>
> Keep the Admin files updated as we go. For anything you add to those files, put it under a "# CLAUDE" heading so I can add my own notes above it. Keep the notes factual and don't write them as though they're my personal reflections or decisions unless I've actually stated them.
>
> Make those adjustments to the proposed approach first, then go ahead with the first working build.
>
> Keep it simple technically and prioritise the actual learning experience over visual polish. Once the first version is built, give me a rundown of what's implemented, any compromises you've made and anything that still needs reviewing or testing.

**Response:** updated `proposed-approach.md`, then built `index.html` and tested it.

**Problems caught before writing code:**

1. The scrap %/parts toggle was planned for weeks 8&ndash;12 only, described as making "the story
   invert". It does not. Output barely moves across weeks 10&ndash;12, so percentage and parts rise
   together and the learner would flip the control and see nothing change. The inversion only exists
   when weeks with different output are compared, so the reveal was moved to all twelve weeks with
   week 7 in frame.
2. Stage 5's chips were drafted as complete thoughts ("I'd ask how many hours we worked in weeks 10
   to 12"), which is a multiple-choice option with a cursor in it. Cut back to fragments that stop
   before the point.
3. Stage 1's note B ("our lowest week, down the longest") was not scoped to weeks 1&ndash;6 and would
   have become false once week 7 appeared. "So far" added.
4. The measure switcher had no direction label. Units is good-high and the other three are good-low,
   so a bar chart that switches between them without saying so actively mis-trains the reader.
5. Stage 3's "in trouble" check originally accepted a truncated scale with all twelve weeks showing.
   That view reads as *recovery*, not trouble. Tightened, with nudges so a near-miss still teaches.
6. A stage 3 task asking the learner to set the view a quoted email was based on was cut, to protect
   the time budget. The two challenges already do that work.

**Problems found by testing, after the code was written:**
See `testing-results.md` for the full list &mdash; eight faults, including focusable bar buttons that
did nothing on two stages, unreadable text on completed items, and a stage 1 chart that could not
answer its own question because six weeks within 210 units of each other look identical from a zero
baseline.

---

## Notes on working method

Testing was automated because the browser extension was not available: headless Chromium driven over
the DevTools Protocol, scripted walkthroughs at desktop and 360px, plus a separate script that
recomputed every figure the activity states on screen and compared it against the text. All figures
passed. The walkthroughs found the eight faults above.

No testing has been done by hand on real devices, in Firefox or Safari, or with a screen reader.

---

## Prompt 3 &mdash; second iteration: interaction and layout

Candidate had manually tested version 1 in Firefox and Chrome, desktop and mobile. Everything
worked. The feedback was about user experience, not function.

> I've gone through the first version manually in Firefox and Chrome on both desktop and mobile, and I've got some feedback for the next iteration.
>
> Overall: the learning structure is good and the functionality is in the right direction. My main issue is the actual user experience. It's very static at the moment, and too much of the activity involves clicking something, scrolling down to see what happened, reading a block of text, and then scrolling back up.
>
> For learners with low digital confidence, I think that's going to become confusing quickly.
>
> I don't want to rebuild everything or introduce a JavaScript framework. Keep the existing simple architecture, but take a look at the design skills available on my system and see how we can use them to make this feel more interactive and intuitive.
>
> A few general things:
> - Keep it simple stupid. I don't want animations and design elements just for the sake of having them
> - Use subtle transitions, highlighting, progressive reveals and visual feedback where they actually help someone understand what's happening
> - Try to keep the current task, the thing they're interacting with and the resulting feedback together on screen as much as possible
> - Avoid adding more content underneath the existing content every time someone clicks something
> - I want the learner to be doing and discovering more, rather than reading explanations that tell them what they should have discovered
> - Keep the current colour scheme broadly the same. I like it, it just needs a bit more personality and interactivity
> - Make sure any animations respect reduced-motion preferences and don't interfere with keyboard or screen reader accessibility
>
> *(Step-by-step feedback followed &mdash; recorded in full in review-findings.md.)*
>
> Before you start changing code, take a look at the design skills available on my system and briefly tell me how you intend to approach the improvements, particularly how you'll reduce scrolling and bring feedback closer to the interactions.
>
> Then implement the changes and test them. I want to review the next version manually before we move to the final audit.

**Skills consulted:** `dataviz` (chart form, marks, interaction, anti-patterns) and `impeccable`
(craft floor, Operate mode, motion guidance).

**Guidance deliberately not followed, and why:**

1. `dataviz` lists "a number on every data point" as an anti-pattern, with "let the axis and tooltip
   carry the rest" as the remedy. Neither works here. From a zero baseline with a 4% spread, axis
   ticks do not separate 4,820 from 4,870, and a tooltip cannot answer "which week is lowest?"
   without hovering every bar. Version 1 testing had already established by screenshot that the
   matching task was unanswerable without the labels. Labels kept on charts of seven bars or fewer;
   tooltips added to the twelve-bar charts where labels do not fit, with keyboard focus showing the
   same content.
2. `impeccable`'s craft floor lists 4px coloured left borders and Unicode glyphs standing in for
   icons among its refusals. The candidate pinned the look ("keep the current colour scheme broadly
   the same, I like it") and asked for no design changes made for their own sake. The skill states
   that a pinned brief overrides it, so both stay. The nested panel-inside-panel it also flags was
   fixed, because that one was structural and fed the scrolling problem.

**Problems caught before writing code:**

1. The first plan was to switch from re-rendering the whole panel to updating individual slots.
   That would have broken the focus restoration and the live region built in the previous
   iteration, both of which were verified empirically, in order to solve a problem that was about
   layout rather than rendering. Abandoned; the render model is unchanged.
2. The first plan for the investigation stage had the learner pick the worst week for each of four
   measures. Week 7 is the answer all four times, so that is the same click repeated four times.
   Replaced with free exploration followed by a single commitment.
3. Checking the data for that stage produced the strongest finding of the project: every measure
   ranks the weeks in almost the same order, and week 5 is second worst on all four. So "worst at
   everything" does not separate week 7 from week 5 &mdash; the size of the gap does. That became
   the lesson of the stage, replacing a weaker one.
4. The first plan marked week 7 loudly when it fell below the 4,600 baseline. That partly defuses
   the deception the learner is being asked to build. It now clips quietly during the challenge and
   is called out afterwards.

**Problems found by testing:** nine, listed in testing-results.md. The notable ones were a grid
overflow that made the whole page shrink-to-fit on a phone and masked every mobile measurement, and
completed buttons rendering white text on a pale green background.

---

## Prompt 4 &mdash; third iteration: copywriting, density and layout

Candidate had reviewed version 2 manually, this time including Safari. The interactions were working;
the remaining problems were register, information density and use of screen space.

> I've gone through version 2 and I think we're getting closer. The interactions are definitely better, but I've still got some feedback on the layout, copywriting and how much information we're giving learners at once.
>
> A few general things first:
> - Go through the copywriting across the whole activity. Put yourself in the position of someone developing workplace training. Would you really use headings like "The week 7 sheet goes up" or phrases like "So, on Monday?"? I'd prefer complete, natural sentences that are still easy to understand. Professional but not overly formal
> - Similar thing with explanations like "Fair, the number is explained, and chasing an explained week wastes everyone's time." It feels a bit too conversational and makes assumptions about what the learner should do. Keep the feedback practical and respectful
> - Please cut back on or totally cut out the em dashes throughout the activity. They're being overused
> - Don't be afraid to introduce a little more animation. The design skills are there for a reason. I'd like the charts and interactions to feel more responsive, particularly when switching between data, revealing information or completing an activity
> - Still keep it simple though. Animations should help communicate something, not just make the page look busy
> - Use the available screen space properly. There are places where we're squeezing information into narrow columns when we have plenty of unused space
> - Information density is probably the biggest issue remaining. Some stages are doing too much at once, and I don't want learners to be overwhelmed with multiple charts, controls, tables and explanations all on one screen
> - Don't be afraid to split an activity across an additional page if it makes the experience easier to follow. Just keep the overall activity within the 10 to 20 minute requirement
> - Keep the accessibility work from the previous versions, including keyboard navigation, focus management and reduced-motion support
> - I've also tested the activity in Safari this time and didn't encounter any issues. Screen reader testing still hasn't been possible for this demo, so keep that documented as a limitation
>
> *(Detailed step-by-step feedback followed, recorded in full in review-findings.md.)*
>
> For this next version, I'd prioritise making the experience easier to follow over adding more features. If that means moving from seven screens to nine, that's fine, provided each screen has a clear purpose and we're still within the expected completion time.
>
> Please review the relevant design skills again and apply them where useful. Keep the one-file approach with no frameworks or dependencies.

**Skills consulted again:** `dataviz` (`interaction.md` and `marks-and-anatomy.md`, not previously read)
and `impeccable` (`animate.md`, Operate mode).

**Applied from the skills:** bar width capped so a bar never fills its slot; hovered marks respond;
tooltips on the charts whose bars are too narrow for labels, with the same content on keyboard focus;
gridlines kept solid and recessive; motion durations of 140ms for feedback, 230ms for state and 340ms
for reveals on an exponential ease-out, with one authored moment per interaction rather than scattered
effects.

**Problems caught before writing code:**

1. The first plan rewrote the chart geometry to add a headroom factor so value labels could sit above
   the bars, following the skill's "label on the cap" spec. That would have touched the bar, gridline,
   target line, mean line and axis positioning all at once, in service of a spec rather than any
   feedback the candidate gave. Both "use the space" complaints were about tables, not bars. Reduced
   to capping bar width, which is one CSS declaration.
2. The first plan used the `display:block` responsive table pattern for the data sheet on small
   screens. That pattern strips a table's implicit ARIA role in Chrome and Safari. With screen reader
   testing already the largest untested risk, that is the wrong place to take an unverified bet. The
   sheet is split into three narrower tables on small screens instead, which keeps the semantics.
3. A word budget was set before writing rather than measured afterwards, because converting terse
   fragments into complete sentences and adding three screens both push the reading time up, and
   20 minutes is a hard ceiling in the brief.

**Problems found by testing:** six, listed in testing-results.md. The notable one was that the
x-axis labels no longer lined up with the bars once the plot became width-capped, which is exactly
the class of error the bar-width change risked introducing.

---

## Prompt 5 &mdash; final refinements before submission

Candidate had reviewed version 3 and was satisfied with the direction. Three specific changes, a
visual review, and a request to document future work rather than build it.

> I've gone through version 3 and I'm pretty happy with where we're at now. The learning experience is much closer to what I had in mind, and I think the decision to split some of the activities across additional steps was the right one.
>
> **Step 1:** I'd like this to feel more like a proper landing page rather than just the first screen of an activity. Welcome the learner, briefly explain what they're going to be doing, roughly how long it takes, and what they should expect to get out of it. Make the actual start of the learning activity really obvious and visually separate from the introduction. Think about whether the weekly figures should be presented as part of that introduction or once they've actually started.
>
> **Step 4:** When I complete the first challenge, the "Go to challenge 2" button isn't particularly obvious. At that point, it's the only way forward, so it needs to stand out much more. Make it larger and more prominent, ideally using the same navigation approach as the rest of the activity.
>
> **General:** Run another visual review across every screen and interaction state, specifically looking for overlapping elements, clipped text, buttons, chart labels, tooltips or anything that could make the interface confusing. I have connected claude in chrome to aid in this. Check different screen sizes and browser zoom levels, not just whether the page technically fits. Keep an eye on the fixed navigation and make sure it isn't obscuring anything important. Also check that the instructions match what the activity actually requires. For example, the scrap comparison asks learners to include weeks 7 and 12, so the completion logic should reflect that. Don't introduce any major changes to the existing design or functionality unless you find an actual issue that warrants it.
>
> *(Future-work notes and project status followed, recorded in design-decisions.md.)*

**Method:** the candidate's own Chrome was used through the browser extension for the visual review,
alongside the headless harness for the measurements that need repeating at several viewport sizes.

**Judgement calls:**

1. The weekly figures were taken off the welcome screen. A landing page that opens with a data table
   is not an introduction. The sheet now appears on the matching step, where it is actually used, at
   full width underneath the activity.
2. The activity navigation is hidden on the welcome screen. With a prominent start block on the page
   and a Start button in the fixed bar, two identical buttons were visible at once. The navigation
   appears from step 1 onwards, which also removes a disabled Back button that could never be used.
3. Challenge 2 is reached through the main Continue button rather than a separate one. The engine now
   lets a stage set its own button label and handle its own advance, which keeps one forward control
   for the whole activity.

**Problems found by the visual review:** five, listed in testing-results.md. Two were real defects
that only showed up in a browser: a tooltip hanging 70px outside its chart on the last bar, and the
match badges outgrowing their column on a narrow screen.

---

## Prompt 6 &mdash; independent audit correction pass

The candidate commissioned an independent audit of the data, calculations, charts and explanations
from ChatGPT, and supplied the report as an HTML file. **The findings in that report are not mine.**
The report is preserved unchanged at `Resources/Admin/Line_3_Independent_Data_Audit.html`.

> I've now had ChatGPT (time on this demo limits me from doing so myself) independently audit the application's data, calculations, charts and instructional explanations.
>
> The complete audit report is in /Resources/Admin/. Find and read the HTML file titled "Line 3 Independent Data Audit", along with the original candidate brief and our existing project notes.
>
> The audit is fairly positive overall. It confirmed that all 60 original data values match the brief, the underlying calculations are correct, and the application's core data-handling logic passed its source-level tests.
>
> However, it identified eight issues with some of our explanations, assumptions, annotations and the final printable note.
>
> I want to use this as our final data accuracy and quality assurance pass before submission.
>
> **First, review the findings independently.** Don't just assume that everything ChatGPT has flagged is correct. Go through all eight findings and three informational observations, compare them against the actual application source and original design brief, and determine whether you agree with each one. For each finding: check the original claim against the source data; reproduce the issue where possible; independently verify any relevant calculations; decide whether the finding is valid, partially valid, or something you disagree with; explain briefly what needs to change and why. If you disagree with something, document your reasoning and supporting evidence rather than silently ignoring it.
>
> Also make sure the audit was performed against the same version of the application we're currently working on.
>
> The independent audit used a Node execution harness rather than a full browser, so don't treat its 320 passing assertions as proof that every browser interaction has been tested.
>
> *(The eight findings and three informational observations followed, with the candidate's own instructions for each. Recorded in review-findings.md alongside the assessment of each.)*
>
> Keep the existing design and learning structure. Don't change any of the original dataset figures. Don't change correct calculations just to address problems with their explanations. Keep the single HTML file with no dependencies or framework. This is a targeted correction pass, not another redesign.
>
> Preserve the original audit report unchanged as evidence of the independent review. Don't rewrite it to reflect the corrected application. Also preserve the full prompt history, including this prompt and any subsequent corrections. Don't retrospectively rewrite previous prompts or represent the audit as your own original findings.

**Version check.** The report quotes SHA-256 `bd8ee19997a91df8a192e228290db7ed9d5653bca8db463d79d562a7eb0280d6`
for the file it reviewed. The working file hashed identically, so the audit ran against the current
code and no finding was stale. The report was also found in `~/Downloads` rather than
`Resources/Admin`; it was copied in unchanged.

**Independent verification before accepting anything.** Every flagged string was located in the
source and every numerical claim recomputed from the brief's own figures with Decimal arithmetic:
the median pair (4,910 and 4,930, with no week equal to 4,920); week 7's direction on all four
measures; the week 11 and week 12 downtime tie; the rounding sensitivity intervals for weeks 11 and
5, which overlap; and the alternative scrap denominator. All of the audit's numbers held. One piece
of its wording is loose: it says every downtime cell from week 10 gets a downward arrow "including 8
hours in week 11", but week 11's arrow was correct (9 hours down to 8). Only week 12 was wrong,
which is what its recommendation says.

**Where I did not simply follow the report.** DATA-007 was accepted as a clarity problem, not as the
factual error the report calls it; the reasoning is in review-findings.md. On DATA-005 I applied a
wider fix than the minimum suggested, because the original logic was positional rather than
comparative and was correct on the other two measures only by coincidence. On INFO-002 I acted on
the dishonest "0 of 3" counter and the average screen's unmatched instruction, but added no new
completion tracking, which the candidate had asked me not to do.

**One correction to my own work found while implementing:** the first draft of the median fix typed
4,910 and 4,930 as literals. They are now derived from the sorted data, like every other figure in
the file.

---

## Prompt 7 &mdash; second audit round and release preparation

The candidate commissioned two further independent reviews: a final data regression audit from
ChatGPT and an instructional design review from Gemini. **Neither set of findings is mine.** Both
reports are preserved unedited in `Resources/Admin/`.

> I've now completed two more independent reviews of the application, one final data regression audit through ChatGPT and one instructional design review through Gemini.
>
> Both reports are in /Resources/Admin. Please find and read them in full, alongside the original brief, our project notes and the current application.
>
> Overall I'm very happy with the results. The ChatGPT audit passed with qualifications and confirmed the eight previous data issues have been resolved. Gemini also considered the activity ready with qualifications, identifying a handful of relatively minor instructional design and accessibility concerns.
>
> I think we're now at the point of wrapping things up, so I want this to be a final targeted correction and release preparation pass, not another redesign.
>
> **ChatGPT regression audit.** REG-001: Agree, fix the average activity so clicking the already-selected "Include week 7" button doesn't satisfy the completion requirement. Align the screen reader announcement for estimated scrap parts with the wording shown on screen. Don't change any of the calculations or original data. Check that the source being changed is the same version the regression report audited before applying fixes.
>
> **Gemini instructional design review.** F-01: keep the existing fill-in-the-blank document, use examples as guidance rather than having them automatically provide the complete answer, and give a gentle prompt if someone tries to finish without contributing anything. They should still be able to proceed if they explicitly choose to skip. The final printout must clearly distinguish their contributions from the resource's supplied learning summary. F-02 focus: agree. F-03 aria-expanded: agree. F-04 mobile tables: agree, but keep the table semantics and don't split related figures so far apart they become hard to compare. F-05: optional. F-06: review the latest implementation and only change it if there's still a genuine problem; I don't want duplicate navigation buttons unnecessarily. F-07 confetti: disagree, keep it.
>
> On Gemini's estimated completion time, that's worth recording as a potential risk, but it's not based on measured testing with actual learners, so don't redesign the resource around that estimate.
>
> Please don't change correct things simply because Gemini offered a preference. If one of the review findings doesn't hold up against the actual source, document why rather than implementing an unnecessary fix.
>
> *(Release preparation instructions followed: confirm the single-file application still runs, make sure no development-only files, private notes, audit material or source brief could be exposed through the public deployment, check the README, check for placeholders or debugging elements, prepare a release-ready version but don't deploy, don't commit.)*

**Version check before touching anything.** The regression report describes "index(6).html; 1,666
lines; 87,456 bytes". The working file matched both exactly, and the brief hash it quotes
(`098585a314c9…`) matched this repository's brief. I initially misread that hash as the
application's and briefly thought the audit was against a different build; it is the brief's.

**Two findings not implemented, with reasons.** F-06 asks for an inline button beside the challenge
feedback. That button existed and was removed one iteration earlier at the candidate's request for a
single forward control; re-adding it would undo that decision. A wording pointer to the navigation
was added instead. F-07 asks for the confetti to be removed; the candidate asked for it and it is
already suppressed under reduced motion.

**One finding where the stated cause did not reproduce.** F-02 attributes poor focus visibility to
the ring clipping against gridlines. Tested: there is no `overflow:hidden` ancestor above any bar,
the ring renders 4 to 5px outside the plot uncut, and gridlines sit behind it. The underlying
concern was still real for a different reason, so an improvement was made and the incorrect
mechanism documented rather than silently accepted.

**A testing fault of my own, found mid-pass.** The first verification run after these edits reported
every correction as absent. The file on disk and the file served were both correct: headless
Chromium had cached the page across two edits made within the same second. All three harness
scripts now cache-bust, and every result in this pass was re-run afterwards. Any earlier run in this
project that happened to straddle a same-second edit could in principle have been affected, which is
an argument for the manual walkthrough rather than a known defect.

**Release preparation.** Deploying the repository root would have published the candidate brief, the
private project notes and all three audit reports. The application moved to `public/index.html` so
the deploy directory contains the single file and nothing else; verified by serving `public/` and
confirming every path under `Resources/` returns 404. The README was written from empty. Dead CSS
left over from the removed example buttons was deleted. No debugging statements, placeholders or
external references exist in the file.

---

## Prompt 8 &mdash; Design Lens, documentation and release

> I've now completed my final manual testing and I'm happy with the activity as it stands. I've got one final feature I'd like to add before I handle deployment, along with finishing up the repository documentation.
>
> **Design Lens.** I'd like to add a small SVG glasses icon in one of the top corners of the application. Clicking it should toggle a feature called Design Lens. The idea is that someone reviewing the resource, particularly the interview panel, can turn this on to explore some of the instructional and design decisions that went into building it. Hovering over relevant elements should highlight them and display a small text box explaining why that element was designed that way. Use the existing notes, development discussions and documentation in the repository as the source of these explanations. Don't invent reasons or retroactively attribute decisions to me that I haven't actually made. Focus on explaining meaningful decisions, not annotating every button or paragraph just for the sake of it. The highlighted element and its explanation should be visually connected, without the text box obscuring the content or other controls. Design Lens should work with keyboard focus and touch as well as mouse hover. Off by default, easy to turn off, and it must not interfere with the learner's interactions, progress or navigation. Include a disclaimer when it is enabled, something along the lines of: *These explanations were generated with AI using the developer's notes and discussions. They may not fully reflect every decision made during development.* If there isn't a documented reason behind a particular design choice, don't invent one. Just leave that element unannotated.
>
> **Independent verification documentation.** I've also consulted other AI tools to independently review the resource. Please include these references: ChatGPT https://chatgpt.com/share/6acb3271-30f8-83ec-8824-b7051e1fb2d3 and Gemini https://share.gemini.google/CdfsaoNilIRA. This isn't a request to reopen the audits. Please distinguish AI-assisted verification from manual testing, and don't describe anything as tested if it wasn't.
>
> *(Documentation, repository tidy-up, final testing and commit instructions followed.)*

**Sourcing the explanations.** The nineteen notes were written by extracting the recorded reasons
from `design-decisions.md` and `review-findings.md` first, then condensing each to two or three
sentences. Several name the audit that caused the change, because that is what the record says.
Two screens carry fewer notes than the rest and the welcome screen carries two, because that is how
much was actually written down about them.

**Three things the first build got wrong, found by looking at it rather than by testing state:**

1. The explanation panel floated below the highlighted element, which put it directly over the
   measure buttons on step 3. A floating box beside a full-width element will always cover whatever
   is underneath. Replaced with a panel docked above the navigation, which cannot cover the element
   it describes; on a phone the marked area is scrolled clear of it.
2. Every marked area carried a dashed outline the whole time the feature was on. It competed with
   the activity and looked like the chart's own "choose a week" affordance. Now nothing shows until
   hover or focus.
3. Highlighting repainted the element's background, which washed out the white text on the dark
   task strip so it could not be read. Highlighting is now an outline only.

**One gap found by testing:** after removing the progress-dots annotation (no room for a marker
beside the step counter), the welcome screen had no notes at all, so turning the feature on there
appeared to do nothing. Two recorded decisions about that screen were added.

**Not done:** no new frameworks or dependencies, no changes to any learning activity, and no
annotation written where the repository holds no recorded reason.

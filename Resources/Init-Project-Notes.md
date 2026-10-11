# Project Notes
Myself thinking through the project + for AI agent use.
Note: The candidate brief takes priority over these notes

## General idea
- Potential name: "Line 3: What's Really Going On?"
- Put the learner in the position of a worker looking at the weekly production numbers
- Nothing too complicated (roughly 15 mins to complete)
- Not too focused on reading graphs - should teach knowing when to questions numbers more than anything

## Learners
- Factory workers who already know their jobs, but might not be confident reading charts or using computers
  - Quick research (https://www.gov.uk/government/publications/quantifying-the-uk-data-skills-gap/quantifying-the-uk-data-skills-gap-full-report, https://dashboard.digitalinclusionindex.org.au/Digital.aspx) found that a factory worker could be perfectly capable of operating specialised machinery or production systems for their speciality, but have limited familiarity with general technology workflows.
  - Potentially a guide/help wizard always available to guide them on the interface
- Don't want it to feel like a school quiz or generic corporate training! As tailored and interactive as possible
- Plain English, short instructions, one thing at a time
- Should work on a phone or shared computer without anyone needing to explain how to use it (wizard/start guide)
- Show an example first -> then let them try things themselves

## Activity ideas
- Start with something interactive and familure (in style as well as function) e.g a simple graph showing production against the weekly target. Then let people select weeks and see what the numbers mean
- Look into a big break in the pattern - Week 7 where production drops and downtime increases. Let them make an initial judgement, then reveal the note about the storm and power outage
- Have an interactive chart where they can change the scale or which weeks are shown. Introducing different impressions of the same data?
- Need to demonstrate at least two ways charts or tables can be misleading
- Then into another big break - 10 to 12 -> Production improves and fault calls go down, but overtime started and the fault reporting form changed + scrap also increases
    - Don't specify or jump to the conclusion that those changes caused the trends. Just get learners asking better questions about the data
- End with a simple workplace decision. Smth like what they'd bring up to their supervisor or what they'd investigate next
- Feedback should explain the reasoning, not just say right or wrong.

## Design (reused)
- Simple, clean, easy to navigate. Not trying to make some massive polished application.
- More interaction than just multiple-choice questions. Clicking data, revealing context and changing charts should actually teach something.
- No points, badges, animations everywhere or childish gamification.
- Make difficulty build up gradually.
- Keep all the original figures exactly as supplied. No made-up factory details.
- Accessibility from the start: keyboard navigation, good contrast, readable tables, mobile support, not relying on colour alone.

## Build
- Keep to just one HTML file with CSS and vanilla JavaScript
- No backend, accounts or external APIs needed
- Will be hosted somewhere simple like Cloudflare Pages
- Keep the data in one place so the charts and explanations all use the same figures
- Human-in-the-loop at each stage

## AI and testing
- Will keep the complete prompt history (including prompts that fail or approaches I don't use). In /Admin/prompt-history.md + similar data in other files I will populate in there
- Make notes of actual AI mistakes, + if I noticed them and what I changed
- Test the interactions properly: going backwards, changing answers, restarting, odd click orders, etc.
- Try different screen sizes and keyboard-only navigation

## Overall goal
- Want to be able to explain why I made each major design choice and how it helps these specific learners
- Show that AI helped build it, but that I checked the output and made the final calls
- Keep it in scope!
- Main goal = small, useful activity that somebody could sit down and complete at work (and not hate)

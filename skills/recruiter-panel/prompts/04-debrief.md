# Debrief

Inputs: `job-intel.md`, `captures/INDEX.md`, and `recruiters/R1.md`, `R2.md`, `T1.md`, `T2.md`.

## PANEL.md
1. **Scoreboard**: table with recruiter, type (non-technical / technical), time spent, decision, confidence, and the moment they decided.
2. **Panel verdict**: how many proceed. Call it: interview likely (3 or 4 proceed), coin flip (2), unlikely (0 or 1). Name the recruiter who came closest to flipping and what would have flipped them. If the two recruiter types disagree, say why: is the candidate strong on paper and thin in proof, or the reverse?
3. **Numbered issues, worst first**. Merge duplicates. For each: the asset (resume / GitHub / LinkedIn / portfolio / cross-source), the evidence (quote or file name), why it hurts at THIS company (tie to job-intel), and who flagged it (R1, R2, T1, T2). Rank by: caused a REJECT or HOLD > flagged by both recruiter types > flagged by several > single pet peeve.
4. **What's working**: signals at least two recruiters called strong. These must survive the fixes.
5. **Must-have coverage**: table of every must-have from job-intel, where the evidence is, and the panel's view of its strength (strong / weak / claim only / missing).
6. **Cross-source mismatches**: from INDEX and the recruiters' notes.
7. **The 10-second test**: what each recruiter took away from their first look, side by side. If these disagree with what the candidate wants to be known for, say so.

## FIXES.md
Start with **Top 5 quick wins** (each under 30 minutes, highest impact first). Then fixes grouped by asset (Resume, LinkedIn, GitHub, Portfolio), ordered by impact. Each fix gives:
- what to change
- the current text, quoted exactly (or the file and screenshot)
- the proposed text or action
- which issue numbers it closes

Asset-specific guidance:
- **Resume**: top third first. Title line, summary, the bullets recruiters quoted as weak. Make sure the must-have keywords from job-intel appear where they are true.
- **LinkedIn**: headline, About, each Experience entry, Featured, and Skills order (the top 3 should be true must-haves from job-intel). Titles and dates must match the resume.
- **GitHub**: which repos to pin, unpin or archive; README sections to add per repo (what, why, how to run, screenshots, live link, stack, what I'd do next); profile README outline; hygiene fixes (remove committed secrets and rotate them, add .gitignore, add tests or CI where cheap).
- **Portfolio**: concrete defects with the page and screenshot (broken link X on page Y, mobile overflow in `portfolio-home-mobile.png`), and which project to lead with for this job.

Writing rules for any proposed text:
- Use only facts present in the candidate's materials or told by the user. Where a fix needs a fact you do not have (a number, a scale, an outcome), write `[ADD: ...]` and collect every one as a question at the end of FIXES.md.
- Plain, specific, human. No em dashes. No buzzwords ("passionate", "leveraged", "spearheaded", "cutting-edge", "results-driven", "dynamic", "synergy"). No lists of three padded for rhythm. No emoji headers.

Both files end with this line:
`Panel run <YYYY-MM-DD>. Language-model simulation, not a guarantee of any hiring outcome.`

---
name: recruiter-panel
description: >-
  Research a specific job and employer, then send four simulated recruiters (two non-technical, two technical, each with a personality) through the user's resume, GitHub, LinkedIn and portfolio, using real screenshots, to decide whether they would interview the user. Use when the user asks for a recruiter review, a hiring panel, a profile audit for a job, or runs /recruiter-panel.
argument-hint: "[job posting URL or pasted text]"
---

# Recruiter panel

You are the orchestrator. You first ask the user for their inputs (step 0), run the phases in order, start the sub-agents, and write the report. Never flatter the candidate. The prompt files for each phase sit in the `prompts/` folder next to this SKILL.md (use the base directory shown when this skill loaded). Read each file with the Read tool when its phase starts.

## 0. Intake gate (do this before anything else)
**Your first action in this skill is to send the user the intake message below, as plain text, and then STOP and wait for their reply.** Do not call any tool, fetch any page, read any file or start any sub-agent until they have answered. This applies even if they already pasted a job link or a resume path: acknowledge what you already have, then ask only for the rest. Plain text is required because the answers are free-form links and paths, so do not use a multiple-choice question tool.

Intake message (drop the lines the user already supplied):

> To run the panel I need a few things. Paste them in one reply:
> 1. **Job posting**: a URL, or the pasted text. (required)
> 2. **Your resume**: a file path (PDF, DOCX or markdown), or pasted text. (required)
> 3. **Your links**, whichever you have: GitHub profile, LinkedIn profile, portfolio or personal site, and any extras (blog, Kaggle, Behance, ArtStation). The more you give, the more the recruiters can judge.
> 4. **Optional context**: location, work authorization, remote or relocation preferences, and anything I should not treat as a red flag (for example, "my professional code is private").
> 5. **LinkedIn PDF** (optional): if LinkedIn won't open for me, export your profile (profile page, More, Save to PDF) and give me the path.
>
> I never need passwords. If a site needs a sign-in, you sign in yourself in the browser I open.

When the reply arrives, check it. If the job posting or the resume is still missing, ask for just those, once more, and wait again. Links are optional: if the user gives none, say that the panel will judge the resume alone and continue. If a link is only a site's homepage (for example `linkedin.com` with no profile name), ask for the full profile URL.

Do not write the user's details into any file outside the run folder.

## 1. Run folder
Create `recruiter-panel-runs/<YYYY-MM-DD>-<company>-<role-slug>/` in the current working directory. Save the posting as `job-posting.md` and the inputs as `inputs.md` inside it. Everything below goes in this folder.

## 2. Phase 1: job intel (three researchers in parallel, then you merge)
Read `prompts/01-job-intel.md`. Start three sub-agents in ONE message, each given that file's full text, the posting, the run folder path and ONE lane (A the role, B the employer, C the people). Each writes `intel/lane-<a|b|c>.md`. They never see the candidate's materials. Then do the "Merge" section yourself and write `job-intel.md`.

## 3. Evidence capture (you do this, not a sub-agent)
Read `prompts/02-capture.md` and follow it for the sources the user supplied. One browser, and all four recruiters must see identical pages, so this is not parallelized. Use whatever browser tools you have; if you have none, use Playwright from the shell for public pages and say in INDEX what could not be captured. Produce `captures/` and `captures/INDEX.md`.

## 4. Phase 2: four recruiters, alone
Read `prompts/03-recruiter-brief.md` and the four files in `prompts/personas/` (`R1-dana.md`, `R2-marcus.md`, `T1-sam.md`, `T2-lena.md`). Start four sub-agents in ONE message. Each gets: the brief, its own persona file, `job-intel.md`, `job-posting.md`, the absolute path of `captures/`, the text of `captures/INDEX.md`, the optional context from step 0, and its output path `recruiters/<R1|R2|T1|T2>.md`. Tell each to open the screenshots itself with the Read tool. Nobody sees anyone else's notes.

## 5. Debrief
Read `prompts/04-debrief.md` and follow it. It writes `PANEL.md` and `FIXES.md`.

## 6. Show the user
Print in chat, in full: the scoreboard, each recruiter's Decision, Note to the hiring manager and What would flip me, the numbered issue list, the top 5 quick wins, every `[ADD: ...]` question, and the run folder path. Then offer to apply the fixes (rewrite the resume, LinkedIn text, README drafts) from `FIXES.md`.

## Rules
- Use only what is in the user's materials and what they told you. Never invent employers, titles, dates, numbers, skills or employer facts. Label guesses "assumed" or "inferred".
- Read-only on every site: never message, connect, follow, star, react, apply or submit anything.
- Be honest. If the candidate is strong, say so and say which recruiter came closest to rejecting.
- Judge only job-related signals. Ignore protected traits.
- This is a simulation by language models. It does not guarantee an interview and is not career or legal advice.

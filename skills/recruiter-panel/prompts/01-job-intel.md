# Phase 1: Job intel

You are a research analyst preparing a hiring panel. Four recruiters will read your briefing and must come away thinking like people who actually hire for this company. You have NOT seen the candidate and you must not look for them. Describe the job as it really is.

## How hard to look
Be aggressive. Read primary pages, not just search snippets. Aim for 15 to 30 searches in your lane, follow links two levels deep, and use extended search when results are thin. Every claim gets a source URL. Mark anything you deduced as "inferred" and anything you could not confirm as "unverified". Date your findings: anything older than 18 months is "stale".

## Lanes (you get ONE)

### Lane A: the role
- Parse the posting: exact title, level, team, location and remote policy, work authorization or visa language, salary band, start date.
- Split requirements using the posting's own words: must-haves ("required", "must", "you have", "minimum") vs nice-to-haves ("bonus", "plus", "nice to have", "preferred").
- Decode the level: compare the title and years against Levels.fyi and similar postings at this company and its peers. What does this level mean here in scope and autonomy?
- Find the company's other open roles (careers page, LinkedIn Jobs, Greenhouse, Lever, Ashby, Workday). Which team is this? Backfill or growth? How many similar roles?
- Posting history: reposted, how long open, edited? (LinkedIn "reposted", Wayback Machine, job aggregators.)
- ATS keyword list: every hard skill, tool, framework, certification and domain term, with how often it appears, whether it is required, and common synonyms.
- Hidden requirements: what the posting implies without saying it (for example "fast-paced, ambiguous" plus a tiny team means expect to own things alone).

### Lane B: the employer
- What they sell, to whom, business model, size, stage, funding or revenue, profitability signals.
- Last 12 months of news: launches, layoffs, hiring freezes, acquisitions, leadership changes, lawsuits, security incidents.
- Engineering: stack (engineering blog, GitHub org, StackShare, job posts, conference talks), how they ship, open source presence, on-call, what they brag about technically.
- Culture: stated values (careers page, handbook) vs what employees report (Glassdoor, Blind, Indeed, Reddit). Keep stated and reported in separate lists.
- Interview process: stages, take-home or live coding, system design, typical questions, timeline, reported pain points (Glassdoor interviews, Blind, LeetCode discuss).

### Lane C: the people
- Who screens: in-house recruiting team or agencies? Titles of the recruiters for engineering. Likely hiring manager or team lead from public sources (job post, engineering blog, talks, LinkedIn search). Professional public info only. No personal lives.
- Who gets hired: find 5 to 10 public profiles of people in this or a similar role at the company (LinkedIn via search, GitHub org members, blog authors, speakers). Report PATTERNS, not dossiers: typical years of experience, prior employer types, degree or not, school tier, common skills, how they describe themselves, whether they have public GitHub or portfolios. Do not list personal details about individuals.
- What the company's recruiters and engineering leaders say publicly about what they look for, and their pet peeves.
- The on-paper bar: what a typical successful hire at this level looks like.

## Your output
Write `intel/lane-<a|b|c>.md` in the run folder: your findings under the bullets above, each with a source URL, then a closing section "Top 5 things a recruiter here would screen for", drawn from your lane's evidence only.

---

## Merge (the orchestrator does this after all three lanes finish)
Write `job-intel.md` with exactly these sections. Resolve conflicts between lanes by preferring newer and primary sources; note conflicts you could not resolve.

1. **Snapshot**: company, role, level, location and remote policy, comp band, work authorization. Five lines.
2. **The real job**: what this person does in week one, month three, year one. Cite or mark inferred.
3. **Requirements**: must-haves, nice-to-haves, hidden requirements.
4. **ATS keywords**: table of term, required (Y/N), count in posting, synonyms an ATS may accept.
5. **Who gets hired here**: the on-paper profile of a typical successful candidate.
6. **Culture**: stated values vs reported reality.
7. **Interview process**.
8. **Instant rejects at this company**: what would get a profile tossed here, from evidence, not generic advice.
9. **Instant yeses**: signals that would fast-track someone here.
10. **Recruiter calibration**:
    - A non-technical recruiter screening for this company: their pressure (req load, time-to-fill, hiring manager temperament), what they skim for, what scares them.
    - A technical recruiter or sourcer screening for this company: which technical signals the hiring manager trusts, what they consider fake or weak, how much they weigh GitHub vs work history.
11. **Open questions, stale and unverified items**.
12. **Sources**: grouped by lane.

Keep sections 1 to 11 under about 1500 words. The recruiters read all of it.

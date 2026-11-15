# recruiter-panel

A Claude Code plugin. You give it a job posting, your resume and your links. It researches the job and employer, then four simulated recruiters (two non-technical, two technical, each with a personality and a time limit) go through your resume, GitHub, LinkedIn and portfolio, using screenshots, and each decides: interview, hold or reject. You get a ranked list of problems and a fix plan.

## Install
```
claude plugin marketplace add YOUR-USER/recruiter-panel
claude plugin install recruiter-panel@recruiter-panel-marketplace
```

## Use
In a session, run `/recruiter-panel:recruiter-panel` (or just ask for a recruiter review). It asks for the job posting, your resume path and your links. Results go in `recruiter-panel-runs/` in the folder you ran it from.

## Needs
- Web search and fetch (job research)
- A browser tool for screenshots (Claude in Chrome or the desktop app's browser; signed in to LinkedIn is best). Without one it falls back to Playwright for public pages.
- `pdftotext` and `pdftoppm` (poppler) for PDF resumes

## Privacy
Your inputs stay in the run folder on your machine. The plugin contains no personal data and the skill never asks for passwords. It only reads pages; it never posts, connects or applies.

This is a simulation by language models. It does not guarantee an interview.

MIT licensed.

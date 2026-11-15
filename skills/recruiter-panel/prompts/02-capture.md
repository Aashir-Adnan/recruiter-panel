# Evidence capture

Goal: a capture pack that lets the recruiters SEE the candidate's online presence the way a real recruiter would, in a browser at real screen sizes. All four recruiters work from this same pack, so it must be complete enough that none of them has to guess what a page looked like.

Write everything to `captures/` in the run folder.

## Tools
Use whatever browser you can drive: Claude in Chrome or the built-in browser (best for LinkedIn because it can be signed in), or Playwright from the shell for public pages:
- `npx playwright screenshot --viewport-size=1440,900 <url> <file>.png`
- add `--full-page` for the full scroll
- `--viewport-size=390,844` for mobile

For every page, capture:
- `fold`: what shows at 1440x900 with no scrolling. This is what a recruiter sees in the first three seconds.
- `full`: the whole page (one full-page shot, or numbered viewport shots `-1`, `-2`, ...).
- the page text as `.txt` (page text tool or `document.body.innerText`).

Name files `<source>-<page>-<fold|full|mobile>.png`, for example `github-profile-fold.png`, `linkedin-experience-full.png`.

Read-only everywhere: never message, connect, follow, star, endorse, react, apply, or change any setting.

## Which sources to capture
Capture only the sources the user actually gave you (resume, GitHub, LinkedIn, portfolio, and any extra links such as a blog, Kaggle, Behance or ArtStation). For an extra link, apply the portfolio steps. For a missing source, write "not provided" in INDEX; recruiters then judge the candidate without it and say so.

## Resume
- PDF: render each page to PNG (`pdftoppm -png -r 110`), extract `resume-layout.txt` (`pdftotext -layout`) and `resume-raw.txt` (`pdftotext` without layout, which approximates what an ATS parser sees). If the raw text comes out scrambled, out of order, or missing sections, record it in INDEX as a finding.
- DOCX: convert to PDF first (LibreOffice headless), then the same.
- Note page count, file name (recruiters see it), and whether links in the PDF are clickable.

## GitHub (`https://github.com/<handle>`, from the URL the user gave)
1. Profile page: fold and full (avatar, bio, profile README, pinned repos, contribution graph, achievements).
2. Repositories tab sorted by last updated: fold.
3. Metadata: fetch `https://api.github.com/users/<handle>` and `https://api.github.com/users/<handle>/repos?per_page=100&sort=pushed` (use `gh api` if available). Save `github-api.json`. In INDEX, build a table: repo, fork (Y/N), stars, main language, last pushed, description, has README, has tests, has CI, license, homepage link.
4. Each pinned repo (up to 6) plus any repo named in the resume, LinkedIn or portfolio: repo landing page fold and full (rendered README), commits page fold, and in INDEX note commit count, contributors, first commit date, tests folder, `.github/workflows`, license, live demo link and whether it loads.
5. Deep file for the top two repos: the core source file an engineer would open first (main entry or the largest hand-written file under `src/` or equivalent, not generated or vendored). Screenshot fold and save the raw text.
6. Quick hygiene scan of those repos (do not open private data): committed `.env` or key-looking strings, committed `node_modules` or build output, default "Create React App" README left in place. Record findings only, do not copy any secret into the pack.

## LinkedIn
Needs a signed-in browser. Capture fold and full for:
- top card (photo, banner, headline, location, open-to-work frame, connections count)
- About
- Experience (click every "see more" first)
- Education, Licenses and certifications
- Skills (the full list page)
- Featured, Projects, Recommendations
- Activity (last 5 posts and comments), fold only

If you cannot open it signed in, use the LinkedIn PDF export the user gave you (if any) and write in INDEX that recruiters are missing photo, banner, Featured and Activity.

## Portfolio
- Home: fold, full, and mobile fold.
- Every page in the main navigation and every project or case study linked from home (up to 8): fold and full.
- Animated or lazy content (count-up numbers, fade-ins, scroll-triggered sections): scroll each section into view the way a person would (mouse-wheel or keyboard scrolling, not a jump), wait 3 seconds, then screenshot. Record both the first value you saw and the settled value. A value that only appears after scrolling is a fragility note (link previews, fast scrollers and reduced-motion users may never see it), not a broken feature, unless it stays wrong after a real scroll and wait.
- Health checks, recorded in INDEX: time until content shows (rough), broken images, layout shifts, console errors (read the console), every link on the home page checked (note 404s and dead demos), whether it links to GitHub, LinkedIn and the resume and whether those links work, whether it is an obvious template, any placeholder or lorem ipsum text.

## Links that fail from here
The capture environment blocks some sites. If a link fails, retry once with WebFetch. If it still fails, record it as "unreachable from the capture environment, unverified", never as broken, and do not let recruiters treat it as a defect.

## INDEX.md
1. **Files**: every file with a one-line description, ordered roughly the way a recruiter would open them (resume, LinkedIn top card, GitHub profile, portfolio home, then deeper).
2. **Cross-source facts**: table of facts that appear in more than one place and whether they match: name, headline or title, current employer and status, each role's title and dates, education and dates, location, email, top skills. Mark every mismatch. Record, do not judge.
3. **GitHub repo table** from step 3 above.
4. **Health findings** from resume parsing, GitHub hygiene, and portfolio checks.
5. **Not captured**: what you could not capture and why.

Do not save cookies, tokens or session data into the run folder.

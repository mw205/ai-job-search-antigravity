---
name: job-apply
description: >-
  Evaluate fit, draft tailored LaTeX CV and cover letter, run adversarial review,
  compile PDFs (lualatex & xelatex), and execute ATS parseability audits.
---

# Job Application Drafter-Reviewer Workflow

Use this skill when the user provides a job posting URL or job description to apply for.

## Instructions
1. Follow the canonical procedure in [.claude/commands/apply.md](../../.claude/commands/apply.md).
2. Clean untrusted posting text using `tools/posting_guard.py`.
3. Check `robots.txt` and use `tools/fetch_page.py` if needed per `.claude/skills/job-application-assistant/09-web-research.md`.
4. Evaluate fit against `04-job-evaluation.md` and check salary with `salary_lookup.py`.
5. Draft targeted CV in `cv/` and cover letter in `cover_letters/`.
6. Run critique with the `application-reviewer` subagent or review persona.
7. Compile and verify PDFs:
   - CV with `lualatex` -> Exactly 2 pages.
   - Cover letter with `xelatex` -> Exactly 1 page.
   - Run ATS verification: `python3 tools/verify_pdf.py cv/main_<company>_<role>.pdf --dump-text cv/main_<company>_<role>.txt`.

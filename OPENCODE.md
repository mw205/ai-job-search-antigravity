# OpenCode Guidelines: AI Job Search

This workspace is fully compatible with OpenCode (`opencode.ai`).

## Runtime Integration
OpenCode shares the exact same methodology, candidate truth base, and skills as Claude Code and Google Antigravity:

1. **Candidate Profile & Truth Base:**
   - Follow [AGENTS.md](AGENTS.md) and [CLAUDE.md](CLAUDE.md).
   - Candidate details, experience, and projects are defined in [.claude/skills/job-application-assistant/01-candidate-profile.md](.claude/skills/job-application-assistant/01-candidate-profile.md).
   - Never fabricate skills, experience, or metrics.

2. **Skills & Commands:**
   - Skills are located in [.agents/skills/](.agents/skills/) in standard Agent Skills format.
   - OpenCode automatically discovers:
     - `job-setup`: Candidate profile setup & onboarding.
     - `job-scraper`: Multi-portal search & deduplication.
     - `job-apply`: Drafter-reviewer application pipeline.
     - `job-rank`: Batch posting fit scoring against candidate rubric.
     - `job-interview`: STAR interview preparation.
     - `job-upskill`: Postings gap analysis.
     - `linkedin-search`: LinkedIn job search CLI (`bun run .agents/skills/linkedin-search/cli/src/cli.ts`).
     - `freehire-search`: FreeHire remote & contract tech job search CLI.

3. **Compilation & Verification:**
   - Compile CV with `lualatex` in `cv/` (must be 2 pages).
   - Compile Cover Letter with `xelatex` in `cover_letters/` (must be 1 page).
   - Verify text layer with `python3 tools/verify_pdf.py cv/main_<company>_<role>.pdf --dump-text cv/main_<company>_<role>.txt`.

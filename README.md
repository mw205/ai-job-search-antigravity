<p align="center">
  <img src="assets/mascot/pip_flight_loop.gif" alt="Pip, the courier bird" width="180">
</p>

# AI Job Search (Antigravity, OpenCode & Claude Code)

*The autonomous, multi-agent job application framework that runs locally on your machine.*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Runtimes](https://img.shields.io/badge/Runtimes-Antigravity%20%7C%20OpenCode%20%7C%20Claude%20Code-blueviolet.svg)](#multi-runtime-support)
[![LaTeX: LuaLaTeX%20%2B%20XeLaTeX](https://img.shields.io/badge/LaTeX-LuaLaTeX%20%7C%20XeLaTeX-008080.svg)](https://tug.org/texlive/)

An AI-powered job search and application operating system designed to run **as it is across Google Antigravity, OpenCode, and Claude Code**. Clone it, configure your profile, and let your AI agent search portals, evaluate fit, tailor your LaTeX CV, draft compelling cover letters, and prepare you for client and technical interviews.

> **Attribution & Provenance:**  
> This project builds upon the proven multi-agent job application methodology originally created by **[Mads Lorentzen](https://github.com/MadsLorentzen/ai-job-search)**. This edition is engineered for seamless cross-runtime compatibility with **Google Antigravity**, **OpenCode**, and **Claude Code** by **[Mohamed Waleed](https://github.com/mw205)**.

---

## Multi-Runtime Support (Use As It Is)

You can open and run this repository with whichever AI assistant you prefer without altering any configuration:

| AI Runtime | Native Configuration | Workflow Execution |
| :--- | :--- | :--- |
| **Google Antigravity** | Reads `AGENTS.md` & `GEMINI.md` | Executes Agent Skills from `.agents/skills/` (`job-setup`, `job-scraper`, `job-apply`, etc.) |
| **OpenCode** | Reads `AGENTS.md` & `OPENCODE.md` | Automatically discovers and runs skills from `.agents/skills/` |
| **Claude Code** | Reads `CLAUDE.md` & `.claude/settings.json` | Runs slash commands from `.claude/commands/` (`/setup`, `/scrape`, `/apply`, etc.) |

---

## Core Capabilities

Antigravity's progressive disclosure, native skill discovery (`.agents/skills/`), hierarchical workspace rules (`AGENTS.md`), and subagent orchestration make it the ideal runtime for managing job hunts:

- **100% Local & Privacy-Preserving:** Your personal data, salary targets, and applications stay on your machine.
- **Native Skill Discovery:** Every workflow is an Antigravity skill (`job-setup`, `job-scraper`, `job-apply`, `job-rank`, `job-interview`, `job-upskill`).
- **Two-Agent Drafter-Reviewer Architecture:** The primary agent acts as the Drafter, while an adversarial reviewer subagent (`application-reviewer`) critiques drafts against the posting and company research.
- **Automated ATS & Layout Verification:** Enforces a strict **2-page CV** (`lualatex`) and **1-page cover letter** (`xelatex`), verified with mechanical ATS text layer extraction (`tools/verify_pdf.py`).
- **Prompt Injection Defense:** Uses `tools/posting_guard.py` to sanitize untrusted job postings, stripping hidden HTML and manipulative prompt injections before evaluation.

---

## Architecture & Workflows

```
  Tell Antigravity:              Tell Antigravity:              Tell Antigravity:
   "Run setup"                   "Search for jobs"              "Apply to <URL>"
        │                               │                              │
        ▼                               ▼                              ▼
┌───────────────┐              ┌─────────────────┐           ┌──────────────────┐
│   job-setup   │              │   job-scraper   │           │    job-apply     │
│   (Onboard    │              │ (LinkedIn,      │           │  (Evaluate fit,  │
│ candidate     │              │  FreeHire, etc.)│           │   check gates,   │
│ truth base)   │              └────────┬────────┘           │   draft LaTeX)   │
└───────┬───────┘                       │                    └────────┬─────────┘
        │                               ▼                             │
        ▼                      ┌─────────────────┐                    ▼
┌───────────────┐              │    job-rank     │           ┌──────────────────┐
│ Candidate     │              │  (Batch score   │           │ Reviewer Agent   │
│ truth base in │              │  postings &     │           │ (Hiring manager  │
│ profile files │              │  deduplicate)   │           │  critique & diff)│
└───────────────┘              └────────┬────────┘           └────────┬─────────┘
                                        │                             │
                                        ▼                             ▼
                               Pick top match ───────────────► ┌──────────────────┐
                                                               │ Compile & Verify │
                                                               │ (lualatex CV 2p, │
                                                               │  xelatex CL 1p,  │
                                                               │  ATS parse test) │
                                                               └──────────────────┘
```

---

## Prerequisites

1. **Google Antigravity:** (Antigravity IDE or CLI).
2. **Python 3.10+:** With `pypdf` for ATS text verification:
   ```bash
   pip install pypdf openpyxl
   ```
3. **Bun (for job search CLIs):**
   ```bash
   # macOS/Linux:
   curl -fsSL https://bun.sh/install | bash
   # Windows PowerShell:
   powershell -ExecutionPolicy Bypass -c "irm https://bun.sh/install.ps1 | iex"
   ```
4. **LaTeX Distribution:**
   - **Linux:** TeX Live or TinyTeX (`sudo apt install texlive-latex-extra texlive-xetex texlive-luatex texlive-fonts-extra`)
   - **macOS:** MacTeX or TinyTeX
   - **Windows:** MiKTeX (Auto-install enabled)

---

## Quick Start (3 Steps)

### 1. Fork and clone

```bash
gh repo fork mw205/ai-job-search-antigravity --clone
cd ai-job-search-antigravity
```

> [!IMPORTANT]
> **A fork of this repo is always public** — GitHub does not allow private forks of
> public repositories — and `/setup` (or `job-setup`) writes your personal data (name,
> contact details, employment history, salary expectations) into **tracked** files.
> If this copy is for your own job search rather than for contributing changes back,
> use a **private repository** with this repo as `upstream` instead — the two-minute
> recipe is in [SETUP.md section 8](SETUP.md#8-pulling-upstream-updates-into-your-fork),
> and every update workflow works identically. Fork only to contribute.

To install portal search CLI dependencies:
```bash
python3 tools/install_portal_clis.py
```

### 2. Open in Google Antigravity & Run Setup

Open the folder in your Antigravity IDE or workspace, and simply tell Antigravity in the chat:

> *"Run setup to build my candidate profile."*

Antigravity will trigger the `job-setup` skill and offer 3 onboarding options:
- **Path A (Documents Folder):** Place your existing CV, LinkedIn PDF export, or project summaries in `documents/` — Antigravity reads and cross-references them.
- **Path B (Paste CV):** Paste or mention your existing CV text in the chat.
- **Path C (Interactive Interview):** Answer structured questions about your technical skills, past projects, and target role types.

### 3. Search and Apply

- **Find Opportunities:**
  > *"Search LinkedIn and FreeHire for remote Flutter or Full-Stack developer contracts."*
  > *(Triggers `linkedin-search` and `freehire-search` to fetch and deduplicate listings.)*

- **Apply to a Specific Job:**
  > *"Apply to this job: https://www.linkedin.com/jobs/view/1234567890"*
  > *(Evaluates fit against your rubric, drafts a tailored 2-page CV and 1-page cover letter, runs reviewer critique, compiles PDFs, and runs the ATS audit.)*

- **Prepare for Interview:**
  > *"I have an interview with <Company> for <Role>. Help me prepare STAR talking points and questions."*
  > *(Triggers `job-interview` using verified examples from your profile.)*

---

## Available Antigravity Skills

| Skill | Command / Prompt | Purpose |
| :--- | :--- | :--- |
| **`job-setup`** | "Run setup", "Configure profile" | Extracts and populates candidate truth base. |
| **`job-scraper`** | "Find jobs", "Scrape jobs" | Scrapes multiple portals with recency and location filters. |
| **`linkedin-search`** | "Search LinkedIn for [role] in [location]" | Runs LinkedIn search CLI directly. |
| **`freehire-search`** | "Search FreeHire for remote [stack] jobs" | Runs FreeHire contract and remote search CLI. |
| **`job-rank`** | "Rank these jobs", "Batch score postings" | Scores a list of jobs against your profile and filters dealbreakers. |
| **`job-apply`** | "Apply to [URL or text]" | Complete 2-agent application drafter, compiler, and ATS verifier. |
| **`job-interview`** | "Prep interview for [Company]" | Generates STAR scenarios and reverse questions. |
| **`job-upskill`** | "Analyze skill gaps in these postings" | Pinpoints market requirements and generates learning goals. |

---

## Repository Structure

```text
├── .agents/
│   ├── rules/
│   │   └── AGENTS.md                 # Antigravity operational rules & verification guidelines
│   └── skills/                       # Native Antigravity Skills
│       ├── job-setup/                # Profile onboarding workflow
│       ├── job-scraper/              # Job scraping & deduplication
│       ├── job-apply/                # Drafter-Reviewer application pipeline
│       ├── job-rank/                 # Batch scoring engine
│       ├── job-interview/            # STAR interview prep
│       ├── job-upskill/              # Skill gap analysis
│       ├── linkedin-search/          # LinkedIn search CLI
│       └── freehire-search/          # FreeHire search CLI
├── AGENTS.md                         # Root workspace rules for Antigravity
├── GEMINI.md                         # Symlink to AGENTS.md
├── CLAUDE.md                         # Candidate profile summary & thin pointer
├── cv/
│   └── main_example.tex              # Master 2-page moderncv template (lualatex)
├── cover_letters/
│   ├── cover.cls                     # Custom 1-page cover letter class (xelatex)
│   └── OpenFonts/                    # Lato and Raleway font assets
├── documents/                        # Drop your CVs, diplomas, or exports here
├── tools/
│   ├── posting_guard.py              # Prompt injection & hidden text filter
│   ├── verify_pdf.py                 # Mechanical ATS text extraction auditor
│   ├── install_portal_clis.py        # Automatic Bun dependencies installer
│   └── rank_state.py                 # Triage state manager
└── README.md
```

---

## License & Attribution

- Built on the core methodology created by **[Mads Lorentzen](https://github.com/MadsLorentzen/ai-job-search)** (MIT License).
- Ported, enhanced, and configured for **Google Antigravity** by **[Mohamed Waleed](https://github.com/mw205)**.
- Licensed under the [MIT License](LICENSE).

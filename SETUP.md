# Setup Guide: AI Job Search (Google Antigravity Edition)

Step-by-step setup instructions for running the AI Job Search operating system with **Google Antigravity**.

---

## 1. Prerequisites

### Google Antigravity
Ensure you have the Google Antigravity execution environment installed (Antigravity IDE or CLI).

### Python (3.10+) & ATS Extraction
Check your Python version:
```bash
python3 --version
```
Install the required packages for ATS verification and salary benchmarking:
```bash
pip install pypdf openpyxl
```

### Bun (for Job Search CLIs)
The portal CLIs (`linkedin-search`, `freehire-search`, etc.) are written in TypeScript and execute via Bun.

- **macOS / Linux:**
  ```bash
  curl -fsSL https://bun.sh/install | bash
  source ~/.bashrc  # or ~/.zshrc
  ```
- **Windows PowerShell:**
  ```powershell
  powershell -ExecutionPolicy Bypass -c "irm https://bun.sh/install.ps1 | iex"
  ```

### LaTeX Engines (for CV & Cover Letter Compilation)
The CV compiles with `lualatex` (to support fontawesome6 and moderncv cleanly); the cover letter compiles with `xelatex` (for Lato and Raleway font loading).

- **Linux (Debian/Ubuntu):**
  ```bash
  sudo apt update
  sudo apt install -y texlive-latex-extra texlive-xetex texlive-luatex texlive-fonts-extra texlive-science
  ```
- **Linux / macOS (User-level Minimal TinyTeX):**
  ```bash
  curl -L https://github.com/rstudio/tinytex-releases/releases/download/v2026.10/TinyTeX-1-linux-x86_64-v2026.10.tar.xz | tar -xJ -C ~/.TinyTeX --strip-components=1
  export PATH="$HOME/.TinyTeX/bin/x86_64-linux:$PATH"
  tlmgr update --self
  tlmgr install moderncv fontawesome5 fontawesome6 academicons import luatexbase pgf titlesec textpos xltxtra cite realscripts needspace
  ```
- **Windows:**
  Install [MiKTeX](https://miktex.org/download) and enable automatic package installation.

---

## 2. Fork or Clone as a Private Repo

> [!WARNING]
> This framework writes your personal contact details, CV, and work history into tracked repository files. **Keep your repository private** on GitHub to protect your personal data.

```bash
git clone https://github.com/mw205/ai-job-search-antigravity.git my-job-search
cd my-job-search
```

Install the search portal dependencies:
```bash
python3 tools/install_portal_clis.py
```

---

## 3. Configure Your Profile with Antigravity

Open the project folder in Google Antigravity.

In the chat prompt, tell Antigravity:
> *"Run setup to build my candidate profile."*

Antigravity will activate the `job-setup` skill and guide you through onboarding:
1. **Documents Folder (Recommended):** Drop your existing CV PDF, LinkedIn export, diplomas, or project links into `documents/` — Antigravity will extract your skills, education, and career achievements.
2. **Paste CV:** Paste your existing CV directly into chat.
3. **Interactive Interview:** Antigravity will ask you targeted questions about your primary stack, years of experience, energizing tasks, and target contract/salary preferences.

All your verified data will be recorded in:
- `CLAUDE.md` (Quick candidate summary)
- `.claude/skills/job-application-assistant/01-candidate-profile.md` (Canonical candidate truth base)
- `cv/main_example.tex` (Master reference CV)

---

## 4. Test Compiling Your Master CV

Verify that your LaTeX environment is configured properly:

```bash
cd cv
lualatex -interaction=nonstopmode -halt-on-error main_example.tex
python3 ../tools/verify_pdf.py main_example.pdf --dump-text main_example.txt
cd ..
```

The output should confirm:
`Verified main_example.pdf (extractor: pypdf, pages: 2)`

---

## 5. Daily Job Search & Application Workflow

### Search for Positions
Ask Antigravity:
> *"Search LinkedIn for remote [Your Role] jobs in [Target Country/Region] posted in the last 14 days."*

### Apply to a Posting
Give Antigravity a job URL:
> *"Apply to this job: https://www.linkedin.com/jobs/view/XXXXXX"*

Antigravity will:
1. Run prompt-injection defense (`tools/posting_guard.py`).
2. Score technical match and check eligibility and language gates.
3. Tailor your 2-page CV and 1-page cover letter.
4. Have an adversarial reviewer subagent critique the drafts.
5. Compile PDFs with `lualatex` and `xelatex` and verify ATS parseability.

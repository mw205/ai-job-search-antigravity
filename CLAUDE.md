# Job Application Assistant for Mohamed Waleed

## Role
This repo is a job and project application workspace. The agent acts as a career advisor, opportunity researcher, and application assistant for Mohamed Waleed, helping with:
1. **Opportunity fit evaluation** - Assess postings (freelance, contract, part-time, full-time) against profile and stack
2. **CV tailoring** - Adapt master LaTeX CV (`cv/main_example.tex`) to target specific projects or roles
3. **Cover letter writing** - Draft targeted, high-converting cover letters using `cover_letters/cover.cls`
4. **Interview preparation** - Prepare answers, talking points, and client qualification questions
5. **Career & contract positioning** - Position for freelance, sub-contracting, and full-time remote engineering

## Candidate Profile

### Identity
- **Name:** Mohamed Waleed
- **Role:** Software Engineer (Flutter, Full-Stack Web, GenAI)
- **Location:** Mansoura, Egypt (Open to Remote Worldwide)
- **Email:** mohamedwaleedabdelghany@gmail.com
- **Phone:** +201092219806
- **Portfolio:** https://mw205.github.io/portfolio-/
- **LinkedIn:** https://www.linkedin.com/in/mohamedwaleed1/
- **GitHub:** https://github.com/mw205
- **Languages:**
  | Language | Level |
  |----------|-------|
  | Arabic | Native |
  | English | Professional working proficiency |
- **CV language:** English
- **Status:** Available for freelance projects, sub-contracts, part-time, and full-time remote contracts
- **LinkedIn headline:** "Software Engineer | Flutter & Full-Stack Web | GenAI Systems"

### Education
- **Bachelor of Computer and Information Sciences (Artificial Intelligence Program)** (2021-2025) - Faculty of Computer Science, Mansoura University (GPA: 3.38)
  - Focus: AI, Algorithms, Data Structures, Software Engineering
- **Professional Diploma in Open Source Applications Development** (2025-2026) - Information Technology Institute (ITI), 9-Month Scholarship, Mansoura Branch
  - Focus: Enterprise full-stack systems, frontend, backend, GenAI & tooling

### Professional Experience
- **Freelance Software Engineer** (Nov 2024 - Present) - Independent / Remote
  - Architected and delivered cross-platform mobile and web applications with Flutter and clean architecture (BLoC, Riverpod).
  - Built backend systems and REST APIs with Laravel and Node.js/Express, integrating MySQL, PostgreSQL, and Firebase.
  - Featured projects: Resto (Melos monorepo + TOTP 2FA), PropMatch (AI real estate platform), Mindly (EdTech with anti-piracy protections), GreenCar (on-demand booking).

### Technical Skills
- **Primary:** Flutter, Dart, Laravel, Vue.js, Node.js, Express.js
- **Secondary:** Python, Django, Angular, Tailwind CSS, Bootstrap, JavaScript/TypeScript
- **Databases:** PostgreSQL, MySQL, MongoDB, Firebase Firestore
- **AI & Tools:** GenAI, Gemini API, RAG, Git, Docker, Linux, Antigravity

### What Excites You
- Building robust mobile products from design to app store delivery
- Integrating applied AI (RAG, smart assistants) into real-world business workflows
- Writing clean, maintainable architecture (Melos monorepos, SOLID principles)

### Target Opportunities
- Freelance & Contract Mobile (Flutter) and Full-Stack Web Development
- Sub-contracting for agency client deliverables
- Remote Part-Time or Full-Time Engineering Contracts (Gulf, Europe, North America, Global)

### Deal-breakers
- Low-quality unverified work with unclear requirements and no escrow/milestone structure
- Onsite-only requirements that require daily physical presence outside Egypt without relocation support
- Work requiring technologies outside core competencies without reasonable onboarding time

## Repo Structure
- `cv/` - LaTeX CV variants (moderncv template, banking style)
- `cover_letters/` - LaTeX cover letters (custom cover.cls template)
- `.claude/skills/` - Canonical skill definitions for the application workflow
- `.agents/skills/` - Job search CLI tools & Antigravity skills

## Workflow for New Applications
1. User provides a posting URL or text (or discovered via `freehire-search` or `linkedin-search`).
2. Evaluate fit first: tech stack match, seniority match, contract type.
3. If good fit: generate tailored CV (`cv/main_<company>_<role>.tex`) and cover letter (`cover_letters/cover_<company>_<role>.tex`).
4. Run review critique with the `application-reviewer` subagent.
5. Compile PDFs (`lualatex` for CV, `xelatex` for cover letter).
6. Verify exact page counts (CV = exactly 2 pages, cover letter = exactly 1 page) and verify ATS text extraction with `verify_pdf.py`.

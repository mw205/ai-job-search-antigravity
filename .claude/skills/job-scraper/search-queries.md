# Search Queries for Job Scraper (Antigravity Edition)

<!-- SETUP: Run the job-setup skill or customize these queries for your skills, target roles, and locations -->

## Installed portal CLIs (primary for `/scrape` or `job-scraper`)

The `job-scraper` skill automatically discovers and runs portal skills under `.agents/skills/*/SKILL.md`:
- `freehire-search`: Tech, remote, contract, full-stack, mobile, AI/ML
- `linkedin-search`: Multi-market & remote search on LinkedIn

The queries below are used for portal queries and WebSearch fallback.

## Query Categories

### Priority 1: Primary Discipline & Role
Targets your core technical specialty across freelance, contract, and full-time remote roles.

```
"[YOUR_PRIMARY_ROLE]" Remote
"[YOUR_PRIMARY_SKILL] Developer" Remote
"[YOUR_PRIMARY_SKILL]" freelance contract
site:linkedin.com/jobs "[YOUR_PRIMARY_ROLE]" Remote
```

### Priority 2: Secondary / Adjacent Discipline
Targets secondary technical strengths or full-stack platforms.

```
"[YOUR_SECONDARY_ROLE]" Remote
"[YOUR_SECONDARY_SKILL]" Remote contract
site:linkedin.com/jobs "[YOUR_SECONDARY_ROLE]" Remote
```

### Priority 3: Applied AI / Modern Tooling
Targets modern engineering roles requiring applied AI, LLMs, or automation.

```
"AI Engineer" Remote
"Full Stack" "AI" Remote
site:linkedin.com/jobs "Software Engineer" "AI" Remote
```

### Priority 4: Freelance Contracts & Sub-contracting
Targets clients, agencies, or startups seeking contract engineers.

```
"[YOUR_PRIMARY_SKILL] contractor" Remote
"Freelance [YOUR_PRIMARY_ROLE]"
"Subcontractor" "Software Engineer" Remote
```

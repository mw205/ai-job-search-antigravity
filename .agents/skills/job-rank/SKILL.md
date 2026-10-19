---
name: job-rank
description: >-
  Batch score scraped or collected job postings against candidate fit criteria,
  detect dealbreakers, and output a ranked shortlist.
---

# Batch Job Ranking Workflow

Use this skill to batch-score scraped jobs against the candidate evaluation framework.

## Instructions
1. Follow the canonical procedure in [.claude/commands/rank.md](../../.claude/commands/rank.md).
2. Read jobs from `job_scraper/seen_jobs.json` or user input.
3. Use `tools/rank_state.py` to maintain triage state.
4. Filter out deal-breakers, language barriers, and expired postings.
5. Rank and output top matching opportunities for freelance/contract/full-time application.

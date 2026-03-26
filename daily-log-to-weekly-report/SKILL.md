---
name: daily-log-to-weekly-report
description: Convert messy daily work logs into a professional weekly report. Use when the user provides raw daily notes, task bullets, meeting notes, technical work items, deployment/debug records, or learning notes and wants a concise weekly summary, highlights, blockers, and next-week plan.
---

# Purpose

Turn raw daily engineering notes into a clean weekly report suitable for:
- manager updates
- self-review
- project tracking
- resume/project bullet extraction
- status sync documents

# Inputs

Expect one or more of:
- dated daily logs
- unordered bullet notes
- task fragments
- meeting notes
- debugging records
- deployment/update notes
- learning notes mixed with delivery work

# Required behavior

1. Read all provided notes carefully.
2. Separate **real deliveries** from:
   - learning-only notes
   - random links
   - incomplete thoughts
   - duplicated items
3. Merge repeated items across days into one coherent achievement.
4. Infer themes and group work into 3-6 meaningful categories.
5. Write in a professional tone.
6. Do not exaggerate impact.
7. If evidence is weak, say "worked on", "investigated", or "continued" instead of overstating.
8. Preserve important technical nouns, product names, model names, tools, and system names.
9. If dates are present, use them to infer weekly sequence.
10. If blockers or risks are not explicit, infer them conservatively only from the notes.
11. When useful, follow the structure in `assets/report_template.md`.

# Output format

Always produce these sections in order:

## Weekly Summary
A short paragraph with the week's overall focus and main outcomes.

## Key Deliveries
- 3 to 7 bullets
- each bullet should describe a concrete delivery, update, validation, integration, deployment, fix, or discussion outcome

## Technical Progress
Group progress under 2 to 5 sub-headings such as:
- Data Pipeline / ETL
- Model / Algorithm
- API / Backend
- Deployment / Infra
- Evaluation / Testing
- Coordination / Product Discussion

Under each heading, summarize the actual progress.

## Risks / Blockers
- concise bullets
- include only items supported by the notes or very conservative inference

## Next Week Plan
- 4 to 8 bullets
- practical and specific
- based on unfinished work and recent direction

# Style rules

- Be concise, factual, and professional.
- Avoid motivational language.
- Avoid vague claims like "significantly improved" unless the notes contain evidence.
- Prefer action verbs: implemented, updated, tested, deployed, validated, investigated, discussed, integrated, migrated, optimized.
- Keep the report manager-friendly, but technically credible.

# Optional extra mode

If the user asks, also append:

## Resume-worthy Highlights
- 2 to 5 bullets rewritten in achievement-oriented resume style

# When information is messy

If the notes are noisy:
1. first identify dated entries
2. cluster related work
3. remove pure reference links unless they support actual work
4. collapse duplicates
5. write the report from the cleaned cluster set

# Examples of user requests that should trigger this skill

- turn this daily log into a weekly report
- summarize my work this week
- make a weekly update from these notes
- convert my raw notes into a professional report
- extract this week's progress from my log

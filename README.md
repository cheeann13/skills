# AI Skills

A small library of practical Claude Code skills for everyday work in construction, project management, and corporate operations.

Each skill is a single markdown file with clear instructions for an AI agent. Anyone can read them, fork them, and adapt them for their own team.

This is an experimental learning library. I write skills as I encounter the same task three times — that's the threshold where a skill is worth more than just doing the work. Patterns surface from AI transformation programs I run with corporate teams; once a skill works for one team, it tends to work for many.

## What is a skill?

A skill is a reusable instruction set that tells an AI assistant how to handle a recurring task — the way you'd brief a junior staff member who's about to take over your inbox while you're on leave.

When you turn a workflow into a skill:

- The first person who masters the task writes it down once
- Everyone else on the team uses it forever
- Quality stays consistent across the team
- New joiners get up to speed faster

That's how AI knowledge stops disappearing into individual browser histories and becomes institutional IP.

## Available skills

| Skill | What it does |
|---|---|
| [`doc-to-dashboard`](./doc-to-dashboard/SKILL.md) | Turns a PDF, Excel, or CSV into a self-contained HTML dashboard with insights, anomalies, and inline charts |
| [`subcon-followup`](./subcon-followup/SKILL.md) | Drafts polite-but-firm follow-up emails to subcontractors or consultants from a few bullets |
| [`vo-summariser`](./vo-summariser/SKILL.md) | Drafts a Variation Order summary from site-change bullets, formatted for client signoff with cost / time / justification / approval recommendation |

More skills coming. If your team writes one worth sharing, send a pull request.

## How to use a skill in Claude Code

1. Clone or download this repository
2. Copy the skill folder you want into either:
   - Your project: `.claude/skills/[skill-name]/`
   - Globally: `~/.claude/skills/[skill-name]/`
3. In any Claude Code session, mention the skill by name or describe a task that matches its trigger conditions

The skill activates automatically when its `description` field matches what you're trying to do.

## How to write your own skill

Open any of the existing skills, copy the structure, change the content. The whole file is plain English. There is no code.

The most important part is the frontmatter — `name` and `description`. The description is what tells Claude when to use the skill, so be specific about the trigger conditions.

## License

MIT. Use freely. Adapt for your team. Share what works.

## Maintained by

Chee Ann · [cheeann.com](https://cheeann.com)

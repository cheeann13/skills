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

## Quick Start — try one skill in 60 seconds

You don't need to install anything to try these skills. Pick the path that matches your setup:

### Path 1 — Claude.ai or ChatGPT (no install, works in your browser)

1. Open the skill you want, e.g. [`doc-to-dashboard/SKILL.md`](./doc-to-dashboard/SKILL.md). Click the **Raw** button on GitHub to view the plain text.
2. Copy the entire content of the file.
3. Open Claude.ai (or ChatGPT) and start a new chat.
4. Paste this single message:

   > I want to use a skill called **doc-to-dashboard**. Below is the skill definition — please follow it exactly when I share my data.
   >
   > [paste the entire SKILL.md content here]
   >
   > Now I'll share my file in the next message.

5. In the next message, attach your file (PDF, Excel, or CSV) and tell Claude what context to use.
6. Claude follows the skill instructions and produces the output.

This works for every skill in this repo. Zero install. Best for non-technical users or for trying a skill once.

### Path 2 — Claude Code in your terminal (5 minutes, recommended)

For people who want the skill to be invoked automatically every time the trigger condition matches.

1. Make sure you have Claude Code installed: [docs.claude.com/en/docs/claude-code](https://docs.claude.com/en/docs/claude-code)
2. Open a terminal and run:

   ```bash
   mkdir -p ~/.claude/skills
   cd ~/.claude/skills
   git clone https://github.com/cheeann13/skills.git
   ```

3. Open Claude Code in any directory: `claude` in terminal.
4. Describe what you want to do. The skill activates automatically when its `description` matches your task.

   Example invocations the skills will recognise:
   - *"Summarise this site change as a Variation Order"* → triggers `vo-summariser`
   - *"Turn this spreadsheet into a dashboard"* → triggers `doc-to-dashboard`
   - *"Draft a follow-up email for a late submission"* → triggers `subcon-followup`

5. To update later: `cd ~/.claude/skills/skills && git pull`.

### Path 3 — Use it in your team's projects

If you want the skill scoped to one specific project (instead of globally), copy the skill folder into the project itself:

```bash
mkdir -p .claude/skills
cp -r ~/.claude/skills/skills/doc-to-dashboard .claude/skills/
```

Now when you run Claude Code from that project, the skill is available locally. Useful when different projects need different skill libraries, or when you want to commit a skill alongside the project that uses it.

## Per-skill quick start

### `doc-to-dashboard`

Drop a spreadsheet in. Get a dashboard out.

```
File: monthly_invoices_apr2026.xlsx
Context: monthly accounts payable register
Audience: my manager
Focus: late payments and supplier concentration
```

Claude returns a self-contained HTML file you can open in any browser, attach to email, or print to PDF. See [the full SKILL.md](./doc-to-dashboard/SKILL.md) for the 8 department adapters.

### `subcon-followup`

Three bullets in. A polite-firm follow-up email out.

```
Project: [project name]
Recipient: [name + role]
Subject of chase: Revised piling submission
Bullets:
- Revised piling design due 18 April, not received
- Calculations for piles B-12 to B-18 outstanding
- Method statement Rev 3 still pending review comments
Severity: standard
```

Severity calibrates the tone: gentle / standard / firm / final. See [the full SKILL.md](./subcon-followup/SKILL.md).

### `vo-summariser`

Site change in. Variation Order summary out, formatted for client signoff.

```
Project: [project code]
VO ref: VO-018
Triggered by: Site instruction dated 22 Apr 2026
Original scope: Foundation Type 2 piling per drawing F-101 Rev B
New scope: Upgrade to Type 3 piling for grid lines C-7 to C-12
Cost impact: RM 86,500
Time impact: 4 working days added to foundation milestone
Justification: Revised soil report showed lower bearing capacity in zone C
```

Output includes scope change, cost breakdown, time impact, justification, approval recommendation, and risk-if-not-approved. See [the full SKILL.md](./vo-summariser/SKILL.md).

## Troubleshooting

**The skill doesn't auto-trigger in Claude Code.** Reference it explicitly: *"Use the doc-to-dashboard skill on this file."* Auto-triggering is based on the description field — if your task wording is far from the description, Claude may not match it.

**The output isn't what I expected.** Check the "Style rules" and "What this skill is NOT for" sections of the skill — those define the boundaries. If your use case is genuinely different, fork the skill and edit those sections for your team.

**I want to add my own skill.** Copy any existing skill folder, change the content, edit the README to list yours, and send a pull request. The whole file is plain English — there's no code to write.

## How to write your own skill

Open any of the existing skills, copy the structure, change the content. The whole file is plain English. There is no code.

The most important part is the frontmatter — `name` and `description`. The description is what tells Claude when to use the skill, so be specific about the trigger conditions.

## License

MIT. Use freely. Adapt for your team. Share what works.

## Maintained by

Chee Ann · [cheeann.com](https://cheeann.com)

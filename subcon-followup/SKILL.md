---
name: subcon-followup
description: Drafts a polite-but-firm follow-up email to a subcontractor or consultant from 3-5 bullet points about what's overdue. Use when chasing missing submissions, late documents, or unanswered queries on construction projects. Adjust severity from gentle reminder to firm chase based on how overdue the item is.
---

# Subcontractor Follow-up Email Drafter

A skill for construction project teams who chase subcontractors and consultants on missing submissions, overdue documents, and unanswered queries.

## When to use this skill

Invoke this skill when you need to draft a follow-up email to a subcontractor or external consultant. Typical triggers:

- A submission is past its agreed deadline (drawings, calculations, method statement)
- A reply to a query is overdue
- A site issue needs documented chase-up before escalating
- A regular weekly status reminder is needed

## What you (the user) provide

A short brief in the chat. Format:

```
Project: [project name or code]
Recipient: [subcontractor/consultant name + role]
Subject of chase: [what you're chasing]
Bullets:
- [item 1 — what's missing, when it was due]
- [item 2]
- [item 3]
Severity: [gentle / standard / firm / final]
CC: [optional — names or roles, e.g., "PM Construction, Contracts Manager"]
```

If any field is missing, ask the user for it before drafting.

## What you (Claude) produce

A complete email ready to paste into Outlook/Gmail. Structure:

1. **Subject line** — clear, dated reference, project code if given
2. **Greeting** — professional, name-first
3. **Context line (1 sentence)** — anchors which project + what was agreed
4. **The ask (bulleted)** — restate items overdue, with original due dates if given
5. **Deadline + consequence** — explicit revised deadline; consequence calibrated to severity
6. **Closer** — collaborative tone, offer to discuss
7. **Sign-off** — professional, leaves space for the user's signature

## Tone calibration by severity

| Severity | Greeting | Closer | Consequence framing |
|---|---|---|---|
| **gentle** | "Hi [Name]" | "Appreciate your prompt response" | None — just a reminder |
| **standard** | "Hi [Name]" | "Please confirm receipt and proposed timeline" | Reference original schedule |
| **firm** | "Dear [Name]" | "We need this resolved before [date] to avoid programme impact" | Note schedule risk |
| **final** | "Dear [Name]" | "Failing your response by [date], we will escalate to [next level]" | Explicit escalation path |

## Style rules

- English. No Bahasa Malaysia, no Manglish.
- Professional, adult-to-adult tone. No "kindly" overuse, no overly long paragraphs.
- Include specific dates and document references. Vague chase emails get vague replies.
- Never use exclamation marks.
- Never threaten in "gentle" or "standard" severity.
- Always close with collaborative language even when severity is "firm" or "final".
- Keep total email under 200 words for gentle/standard, under 300 for firm/final.

## Example invocation

User pastes:
```
Project: [Sample Tower Block A]
Recipient: [Subcontractor name], Foundation subcontractor
Subject of chase: Revised piling submission
Bullets:
- Revised piling design due [date], not received
- Calculations for borepiles [range] outstanding
- Method statement Rev 3 still pending review comments from us
Severity: standard
CC: PM Construction, Contracts Manager
```

You draft something like:

```
Subject: [Project] — Outstanding Piling Submission (due [date])

Hi [Name],

Following up on the revised piling submission for [Project] — three items remain outstanding from our last project meeting:

  1. Revised piling design — original due date [date], not yet received
  2. Calculations for borepiles [range] — outstanding
  3. Method statement Rev 3 — pending your reply to our review comments (issued [date])

These items are on the critical path for our [milestone] date. Please confirm receipt of this note and propose a revised submission timeline for each item by EOB [day].

Happy to jump on a 15-min call this week if it helps unblock anything from your side.

Thanks,
[Your name]

CC: [PM Construction], [Contracts Manager]
```

## Adapt for related use cases

This same skill structure works for:

- Chasing consultant replies on RFIs (Requests for Information)
- Following up on E-Invoice / supplier payment queries
- Chasing internal departments for inputs (just adjust greeting and closer)
- Customer Service team chasing homeowner replies on defect rectification

For homeowner-facing chases, soften the greeting further and add a relationship-preserving line.

## What this skill is NOT for

- Initial briefs or scope documents — different skill.
- Internal team-to-team comms with strong existing relationships — overformal.
- Legal or contractual notices — those need legal review, not an AI draft.
- Anything requiring confidential commercial figures — keep those off public AI tools entirely.

## Notes for skill authors

This skill is part of an experimental shared-skill pattern for Malaysian construction teams. To adapt it for your firm:

1. Edit the "Style rules" section to match your house tone
2. Update the "Tone calibration" table with your firm's escalation conventions
3. Replace the example with one from your own project library
4. Add company-specific abbreviations to the prompt (e.g., your VO format, your project code structure)

To use this skill in Claude Code, save this file as `SKILL.md` inside `.claude/skills/subcon-followup/` in your project, or globally at `~/.claude/skills/subcon-followup/`. Then invoke it by referencing the skill name in any Claude Code session.

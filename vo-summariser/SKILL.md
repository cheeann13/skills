---
name: vo-summariser
description: Drafts a Variation Order summary from a few bullets about site changes, formatted for client signoff. Includes scope change, cost impact, time impact, justification, and approval recommendation. Use when a project change has been agreed on site and needs to be turned into a formal VO document for the client and contracts team. Calibrates the level of formality based on cost and time impact.
---

# Variation Order Summariser

A skill for construction project teams who turn agreed site changes into formal Variation Order summaries for client signoff. Replaces the hour-or-two of reformatting that a PE or PM does after every site meeting.

## When to use this skill

Invoke when:

- A site change has been verbally agreed and needs to be documented
- A subcontractor has raised a VO request that needs your draft response
- The contracts team needs a structured summary before generating the formal VO instrument
- A weekly batch of small VOs needs to be packaged for the client

## What you (the user) provide

A short brief in the chat:

```
Project: [project name or code]
VO ref: [optional — auto-suggest if not given]
Triggered by: [site instruction / consultant note / RFI / variation request]
Original scope: [what was in the contract]
New scope: [what is now being done]
Cost impact: [RM amount, with breakdown if available — or "to be quantified"]
Time impact: [days added or saved — or "no impact"]
Justification: [why the change is needed]
CC: [optional — names or roles, e.g. "Project Director, Contracts Manager"]
```

If any of `Original scope`, `New scope`, or `Justification` is missing, ask before drafting. Without these, the VO will be too generic to be approved.

## What you (Claude) produce

A complete Variation Order summary structured for client signoff. Eight sections:

1. **Header**: Project name + code, VO reference, date, addressed-to, prepared-by
2. **Background** (1 sentence): What triggered the change. Who instructed or raised it.
3. **Scope Change**: Clear before-and-after, in plain language. Include drawing references, specification clauses, or BOQ item numbers if given.
4. **Cost Impact**: RM amount with breakdown (materials, labour, P&P, sub-contractor) where available. Include calculation basis. Flag if quantification is pending.
5. **Time Impact**: Days added or saved, and which milestone(s) shift as a result.
6. **Justification**: Why this change is necessary. Concrete reasons — site condition, design clash, client request, regulatory requirement, value engineering.
7. **Approval Recommendation**: Recommend approve / approve-with-conditions / decline-with-alternatives. Include the level of authority needed based on cost threshold.
8. **Risk if Not Approved**: 1-2 lines on what happens if the client doesn't approve — schedule impact, safety risk, abortive work, contractual exposure.

## Severity calibration

Adjust formality and required signoff level based on cost and time impact:

| Severity | Cost trigger | Time trigger | Tone | Signoff |
|---|---|---|---|---|
| **Minor** | Below RM 25k | No critical-path impact | Concise, single-page | PM authority |
| **Moderate** | RM 25k – RM 100k | 1-3 days | Detailed, with references | Project Director |
| **Significant** | RM 100k – RM 500k | 3-10 days | Full justification + risk | Client representative |
| **Major** | Above RM 500k | Over 10 days or critical-path | Formal, with alternatives | Client + main contractor sign-off |

The thresholds are conservative defaults. Adapt to your firm's contract delegation matrix.

## Style rules

- English. No Bahasa Malaysia in the body. (BM appendix optional if requested.)
- Professional, factual tone. Adult-to-adult. No "kindly" overuse.
- Include specific references — drawing numbers, RFI numbers, original BOQ items, dates of site meetings.
- Currency formatted as `RM 123,456.78` with two decimals only when fractional.
- Dates rendered as `DD MMM YYYY` (e.g., "27 Apr 2026").
- Cost breakdowns shown as a table, not prose.
- Justification must be specific. "Required due to revised soil report dated [date]" — not "due to site conditions."
- Never threaten or guilt-trip the client. The VO is a record, not a negotiation.
- If cost or time is uncertain, write "to be quantified by [date]" with a clear next step. Don't fabricate numbers.

## Example invocation

User pastes:

```
Project: [Sample Tower Block A — TBA-2026]
VO ref: VO-018
Triggered by: Site instruction dated 22 Apr 2026 from Project Director
Original scope: Foundation Type 2 piling per drawing F-101 Rev B
New scope: Upgrade to Type 3 piling for grid lines C-7 to C-12 due to revised soil report
Cost impact: RM 86,500 — materials RM 52,000 / labour RM 28,000 / equipment RM 6,500
Time impact: 4 working days added to foundation phase milestone
Justification: Revised soil report dated 18 April 2026 from [consultant] showed lower bearing capacity in zone C than original investigation
CC: Project Director, Contracts Manager
```

You draft:

```
VARIATION ORDER SUMMARY — VO-018
Project:        [Sample Tower Block A] (TBA-2026)
Date:           27 Apr 2026
Addressed to:   [Client representative]
Prepared by:    [Your name]
CC:             Project Director, Contracts Manager

1. BACKGROUND
   Site instruction dated 22 Apr 2026 from the Project Director, following
   the revised soil report (dated 18 Apr 2026) which indicated lower
   bearing capacity than the original soil investigation in foundation
   zone C.

2. SCOPE CHANGE
   Original (per drawing F-101 Rev B):
     Foundation Type 2 piling — grid lines C-7 to C-12.

   Revised:
     Foundation Type 3 piling — grid lines C-7 to C-12.

   Drawing F-101 Rev C to be issued by [consultant] reflecting the change.

3. COST IMPACT
   | Item       | Amount (RM) |
   |------------|-------------|
   | Materials  | 52,000.00   |
   | Labour     | 28,000.00   |
   | Equipment  |  6,500.00   |
   | TOTAL      | 86,500.00   |

   Basis: 6 piling locations, Type 3 unit rate per current sub-contractor
   schedule.

4. TIME IMPACT
   4 working days added to the foundation phase milestone.
   Revised foundation completion: 12 May 2026 (originally 6 May 2026).
   No impact to overall practical completion if recovery measures in
   the structural works phase are implemented as per Mitigation Plan
   (separate document).

5. JUSTIFICATION
   The revised soil report identified bearing capacity in zone C below
   the threshold required for Type 2 piling. Type 3 piling is necessary
   to meet structural design loads safely and to maintain compliance
   with the structural engineer's specification.

6. APPROVAL RECOMMENDATION
   APPROVE. Cost and time impact are within the moderate band; approval
   authority sits with the Project Director and Client representative
   per the contract's delegation matrix.

7. RISK IF NOT APPROVED
   Continuing with Type 2 piling against the revised soil report would
   expose the project to structural risk and potential rework. Delay in
   approval beyond 30 Apr 2026 will push the foundation milestone by
   each day held.

[Your name]
[Role / Project]
```

## Adapt for related use cases

This skill structure also works for:

- Subcontractor variation requests (you receive, you respond) — invert "your" perspective; use this format to document your reply.
- Client-instructed scope additions — same template, with "Triggered by" reading "Client instruction dated [date]."
- Value-engineering proposals — adjust Section 6 to "Recommend evaluate" with options.
- RFI-driven variations — link the RFI number in the Background section.

## What this skill is NOT for

- Initial contract drafting or BOQ generation — different skill.
- Disputed claims or extension-of-time submissions — those need contractual specialists, not an AI draft.
- Confidential commercial figures (subcontractor private rates, client margin) — keep those off public AI tools entirely.
- Final VO instruments. This is a SUMMARY for the contracts team to convert into the formal contractual document. The legal instrument is contracts-team work.

## Notes for skill authors

To adapt for your firm:

1. Edit the `Severity calibration` table to match your firm's delegation matrix and authority limits.
2. Replace the example references (`F-101`, `TBA-2026`) with formats your team recognises.
3. Add common drawing-reference, RFI, and BOQ formats your projects use.
4. If your firm uses a fixed VO template (e.g., a specific BIM-extracted or contract-management-system format), point this skill at that template instead of generating from scratch.
5. For Malaysian construction contracts, consider adding PAM 2018 or PWD 203A clause references where relevant.

To use this skill in Claude Code, save this file as `SKILL.md` inside `.claude/skills/vo-summariser/` in your project, or globally at `~/.claude/skills/vo-summariser/`. Invoke it by mentioning a VO request with the required fields.

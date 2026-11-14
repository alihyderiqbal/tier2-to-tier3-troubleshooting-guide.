# Incident RCA Template

*Evidence-linked root cause analysis for engineering, plus a customer update block.*

**How to use:** Part A is for engineers and for my portfolio. Part B is for customers. Fill in Part A first, then write Part B from it so the two never contradict each other. Delete the guidance text in *italics* when filling in.

## The evidence rule

**Every causal claim must cite a piece of evidence by ID (for example `[E3]`).** Evidence is a log line, a payload, a query result, a screenshot or a trace, listed in the Evidence Index at the end. If a statement has no evidence, label it **Assumption** and say how it could be checked. No evidence, no claim.

## Definitions

- **Symptom:** what the user or system showed (for example, failed syncs, an error response).
- **Trigger:** the event that started the failure (for example, a change in the data being sent).
- **Root cause:** the underlying condition that, if removed, would have prevented the incident.
- **Contributing factor:** something that made the incident possible, worse or harder to detect, but did not start it on its own (for example, missing validation).

---

# Part A: Engineering RCA

## 0. Incident details

| Field | Value |
|---|---|
| Title | |
| Incident ID | *(simulated or sanitised)* |
| Start and end (with timezone) | |
| Priority / severity | |
| Status | Investigating / Identified / Monitoring / Resolved |
| Author | |
| Reviewers | |

## 1. Summary

*Two or three sentences: what failed, for whom, why, and how it was resolved. Cite evidence.*

## 2. Impact

- **Who and what was affected:** *(users, tenants, endpoints, records)* `[E#]`
- **Duration:** 
- **Data integrity:** *Lost, duplicated, delayed or unaffected? Will failed events replay? Only state replay if verified.* `[E#]`
- **Business or SLA impact:** 

## 3. Timeline

*Use one timezone throughout. Every row needs evidence.*

| Time | Event | Evidence |
|---|---|---|
| | First failure observed | `[E#]` |
| | Issue reported | `[E#]` |
| | Investigation started | |
| | Root cause identified | `[E#]` |
| | Fix or workaround applied | `[E#]` |
| | Resolution validated | `[E#]` |

## 4. Investigation

**Initial hypothesis:** *"I think X is happening because Y."*

| Hypothesis | Verdict (confirmed / ruled out / unresolved) | Evidence |
|---|---|---|
| | | `[E#]` |
| | | `[E#]` |

**Working vs failing comparison:** *What differed between a working case and a failing one?* `[E#]`

**What changed:** *Releases, configuration, credentials, integrations, data shape, and how the timing lines up.* `[E#]`

## 5. Root cause

*One clear statement. Cite evidence.* `[E#]`

## 6. Contributing factors

*What made the incident possible, worse or harder to detect?* `[E#]`

## 7. Detection

- How was the issue found?
- How could it have been detected sooner?

## 8. Resolution or workaround

*What was done, by whom, and what is permanent versus temporary.*

## 9. Validation

*How I confirmed the fix, using the same kind of evidence that showed the failure.* `[E#]`

## 10. Prevention and follow-ups

| Action | Type (detect / prevent / mitigate) | Owner | Status |
|---|---|---|---|
| | | | |

## 11. What I would check with more access

*Access-free reasoning: what I would look at beyond my permissions, and why.*

## 12. Confidence and open questions

- **Confidence in the root cause:** High / Medium / Low, and why
- **Open questions:**
- **Assumptions (unsupported by evidence):**

## Evidence Index

| ID | Type (log / payload / SQL / HAR / screenshot) | Description | Reference (sanitised) |
|---|---|---|---|
| E1 | | | |
| E2 | | | |
| E3 | | | |

---

# Part B: Customer update block

*Write this after Part A. The readers are technical (IT admins, integrators, operations managers) and must report upward, so be specific about their side and plain about ours.*

```
Subject: [Status] – [short description of the problem]

Status: Investigating / Identified / Monitoring / Resolved

What happened
[Plain description. Be specific about their side: endpoint, field names,
status codes, example payload shape.]

Impact and data integrity
- Affected: [what and how many]
- Data: [lost / duplicated / delayed / unaffected]
- Failed events: [will / will not replay automatically, ONLY if verified.
  Otherwise: "We are confirming whether failed events will replay."]

Confirmed so far
- [Facts supported by evidence]

Still being checked
- [Open questions]

Workaround (if any)
[Steps they can take now, for example reverting a setting, adjusting a
payload field or re-triggering manually.]

What we need from you (if anything)
[Specific, answerable requests.]

Next update
[A specific time you can keep. If no fix yet, say so, and still give a time.]
```

## Writing rules for customer updates

1. **Specific about their side, silent on our internals:** field names, status codes and payload shape are fine. Internal infrastructure, service names, other customers and internal process are not.
2. **Confirmed versus unconfirmed:** keep the two lists separate. Do not present a hypothesis as a fact.
3. **No promises you can't keep:** no guaranteed fix times, and no claims about replay or data recovery unless verified.
4. **Commit only to next-update times you can meet.** A missed update damages trust more than a vague one.
5. **No blame:** describe what happened, not whose fault it was.
6. **One timezone,** stated explicitly.
7. **Consistency check:** every statement in Part B must match Part A.

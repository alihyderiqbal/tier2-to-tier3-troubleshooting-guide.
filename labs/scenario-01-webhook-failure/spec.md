# Scenario-01: Simulated Webhook Delivery Failure

> **Simulated environment (`simulated-webhook-lab`).** Everything here is fictional: systems, tenants, IDs, payloads and logs. It does not describe any real vendor, employer or customer, and it does not reproduce any real product's behaviour.

*Status: design spec. The evidence pack is generated in the next session.*

## 1. Learning objectives

By the end of this lab I should be able to:

- Isolate variables by comparing working and failing events.
- Trace one request across layers using a correlation ID (delivery record → receiver logs → database).
- Use read-only SQL to check what actually happened to the data.
- Resist a plausible but wrong explanation (the red herring).
- Separate symptom, trigger, root cause and contributing factor.
- Write an evidence-linked RCA and a customer update, and describe what I would send to engineering.

## 2. Setting

A fictional **Sender System** posts event notifications (webhooks) to a fictional **Receiver Service** that stores them in a database. A customer administrator reports that some events are not arriving. The Sender's delivery dashboard shows repeated retries.

| Component | Role in the lab |
|---|---|
| Sender System | Produces events, records delivery attempts and retries |
| Receiver Service | Exposes the webhook endpoint, validates and stores events |
| Application logs | Receiver-side logs with correlation IDs |
| Database | Read-only SQLite snapshot of what the Receiver stored |

## 3. What I receive (the evidence pack)

The lab is delivered as an **evidence pack, not source code.** This mirrors Tier 2 reality, where I can see logs, data and delivery records but cannot read the application's code.

- A customer ticket describing the symptom
- A delivery export from the Sender (attempts, timestamps, status, retry counts)
- Receiver application logs for the incident window, with realistic noise
- A read-only SQLite database snapshot
- A small set of sample event payloads

**Access rules:** read-only SQL; no code access; no changing the data. Optional stretch: a local replay script for sending payloads to a stand-in receiver. If I use it, I do not open its source.

## 4. Design constraints (for the generator)

The following are build requirements, not hints about the defect.

1. **Exactly one planted defect.** No accidental second failure.
2. **Exactly one red herring:** plausible, visible in the evidence, and unrelated. It can be ruled out with evidence in the pack.
3. **Partial blast radius.** Some events succeed and some fail, so working-versus-failing comparison is possible.
4. **Realistic noise:** unrelated warnings, healthy traffic from other tenants, mixed timestamps with explicit timezones.
5. **Consistency across artifacts:** counts and timestamps in the delivery export, logs and database must agree.
6. **Status codes are deliberate evidence.** The status class the Receiver returns must matter for the RCA.
7. **Realistic retry behaviour:** a backoff schedule, and a defined final state after the last attempt.
8. **Difficulty target:** solvable in 60 to 90 minutes with the evidence pack alone.
9. **No giveaways:** file names, column names, comments and metadata must not hint at the cause.
10. **Vendor-neutral and fully synthetic.**

## 5. My task

Time-box: **90 minutes.** Keep a **raw investigation log in my own words** as I go (timestamp, what I checked, what I saw, what I concluded). Then produce:

1. A written hypothesis (before and after investigation)
2. An RCA using `rca-templates/incident-rca-template.md`, with every causal claim cited to evidence
3. A customer update block (Part B of the template)
4. An escalation package: what I would send to engineering, and what I would check with more access

## 6. Hint ladder

Hints are requested one at a time, and **each one I use is recorded in my RCA** with the time.

| Level | Type | What it gives |
|---|---|---|
| Hint 1 | Method nudge | A question about approach, with no pointer to the cause |
| Hint 2 | Evidence pointer | Which part of the evidence pack to examine, and what to compare |

Opening the answer key before submitting my RCA **voids the lab.** If that happens, I note it and move on to a new scenario rather than pretending it was blind.

## 7. Review rubric

After I submit my RCA, it is reviewed against the answer key. Each criterion is rated **Met / Partly met / Not met**, and the review comments on my reasoning as well as my conclusion.

| Criterion |
|---|
| Root cause correctly identified and distinguished from the trigger |
| Contributing factor identified |
| Red herring ruled out with cited evidence |
| Every causal claim cites an evidence ID; assumptions are labelled |
| Timeline matches the evidence |
| Working-versus-failing comparison is shown |
| Customer update separates confirmed from unconfirmed and makes no unverified promises |
| Escalation package is complete and includes what I would check with more access |
| Hints used and time taken are recorded honestly |

## 8. Generation quality gate

Before the lab is released, the generator must confirm:

- [ ] Only one defect exists, and it reproduces deterministically
- [ ] The red herring is genuinely unrelated
- [ ] Delivery export, logs and database tell the same story (counts and timestamps reconcile)
- [ ] Nothing in file names, columns, comments or metadata gives away the answer
- [ ] The answer key matches the generated files exactly, down to record and line references
- [ ] No real names, vendors or data appear anywhere

## 9. Repo handling

- `answer-key.md` is **not committed** until my RCA is written. Add it to `.gitignore` until then.
- The generator and any source that reveals the defect stay out of the repo until after the RCA, then are added alongside the key.
- The evidence pack, spec and my RCA can be committed as normal.
- Before committing, check that nothing is traceable to a real employer, customer or colleague.

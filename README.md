# Tier 2 → Tier 3 Investigation Framework

*Status: v0.1 skeleton. To be revised after completing Scenario-01.*

A practical, evidence-first approach to investigating technical problems in SaaS support: isolate variables, trace an issue across the stack, prove the root cause, and hand off (or resolve) with confidence.

All examples in this repo are sanitised or simulated. Nothing here describes a real employer, customer or system.

---

## The investigation loop

### 1. Define the problem and its impact
- What is failing, for whom, and since when?
- How many users or records are affected? Is there data loss, duplication or a security angle?
- How close is the SLA? Set priority from impact and urgency, not from how interesting the problem is.

### 2. Scope and isolate
- Can I reproduce it consistently, or is it intermittent?
- What is the blast radius: one user, one tenant, one browser or OS, one endpoint, or everyone?
- Have I ruled out user error, misconfiguration and permissions?
- **Compare a working case with a failing one** (another tenant, an earlier date, a different payload). The difference is usually the clue.

### 3. Ask "what changed?"
- Recent deployments or releases
- Configuration or permission changes
- Rotated or expired credentials and tokens
- New or modified integrations
- Changes to the shape of the data being sent (fields, types, nulls, lengths)
- Does the first failure line up in time with any of these?

### 4. Gather evidence across the stack

| Layer | What to collect | Typical tools |
|---|---|---|
| Client / UI | Exact steps, timestamp, user and tenant, browser console and network trace (HAR) | Browser DevTools |
| API | Request and response: URL, method, headers, payload, status code | Postman, curl |
| Integration | Webhook delivery logs, retry behaviour, queue state | Delivery dashboards, logs |
| Application | Correlation or request IDs, stack traces, timeouts | Log viewer, grep |
| Database (read-only, if permitted) | Whether the data was written, missing or stuck; constraint errors | SQL `SELECT` queries |
| Auth / permissions | Token validity and expiry, scopes, role assignments | Token inspection, admin console |

**Status codes are clues, not verdicts.** A 4xx usually means the request was rejected (client or contract problem). A 5xx usually means the server failed while handling it. Both can point at the same underlying change.

### 5. Form a hypothesis, then try to disprove it
- State it plainly: "I think X is happening because Y."
- List the evidence for it and the evidence against it.
- List the alternatives I ruled out, and how.
- Beware the obvious but wrong explanation (timeouts, rate limits and expired tokens are common red herrings).

### 6. Decide: resolve, work around, or escalate
Escalate when:
- Configuration, permissions and known workarounds are ruled out, **and** the fix needs code, database writes or schema changes, infrastructure, or internal services I cannot reach.
- Impact or urgency is high (data loss, security, SLA at risk). Escalate early with what I have rather than finishing the investigation first.
- I have exceeded my time-box without narrowing the problem.

If I lack access, I still write down **what I would check with access, and why.** That is what separates advanced Tier 2 from stuck Tier 2.

### 7. Validate and write up
- Confirm the fix with the same evidence that showed the failure.
- Record the root cause and any contributing factors separately.
- Write the RCA (see `rca-templates/`) and the customer update.

---

## The escalation package

A good escalation lets engineering start work without repeating mine.

- [ ] Summary and impact
- [ ] Steps to reproduce
- [ ] Timestamps (with timezone)
- [ ] Correlation, request or record IDs
- [ ] A failing and a working example (sanitised payloads and responses)
- [ ] Relevant log snippets
- [ ] What changed, and when
- [ ] My hypothesis, with evidence for and against
- [ ] What I ruled out
- [ ] Workaround and customer-communication status
- [ ] What I would check with more access

---

## Repository map

| Path | Purpose | Status |
|---|---|---|
| `README.md` | This framework | Skeleton |
| `playbooks/post-escalation-debrief.md` | Questions to ask engineers after an escalation closes | Planned |
| `labs/scenario-01-webhook-failure/` | Blind lab: silent payload/schema change with webhook retries | Planned |
| `rca-templates/incident-rca-template.md` | Evidence-linked RCA and customer update template | Planned |
| `PROJECT_PLAN.md` | Roadmap, responsibilities and success criteria | Done |

---

## Ground rules

1. **Evidence rule:** every causal claim cites a log line, payload or query result.
2. **Blind labs:** the answer key stays hidden until my RCA is written; any hints I use are recorded.
3. **Sanitised or simulated only:** no real customer, employer or vendor details.

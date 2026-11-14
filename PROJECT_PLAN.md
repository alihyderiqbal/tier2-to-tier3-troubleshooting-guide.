# Project Plan: Tier 2 → Tier 3 Investigation Portfolio (v1)

*Status: v1 plan. Created 14 November 2026.*

## 1. Goal

Build a public GitHub repository that shows how I investigate a technical problem across the stack (API → logs → database), prove the root cause with evidence, and communicate the findings clearly enough to hand straight to engineering.

## 2. Vision and audience

- **Primary purpose:** my own development from intermediate Tier 2 to advanced Tier 2 and, eventually, Tier 3 Technical Support Engineer.
- **Secondary purposes:** share selected material with other technical support professionals, publish write-ups on LinkedIn, and use the repo as a portfolio project for UK employers.
- **Two-minute takeaway for a hiring manager:** this engineer does not guess or blindly escalate. They isolate variables systematically, trace issues across the stack, and communicate findings clearly.
- **Approach:** a portfolio of troubleshooting evidence, not a textbook. Each scenario shows the problem, the evidence collected, the investigation, the tools used, the root cause and how the fix was validated.

## 3. Scope

**In scope for v1**

- One investigation framework (README)
- One post-escalation debrief checklist
- One blind lab: a silent payload/schema change combined with webhook retries
- One RCA and customer update template
- One completed RCA from the lab

**Out of scope for v1**

- The remaining topic areas (see the expansion backlog)
- Cloud infrastructure labs
- Multiple scenarios

**Lab environment:** local only (laptop with Postman, curl, Python, SQLite or PostgreSQL, a Linux terminal). No heavy cloud setup.

## 4. Deliverables and responsibilities

| # | Deliverable | Me | Claude | Done when |
|---|---|---|---|---|
| 1 | `README.md` investigation framework | Supply real triage gates; check against real tickets | Structure them; add hypothesis, "what changed?", priority and access-free reasoning | One-page skeleton exists; revised after the lab |
| 2 | `playbooks/post-escalation-debrief.md` | Choose the engineers; pilot on a real closed escalation | Draft 4–5 questions, including what they checked first and why | Piloted at least once and revised |
| 3 | `labs/scenario-01-webhook-failure/` | Investigate blind; log every hint used | Build the simulated stack, noisy logs, one red herring, a 2-step hint ladder and a separate answer key | Lab runs; key hidden |
| 4 | `rca-templates/incident-rca-template.md` | Provide findings and evidence | Template with evidence-linked claims and a customer update block | Used on the first RCA |
| 5 | First completed RCA | Raw investigation log, root cause, validation | Review against the key; critique the reasoning | Committed, with the key added afterwards |

## 5. Delegation map

| Task | Skills needed | What AI handles | What needs my judgement | Main risk → mitigation |
|---|---|---|---|---|
| 1. Framework | Request-flow mental model; isolating variables; escalation criteria | Structure, wording, suggesting missed checks | My real escalation criteria; what Tier 2 access allows | Generic blog-post framework → I supply the gates; revise after the lab |
| 2. Debrief checklist | Technical grounding; tactful questioning | Draft a short question set | Who to ask, when, and what is useful rather than intrusive | Sounds like an audit, or assumes how Tier 3 works → pilot it; keep it under 5 questions |
| 3. Blind lab | Simulated stack; realistic failure modes; logs; SQL | Build the lab, noisy logs, red herring, hint ladder, key | Realism; honest investigation; difficulty | Accidental second bug; logs too clean; peeking → verify the lab; add noise; keep the key separate |
| 4. RCA template | Symptom vs trigger vs root cause; two-audience writing | Structure, plain-language rewriting, consistency | Deciding the true cause; what may be promised or disclosed | Fluent but unsupported causal chains → every claim cites an artifact |
| 5. First RCA | All of the above, plus discipline | Review against the key; later a LinkedIn version | The investigation, the conclusion, what to publish | Over-polished RCA that no longer shows my thinking → keep a raw log; AI polishes the final copy only |

## 6. Timeline

| When | What | Time |
|---|---|---|
| Hour 1 | Draft deliverables 1, 2 and 4 and the lab design spec | 15 + 10 + 15 + 20 min |
| Session 2 | Claude generates the lab and key (kept separate); I investigate blind | 2–3 hours |
| Session 3 | Write the RCA, review against the key, commit | 2–3 hours |
| After v1 | LinkedIn post from the RCA; Scenario-02 | Ongoing, 2–3 hours a week |

## 7. Success criteria for v1

- [ ] All five deliverables are in the repo, and the README makes sense to a stranger.
- [ ] The lab was investigated blind, and the RCA records any hints used.
- [ ] Every causal claim in the RCA cites a log line, payload or query result.
- [ ] The RCA separates the root cause from contributing factors (for example, the sender's contract change versus the receiver's missing validation).
- [ ] The debrief checklist has been piloted on at least one real escalation.
- [ ] Nothing in the repo is traceable to an employer, customer or colleague, and the lab is labelled as simulated.
- [ ] I can explain the investigation aloud in two minutes without notes.

## 8. Standing rules

1. **Confidentiality:** only sanitised or simulated content. No customer information, internal processes, private logs or identifiable details.
2. **Replies stay private:** answers from colleagues in debriefs are used to improve the checklist, not pasted into the repo.
3. **Evidence rule:** every causal claim cites a concrete artifact (log line, payload or SQL output).
4. **Answer key:** committed only after the RCA is written.
5. **Raw log first:** I keep an investigation log in my own words before AI polishes anything.
6. **No vendor imitation:** the lab is a generic simulated environment and is labelled as such.
7. **Customer updates:** state what is confirmed versus still being checked, and commit only to update times I can keep.

## 9. Expansion backlog (ideas, not commitments)

Each new topic becomes a scenario using the same pattern: blind lab, raw log, evidence-linked RCA.

- Scenario-02: authentication and permissions failures (token expiry, scopes)
- Scenario-03: networking (DNS, TLS, connectivity)
- Scenario-04: Linux and Windows diagnostics (logs, services, command line, PowerShell and Bash)
- Scenario-05: database troubleshooting (slow queries, locks, constraint errors)
- Scenario-06: incident management (SLAs, prioritisation, escalation under time pressure)

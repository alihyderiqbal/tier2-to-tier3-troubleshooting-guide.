# Post-Escalation Debrief Checklist

*A five-minute, low-friction way to learn how engineers investigate, and to make my next escalation cleaner.*

## Purpose

After an escalation closes, I only see the outcome, not the investigation. This checklist closes that gap. It is **not** a review of the engineer's work or of how long the fix took. It is a way for me to learn what a good investigation looks like and what my handoff was missing.

## When to use it

- Right after an escalation closes, while it is still fresh.
- Asynchronously (a short message thread), or as the last two minutes of an existing call.
- For non-routine escalations only. A quick, obvious fix doesn't need a debrief.
- No more than one or two debriefs a week with the same person.

## The five questions

1. **What did you check first, and why?**
   *Teaches me where an experienced engineer starts and what they treat as most informative.*
2. **What did you rule out, and how?**
   *Shows me which alternatives were considered and what evidence eliminates them.*
3. **What was the deciding clue that pointed to the cause?**
   *The single observation that mattered most, which I can learn to look for.*
4. **What in my escalation saved you time, and what was missing?**
   *Direct feedback on my handoff package.*
5. **What could I have checked or tried at my level before escalating?**
   *Separates what genuinely needed engineering access from what I could have done myself.*

## Ready-to-send message (shortened for chat)

> Thanks for picking up that escalation. If you have five minutes, could you reply with a line or two on each of these? It's to make my next handoff cleaner, not to review the fix.
>
> 1. What did you check first, and why?
> 2. What did you rule out, and how?
> 3. What was the deciding clue?
> 4. What in my handoff helped, and what was missing?
> 5. What could I have tried at my level before escalating?

## After the debrief

1. Write a short private note in my own words: what I learned and what I'd do differently.
2. Turn each lesson into a **generic** statement that could apply to any system. For example: *"Compare a failing payload with a working one before reading logs."*
3. Update the investigation framework (`README.md`) or the escalation package checklist if the lesson is general.
4. Thank them, and tell them what I changed because of their answers. That keeps the next debrief easy to get.

## Privacy reminder (read before committing anything)

**Do not log private replies in this repository.** That includes quotes, paraphrases or summaries that could be traced back to a person, a ticket or a customer.

Before committing anything inspired by a debrief, check that it contains none of the following:

- Names, usernames or job titles of colleagues
- Ticket, case or incident IDs
- Customer, company, product or tool names that identify a workplace
- Internal process descriptions, logs or screenshots

Only generic lessons that stand on their own belong in the repo.

## Pilot and refine

I will pilot this on a real closed escalation, then adjust the wording based on which questions drew useful answers. The pilot notes stay private.

# Example plan: running AI quality and adoption after launch

> This is an illustrative plan written for this casebook. It is not taken from any employer and contains no confidential information. It picks up where [case 5](05-example-prd-ai-chat-handoff.md) stops: the handoff feature has shipped, and now a team has to keep it good. It shows how I would run that as the product owner or AI lead.

## Context

A travel company's AI chat assistant has launched human handoff to 10% of traffic in one market. The PRD had an offline eval set and a release gate. What it did not have was an owner for quality once the feature was live, a routine for looking at it, or a plan for getting support agents to trust the AI summaries.

## Problem

Launch plans for AI features usually end at "monitor in production". In practice nobody owns the eval set after week two, prompt and model changes ship because they look better in a demo, and the people downstream (here, support agents) quietly stop using the output if it lets them down twice. Quality drifts and nobody can say when it started.

## What I would set up

**One owner and a weekly 30-minute quality review.** The product owner owns the eval set and the review. Attendees: one engineer, the support lead and whoever changed a prompt or model that week. The agenda is fixed:

1. Eval scores since last week, against the release gate
2. Ten handed-off conversations picked at random, read together
3. Agent ratings of summaries (requirement R7 in case 5) and any comments
4. Decide: keep, tune or roll back

**An eval set that grows from real failures.** Every bad handoff or wrong summary found in review becomes a new labelled case, with personal data removed first. The set starts at around 200 conversations and only grows. Cases are never deleted to make a score look better.

**Decision rules written down before anyone needs them.**

| Signal | Rule |
| --- | --- |
| Summary accuracy on the eval set drops after a prompt or model change | Do not ship the change. No exceptions for "it reads better" |
| Handoff rate moves by more than a third in a week | Review that day, roll back the last change if it explains it |
| Any summary contains card or passport data | Stop the feature for that market, fix, add a test, then restart |
| Agent summary ratings fall for two weeks running | Pause the next rollout stage until the cause is found |

**Cost as a guardrail, not an afterthought.** Track cost per handed-off conversation alongside quality. A change that improves accuracy slightly but doubles cost goes back to the review, not straight to production.

## Adoption: getting agents to rely on the summary

The feature only works if agents read the summary instead of scrolling the transcript. That is a trust problem, and trust comes from the agents seeing it be right.

- **Start with a few volunteer agents** who give feedback in a shared channel. Their comments shape the first round of prompt changes.
- **Show the source.** Every fact in the summary that came from a booking system is marked as such, so agents can tell system data from model text at a glance.
- **Close the loop in public.** When an agent's report leads to a fix, say so in the channel. People keep reporting problems when they can see reports get acted on.
- **Measure use, not just accuracy.** Track how often agents open the full transcript after reading a summary. If that number stays high, the summary is not trusted yet, whatever the eval score says.

## Decision record: how to run the eval set

| Option | For | Against |
| --- | --- | --- |
| A. Spreadsheet plus a script that scores it | Fast to start, anyone on the team can add a case | Breaks down past a few hundred cases; easy to edit results by hand |
| B. Evals in the codebase, run in CI on every prompt or model change | Release gate is automatic; history lives in Git | Needs engineering time up front; non-engineers need a way to add cases |
| C. A third-party eval platform | Dashboards and labelling tools out of the box | Another vendor for conversation data; cost; lock-in |

I would pick **B**, with a simple form so the support lead can submit new cases without touching code. The release gate is the part that matters most, and it only holds if it runs automatically. Option A is a fine first two weeks while B is built. The playbook chapter on [evaluating AI features](https://github.com/bgildea/ai-native-delivery-playbook/blob/main/05-evals.md) covers how I set this up in code.

## What I would measure in the first 90 days

- Summary accuracy on the eval set, per release
- Handoff precision and recall on the eval set
- Share of handoffs where the agent opens the full transcript
- Repeat-question rate after handoff
- Cost per handed-off conversation
- Number of new eval cases added from real failures (a team that is looking finds them)

## What this shows

Owning an AI feature after launch: quality routines, decision rules agreed in advance, cost guardrails, and the adoption work that decides whether people downstream use the output at all.

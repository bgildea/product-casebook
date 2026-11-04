# Example PRD: human handoff in an AI chat assistant

> This is an illustrative PRD written for this casebook. It is not taken from any employer and contains no confidential information. It shows how I structure a spec for an AI feature, drawing on my time as Technical Product Owner on AI chat and messaging products.

## Summary

Let customers move from the AI assistant to a human agent at the right moment, with the conversation context carried across, so nobody has to repeat themselves.

## Problem

Customers using an AI travel assistant sometimes get stuck: the request is too complex, the bot misunderstands, or they simply want a person. Today the handoff is a dead end ("please call us"), or it drops the agent into the chat with no context. Both cost time and goodwill.

## Goals and non-goals

**Goals**
- Customers reach a human within the same chat when they need one
- Agents see a short summary and the key facts before they type their first message
- The assistant hands off on its own when it is clearly failing, not only when asked

**Non-goals**
- Replacing agent routing or workforce management
- Handing off on voice channels (separate project)

## Users

| User | Need |
| --- | --- |
| Traveller | Get the problem solved without starting over |
| Support agent | Understand the case in seconds |
| Support lead | See why handoffs happen so the assistant can improve |

## Requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| R1 | Customer can ask for a human at any point in natural language ("agent", "talk to a person") | Must |
| R2 | Assistant triggers handoff after repeated failed intents or detected frustration | Must |
| R3 | Agent receives an AI-generated summary: intent, booking reference, what was already tried | Must |
| R4 | Summary never includes payment card data or passport numbers | Must |
| R5 | Customer is told the expected wait time and can leave and be notified | Should |
| R6 | Every handoff is tagged with a reason for reporting | Should |
| R7 | Agent can rate summary accuracy with one click | Could |

## AI-specific risks and how we handle them

| Risk | Mitigation |
| --- | --- |
| Summary states something the customer never said | Summaries quote booking facts from systems of record, not from the model; agent sees the transcript one click away |
| Handoff triggers too often, flooding agents | Thresholds tuned in a staged rollout; handoff rate is a guardrail metric |
| Handoff triggers too rarely, trapping customers | "Talk to a person" always works, regardless of model confidence |
| Sensitive data leaks into the summary | Redaction runs before summarisation; covered by automated tests |

## Evaluation plan

- **Offline:** a labelled set of real-world-style conversations, scored for "should hand off" (precision and recall) and summary accuracy against a rubric
- **Online:** handoff rate, time to first agent reply, repeat-question rate after handoff, customer satisfaction on handed-off chats
- **Release gate:** no drop in summary accuracy on the eval set between model or prompt changes

## Success metrics

- Fewer customers repeating information after handoff
- Shorter time from handoff to resolution
- Handoff reasons that feed back into assistant improvements each sprint

## Rollout

1. Internal agents only, summaries shown but not relied on
2. 10% of chat traffic in one market, thresholds tuned weekly
3. All markets, with the eval set run on every model or prompt change

## Open questions

- Which systems of record does the summary read from on day one?
- Do agents want the summary in the chat or in their case panel?

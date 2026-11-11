# Revenue reporting a medical society could trust

**Role:** WordPress developer and technical lead for a national medical professional society (2023 to 2026)
**Stack:** WordPress, WooCommerce, Stripe, Mailchimp

## Context

The society runs memberships and an annual conference through its WordPress site, with payments in Stripe. The board wanted to know how much each product earned: membership tiers, conference tickets, workshops.

## Problem

Stripe showed total revenue but not revenue per product in a form the treasurer could use. Subscriptions and one-off payments were mixed together, and some members had duplicate active subscriptions, which made totals unreliable.

## What I did

1. **Clarified the actual question.** "Better reporting" was broken down into specific questions: revenue per product, conference ticket sales, and current paying members.
2. **Fixed the data at the source.** Product metadata on Stripe objects, so revenue can be reported per product instead of guessed from descriptions.
3. **Cleaned up duplicates.** Audited and resolved members with more than one active subscription.
4. **Built small, focused tools instead of a dashboard project.** A ticket totals plugin suite for conference tracking and a Mailchimp subscriber count, each answering one question.

## Decision record: buy a reporting tool or tag the data?

| Option | For | Against |
| --- | --- | --- |
| A. Third-party Stripe analytics tool | Fast to switch on | Another subscription; still wrong if the source data is ambiguous |
| B. Custom dashboard | Exactly what they asked for | Weeks of work and a maintenance burden for a small organisation |
| C. Product metadata on every Stripe object, plus small targeted reports | Fixes the root cause; any future tool will work too | Needed a checkout change and a one-off backfill |

**Decision:** C. The problem was data quality, not visualisation.

## Outcome

Revenue can be reported per product straight from Stripe, conference ticket totals are tracked in one place, and the duplicate subscriptions are resolved.

## Skills this shows

Turning a vague request into answerable questions, payments data hygiene, choosing the smallest fix that solves the real problem, working with non-technical stakeholders.

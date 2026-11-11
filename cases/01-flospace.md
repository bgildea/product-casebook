# FloSpace: marketplace or LINE-native infrastructure?

**Role:** Co-founder, product and engineering lead
**Where:** Bangkok
**Stack:** Next.js, Postgres, Omise (Thai payments), Ably (realtime), LINE Messaging API

## Context

FloSpace started as a booking marketplace for independent fitness instructors in Bangkok: yoga, pilates, personal training. Instructors needed a way to list classes, take payment and manage bookings without paying studio commissions. Clients wanted to find and book a class in a couple of taps.

## Problem

Thailand runs on LINE. Instructors were already taking bookings through LINE chats and bank transfer screenshots. A standalone marketplace asked both sides to change habits at once: clients had to install or bookmark something new, and instructors had to move their regulars off a channel that already worked.

## What I did

- Built the core product: instructor profiles, class schedules, booking flow, Omise card and PromptPay payments, and realtime availability with Ably
- Integrated LINE so booking confirmations and reminders arrived where people already were
- Interviewed instructors about how they actually ran their week, which surfaced the real competitor: a LINE group plus a spreadsheet
- After a meeting with an investor connected to LINE's start-up programme, evaluated pivoting from a consumer marketplace to booking infrastructure delivered inside LINE (LIFF mini apps)

## Decision record: marketplace vs LINE-native booking infrastructure

| Option | For | Against |
| --- | --- | --- |
| A. Keep building the marketplace | Owns the customer relationship; brand and SEO compound over time | Needs demand on both sides at once; expensive client acquisition in one city |
| B. Pivot to LIFF booking tools sold to instructors and studios | Meets users inside LINE; instructors bring their own clients, so no cold-start on demand | Smaller ticket per customer; dependent on LINE platform rules |
| C. Hybrid: LIFF tools first, marketplace as a later layer | Gets usage now, keeps the marketplace option | Two products to maintain with a tiny team |

The strongest argument for B: distribution already existed in LINE, so the product's job could be to make that channel less manual rather than to replace it.

**Outcome:** I paused FloSpace before committing to either direction. The evaluation was still worth doing. It showed the marketplace's real problem was distribution, not missing features, and more features on option A would not have fixed that.

## Lesson

Products that plug into a channel people already use beat products that need to build a new one. That has shaped how I assess every product bet since.

## Skills this shows

Discovery interviews, platform strategy, payments in a local market, realtime UX, making a pivot decision with explicit options.

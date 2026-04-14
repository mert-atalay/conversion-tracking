# Conversion Tracking Review Pack

This repository is a public, docs-only handoff pack for reviewing the current CEFA conversion-tracking situation during the website transition.

It is designed for:

- GPT Pro review
- architecture challenge
- replacement planning
- handoff across collaborators

## What This Repo Includes

- sanitized current-state notes
- live parent inquiry field inventory
- plugin runtime findings based on verified inspection
- the original target architecture that first framed the hardening work
- the revised phase-1 architecture that reduced launch risk after deeper review
- final redesign page-map summary
- a GPT review brief with pushbacks and review questions
- a final copy-paste GPT Pro prompt with direct file links

## What This Repo Does Not Include

- proprietary Gravity Forms plugin source
- raw WordPress plugin zips
- private credentials
- environment-specific exports
- unredacted integration artifacts

## Recommended Reading Order

1. [`docs/review/gpt-pro-review-brief.md`](./docs/review/gpt-pro-review-brief.md)
2. [`docs/current-state/parent-inquiry-runtime.md`](./docs/current-state/parent-inquiry-runtime.md)
3. [`docs/current-state/live-parent-inquiry-inventory.md`](./docs/current-state/live-parent-inquiry-inventory.md)
4. [`docs/evidence/plugin-hook-map.md`](./docs/evidence/plugin-hook-map.md)
5. [`docs/planning/original-target-architecture.md`](./docs/planning/original-target-architecture.md)
6. [`docs/planning/revised-phase-1-architecture.md`](./docs/planning/revised-phase-1-architecture.md)
7. [`docs/planning/final-page-map.md`](./docs/planning/final-page-map.md)
8. [`docs/review/gpt-pro-final-prompt.md`](./docs/review/gpt-pro-final-prompt.md)

## Fast Summary

The most important current-state finding is that the parent inquiry flow is still a legacy runtime centered on:

- page slug `inquire-form`
- Gravity Form `4`
- a custom `cefa-school-journey-code-manager` plugin

That custom plugin is not just UI glue. It currently:

- resolves school, program, and days-offered behavior
- backfills hidden attribution fields at submit time
- posts the final inquiry directly to KinderTales after submission

Any redesign or Gutenberg migration should treat that as a real runtime contract that must be ported, replaced, or staged out carefully.

## Why The Plan Changed

The first architecture direction was useful, but it was too ambitious for a launch-phase implementation once the live parent runtime was verified more deeply.

The recommendation changed for five concrete reasons:

- the current parent inquiry flow is more tightly coupled than a simple form rebuild
- full sGTM in phase 1 adds infrastructure and migration risk before parity is proven
- GTM-only capture is a weak base if the goal is ad-blocker recovery
- some suggested implementation details were technically wrong or too optimistic for launch, especially around `localStorage`, PHP render-time access, and BigQuery-based uniqueness
- Meta CAPI is a practical server-side phase-1 win, while broader server-side Google Ads work should not block launch

The result is not a reversal.

It is a resequencing:

- original architecture becomes the future-state north star
- revised phase-1 architecture becomes the launch recommendation
- sGTM moves to a later phase after browser and collector parity is proven

## Suggested GPT Usage

Use GPT Pro to review this repository as:

- a verified current-state evidence pack
- an original target-state plan that still matters
- a revised phase-1 plan that is intended to ship first

Do not use this repo as proof that the new implementation already exists.

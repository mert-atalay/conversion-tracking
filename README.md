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
- final redesign page-map summary
- a GPT review brief with pushbacks and review questions

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
5. [`docs/planning/final-page-map.md`](./docs/planning/final-page-map.md)

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

## Suggested GPT Usage

Use GPT Pro to review this repository as a target-state planning and replacement-analysis pack, not as proof that the new implementation already exists.

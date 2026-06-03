# CEFA Conversion Tracking Source Pack

Prepared: 2026-06-03  
Purpose: source-ready Markdown context for future ChatGPT tasks related to CEFA conversion tracking, naming, UTMs, school taxonomy, and paid-media reconciliation.

## How To Use This Pack

Add this `docs/source/` folder as the main ChatGPT source context when asking for CEFA tracking, reporting, naming, UTM, or paid-media QA work.

Recommended reading order:

1. `docs/source/conversion-tracking-rules-spec.md`
2. `docs/source/naming-utm-school-standards.md`
3. `docs/source/school-taxonomy-may-2026.md`
4. `docs/source/may-2026-paid-media-reference.md`
5. Existing repo files under `docs/current-state/`, `docs/evidence/`, `docs/planning/`, and `docs/review/` for the detailed historical evidence pack.

## Source Truth Hierarchy

Use this order when sources conflict:

1. Verified current-state repo evidence: live parent inquiry runtime, live field inventory, and plugin hook map.
2. May 2026 audit artifacts: paid-media, GA4, and Form 4 business-lead reconciliation.
3. This source pack: normalized rules and recommendations derived from the evidence.
4. Platform-reported conversion counts: useful for delivery diagnostics, but not final business CPL.

## Current Non-Negotiables

- The live parent inquiry flow is a legacy Gravity Forms plus custom-plugin runtime, not a simple embedded form.
- The current parent route pattern is `/inquire-form/?location=<school_uuid>&title=<school_slug>`.
- The current form is Gravity Form `4` and the current school-entry model uses one shared backend form across schools.
- The custom `cefa-school-journey-code-manager` plugin currently controls school/program/day behavior, hidden attribution writeback, and direct KinderTales delivery.
- Phase 1 should preserve the existing KinderTales business path while adding first-party attribution capture, hidden-field population, shared `event_id`, a webhook collector, audit storage, and Meta CAPI backup.
- Full sGTM and broader server-side routing should remain phase 2 unless implementation evidence proves they are needed sooner.
- May 2026 business CPL should use deduped, non-test paid Form 4 target leads, not raw platform lead counts.

## Files Created In This Source Pack

| File | Use it for |
|---|---|
| `conversion-tracking-rules-spec.md` | Conversion rules, event specs, destination responsibilities, field contracts, phase split, and validation checklist. |
| `naming-utm-school-standards.md` | Naming convention, UTM taxonomy, campaign/ad naming standards, school slug rules, and canonical value lists. |
| `school-taxonomy-may-2026.md` | Canonical active school list, campaign IDs, school slugs, observed paid target slugs, alias warnings, and UUID guidance. |
| `may-2026-paid-media-reference.md` | May 2026 paid-media audit summary, reconciliation rules, school action matrix, and optimization guardrails. |

## Important Caveats

- This repo does not prove the new implementation exists. It is a verified current-state and planning source pack.
- Do not infer missing school UUIDs from campaign names or slugs. Use verified school identity sources only.
- Do not treat the redesign page map as the canonical school identity crosswalk.
- Do not merge parent enrollment, open house, summer camp, weekend care, franchise inquiry, and franchise site leads into one undifferentiated conversion bucket.

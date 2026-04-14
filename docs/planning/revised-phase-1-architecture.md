# Revised Phase-1 Architecture

## Final Call

Phase 1 should be a browser-primary plus webhook-collector implementation.

Full sGTM should move to phase 2.

## Why We Changed

The plan changed because the launch path needs to be simpler and safer without giving up the main hardening benefits.

The evidence-driven reasons are:

- the current parent inquiry flow is still a legacy runtime, not a clean-slate form rebuild
- KinderTales delivery is business-critical and should not be disrupted during the first hardening pass
- ad-blocker recovery requires a first-party capture layer, not GTM alone
- the team can get most of the early value from a collector and reconciliation layer without taking on full sGTM complexity immediately

## Recommended Phase-1 Stack

### 1. Keep the current business-critical path intact

- preserve the existing KinderTales delivery path during phase 1
- avoid merging new measurement logic into the legacy school-journey plugin
- treat the legacy plugin as a dependency to isolate around, not a place to refactor first

### 2. Add a lightweight measurement layer

Create a new measurement-focused plugin or equivalent site-owned layer that does only the tracking-specific work needed for the new stack.

Its responsibilities should be:

- create or guarantee `event_id`
- populate hidden tracking fields
- expose school and landing context for browser tags and webhooks
- avoid breaking existing form submission behavior

### 3. Use first-party attribution capture outside GTM

Use a small first-party script to capture UTMs, click IDs, landing page, and landing school context.

Storage recommendation:

- `localStorage` as the primary store
- first-party cookie fallback
- explicit TTL and overwrite rules

Do not depend on GTM alone for capture if recovery from blocked client-side tags is part of the goal.

### 4. Populate hidden fields client-side with server fallback

The field-population model should be:

- read stored attribution in the browser
- write it into Gravity Forms hidden fields before submission
- generate `event_id` in the browser when possible
- generate a server fallback if the field is missing

Do not assume PHP can read `localStorage` during form render.

### 5. Keep browser-side GA4 and browser-side Google Ads in phase 1

Browser tags should still fire for:

- GA4 primary conversion event
- Google Ads conversion path
- Meta Pixel browser event

Each should use the shared `event_id` for reconciliation and deduplication.

### 6. Add a Gravity Forms webhook to a collector

Gravity Forms should post the submission payload, including hidden fields, to a collector endpoint.

The collector should:

- accept the webhook without blocking the form submit
- validate basic payload integrity
- write durable audit records
- dedupe by `event_id`
- fire Meta CAPI as the main server-side recovery channel

### 7. Use BigQuery for audit and reconciliation, not request-time uniqueness

BigQuery should hold:

- raw webhook payloads
- normalized event records
- validation outcomes
- reconciliation outputs

Use a more appropriate dedupe pattern than BigQuery request-time lookup if strict idempotency is required.

### 8. Defer sGTM and broader server-side routing

Move these to phase 2 unless implementation evidence proves they are needed earlier:

- full sGTM deployment
- server-side Google Ads uploads or enhanced-conversion expansion
- more advanced routing and enrichment logic
- wider cross-property server-side standardization

## Suggested Phase Split

### Phase 1: launch-safe hardening

- first-party capture
- hidden-field population
- `event_id`
- browser GA4
- browser Google Ads
- browser Meta Pixel
- Gravity Forms webhook
- collector audit trail
- Meta CAPI backup
- BigQuery reconciliation

### Phase 2: server-side expansion

- sGTM
- broader server-side routing
- stricter event governance
- advanced platform integrations where justified

## What GPT Pro Should Challenge

GPT Pro should pressure-test:

- whether this phase split is the right one
- whether the first-party capture layer is scoped correctly
- whether the collector should stay Meta-first in phase 1
- whether any school-selection logic must be copied sooner into a new integration layer
- whether any browser dependency still creates unacceptable risk

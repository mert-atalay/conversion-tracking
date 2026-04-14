# Original Target Architecture

## Purpose

This file preserves the earlier architecture direction that shaped the CEFA transition work before the latest risk correction.

It should now be read as:

- the original target direction
- the future-state north star
- not the recommended launch-phase implementation

## What Still Holds

These ideas still look sound and should remain part of the long-term design:

- use a durable `event_id` across browser, webhook, collector, and reporting layers
- treat collector plus durable persistence as the business-truth boundary
- preserve school identity explicitly, especially `school_uuid`
- separate measurement logic from business-critical KinderTales delivery
- reconcile browser events, collector events, and downstream leads in BigQuery
- move toward stronger server-side resilience and better attribution auditability

## What This Version Implicitly Optimized For

The original direction implicitly optimized for:

- maximum data hardening early
- faster recovery from browser loss
- cleaner future attribution analysis
- eventual server-side routing maturity

That made it a strong strategy document, but a riskier launch plan.

## Why It Is No Longer The Phase-1 Recommendation

After verifying the live parent inquiry runtime and pressure-testing the implementation path, several issues became clear:

- the live flow is still tightly coupled to page slug `inquire-form`, Gravity Form `4`, and the custom school-journey plugin
- full sGTM introduces infrastructure, domain, client, and migration overhead before the team has parity on the existing flow
- relying on GTM to capture attribution undermines the goal of recovering signal when GTM or tags are blocked
- some suggested implementation details were too optimistic for phase 1

Examples:

- PHP cannot read `localStorage` during `gform_pre_render`
- BigQuery should not be used as a per-request primary-key validator
- server-side Google Ads uploads are more complex than Meta CAPI and should not become a launch blocker

## Correct Interpretation Now

Keep this architecture as the future-state target, especially for phase 2 and later hardening.

Use it to guide:

- eventual sGTM adoption
- broader server-side event routing
- stricter validation and enrichment
- more advanced attribution governance

Do not use it as the exact launch blueprint for the first implementation pass.

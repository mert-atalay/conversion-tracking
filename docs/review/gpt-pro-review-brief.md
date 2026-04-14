# GPT Pro Review Brief

## What You Are Reviewing

You are reviewing the CEFA conversion-tracking transition with special attention to:

- the verified parent inquiry runtime
- the original target architecture
- the revised phase-1 launch architecture
- the reasons the recommendation changed

Read these files in this order:

1. `README.md`
2. `docs/current-state/parent-inquiry-runtime.md`
3. `docs/current-state/live-parent-inquiry-inventory.md`
4. `docs/evidence/plugin-hook-map.md`
5. `docs/planning/original-target-architecture.md`
6. `docs/planning/revised-phase-1-architecture.md`
7. `docs/planning/final-page-map.md`

## Final Review Stance

Treat the current-state evidence as the truth layer.

Treat the original target architecture as the future-state north star.

Treat the revised phase-1 architecture as the current launch recommendation.

## What Is Verified

- the parent inquiry flow still depends on Gravity Form `4`
- the route still depends on `location=<school_uuid>` and `title=<school_slug>`
- the current page still loads a custom school-journey plugin
- the current custom plugin handles school/program/day behavior
- the current custom plugin fills hidden attribution fields at submit time
- the current custom plugin posts the final inquiry directly to KinderTales after submission

## Why The Recommendation Changed

The recommendation shifted because the earlier direction was too complex for phase 1 once the live runtime and implementation constraints were reviewed more carefully.

The main reasons are:

- the current runtime is more coupled than a clean-slate form migration
- full sGTM adds unnecessary launch risk before parity exists
- GTM-only attribution capture is weak if the goal is recovery from blocked client-side tags
- some proposed implementation mechanics were not technically sound for a phase-1 build

## Pushbacks

You should push back on any plan that assumes:

- Gutenberg alone replaces the current runtime
- a new form ID can be introduced without code changes
- the current logic lives only in Gravity Forms config
- the current KinderTales delivery path is just a generic webhook feed
- the custom plugin is portable as-is without its existing database state

You should also push back on any phase-1 plan that assumes:

- GTM alone should own attribution capture
- PHP can read `localStorage` during Gravity Forms render
- BigQuery should be queried at request time to enforce uniqueness
- server-side Google Ads work is required before launch

## Questions To Answer

1. What is the safest replacement strategy for the current legacy runtime:
   - full port
   - adapter
   - staged dual-run
   - controlled retirement
2. Which responsibilities belong in:
   - a new measurement plugin
   - a form integration layer
   - GTM
   - server-side collector logic
3. What must be preserved exactly in the new implementation:
   - school UUID context
   - selected school state
   - program selection
   - days-offered behavior
   - hidden attribution writeback
   - KinderTales delivery
4. What staging tests are mandatory before production cutover?
5. What should be treated as launch blockers versus fast-follow items?
6. Is the revised phase-1 plan the right launch plan, or should any part of the original target architecture move back into phase 1?
7. What should remain explicitly deferred to phase 2, especially around sGTM and broader server-side routing?

## Expected Output

Return:

- a corrected architecture recommendation
- an explanation of whether the shift from the original plan to the revised phase-1 plan is justified
- explicit pushbacks on risky assumptions
- a cutover strategy
- a staging validation checklist
- a view on whether the legacy plugin should be ported, wrapped, or replaced
- a clear separation between launch-now work and future-state work

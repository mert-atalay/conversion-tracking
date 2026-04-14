# GPT Pro Review Brief

## What You Are Reviewing

You are reviewing the current CEFA conversion-tracking transition with special attention to the parent inquiry runtime and the redesign replacement risk.

Read these files in this order:

1. `README.md`
2. `docs/current-state/parent-inquiry-runtime.md`
3. `docs/current-state/live-parent-inquiry-inventory.md`
4. `docs/evidence/plugin-hook-map.md`
5. `docs/planning/final-page-map.md`

## Final Review Stance

Treat the current architecture pack as strong target-state direction.

Do not treat it as already-proven implementation truth.

## What Is Verified

- the parent inquiry flow still depends on Gravity Form `4`
- the route still depends on `location=<school_uuid>` and `title=<school_slug>`
- the current page still loads a custom school-journey plugin
- the current custom plugin handles school/program/day behavior
- the current custom plugin fills hidden attribution fields at submit time
- the current custom plugin posts the final inquiry directly to KinderTales after submission

## Pushbacks

You should push back on any plan that assumes:

- Gutenberg alone replaces the current runtime
- a new form ID can be introduced without code changes
- the current logic lives only in Gravity Forms config
- the current KinderTales delivery path is just a generic webhook feed
- the custom plugin is portable as-is without its existing database state

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

## Expected Output

Return:

- a corrected architecture recommendation
- explicit pushbacks on risky assumptions
- a cutover strategy
- a staging validation checklist
- a view on whether the legacy plugin should be ported, wrapped, or replaced

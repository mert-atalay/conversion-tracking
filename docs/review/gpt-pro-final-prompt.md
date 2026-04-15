# GPT Pro Final Prompt

Copy and paste the prompt below into GPT Pro.

```text
You are reviewing the CEFA website-transition conversion-tracking architecture.

Important: do not treat this repo as proof that the new build already exists. Treat it as a verified current-state evidence pack plus two planning layers:

1. the original target architecture that first framed the hardening work
2. the revised phase-1 architecture that we now believe is safer to ship first

Read these files in this exact order:

1. https://github.com/mert-atalay/conversion-tracking/blob/main/README.md
2. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/current-state/parent-inquiry-runtime.md
3. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/current-state/live-parent-inquiry-inventory.md
4. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/evidence/plugin-hook-map.md
5. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/planning/original-target-architecture.md
6. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/planning/revised-phase-1-architecture.md
7. https://github.com/mert-atalay/conversion-tracking/blob/main/docs/planning/final-page-map.md

Context you must hold while reviewing:

- The live parent inquiry flow is still a legacy runtime centered on `/inquire-form/`, Gravity Form `4`, and a custom `cefa-school-journey-code-manager` plugin.
- The current parent pattern is one shared backend Gravity Form reused across schools. Different school pages resolve into the same form runtime using URL parameters such as `location=<school_uuid>` and `title=<school_slug>`.
- That plugin is not just UI glue. It currently handles school/program/day behavior, hidden attribution-field writeback, and direct KinderTales posting after submission.
- We originally leaned toward a more ambitious hardening direction. After reviewing the live runtime and the implementation risk, we shifted the recommendation.
- We are not abandoning the original direction. We are resequencing it:
  - original target architecture = future-state north star
  - revised phase-1 architecture = launch recommendation
  - sGTM = likely phase 2, not phase 1

The main reasons for the shift are:

- full sGTM in phase 1 may add too much infrastructure and migration complexity before parity is proven
- GTM-only attribution capture is a weak base if recovery from blocked client-side tags is a goal
- some proposed implementation details appear wrong or too optimistic for phase 1, especially around PHP render-time access to `localStorage`, BigQuery-based uniqueness checks, and server-side Google Ads scope
- the safest first move appears to be a browser-primary plus webhook-collector model that preserves KinderTales continuity while adding auditability and recovery

Important implementation nuance:

- do not reason about the current parent site as if each school has its own separate Gravity Form
- reason about it as one shared Gravity Form runtime with school-bound entry through URL parameters and plugin logic

Please answer in five sections:

1. Final judgment
Tell us whether the revised phase-1 plan is the right launch plan, or whether any part of the original target architecture should move back into phase 1.

2. Pushbacks
List the main assumptions you would push back on, especially if either plan still understates the legacy-runtime coupling, attribution-capture risk, webhook risk, or collector complexity.

3. Recommended architecture
Give a corrected architecture recommendation that clearly separates:
- launch-now work
- launch blockers
- fast-follow work
- future-state phase-2 work

4. Replacement and cutover strategy
Explain the safest way to handle the current legacy runtime:
- port
- wrap
- adapter
- staged dual-run
- controlled retirement

Be explicit about what must be preserved exactly:
- school UUID context
- landing school context
- selected school state
- program selection
- days-offered behavior
- hidden attribution writeback
- event_id continuity
- KinderTales delivery

5. Staging and validation checklist
Give the exact staging tests required before any production cutover. Include browser-side, webhook-side, collector-side, ad-blocker, duplicate-submit, missing-location, and landing-vs-selected-school mismatch scenarios.

Additional instructions:

- Call out anything in the revised phase-1 plan that is still too complex for a first release.
- Call out anything in the original target architecture that is too valuable to defer.
- If you think the phase split should be adjusted, say exactly how.
- If you think sGTM should still stay out of phase 1, defend that clearly.
- If you think it should come back into phase 1, explain exactly why the added complexity is justified.
- Refer directly to the GitHub file URLs above in your reasoning so the review can be audited later.
```

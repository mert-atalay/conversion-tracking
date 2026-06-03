# CEFA Conversion Tracking Rules Spec

Prepared: 2026-06-03  
Scope: CEFA parent inquiry, franchise inquiry/site conversion surfaces, first-party attribution capture, event naming, hidden-field rules, webhook/collector rules, and validation.

## 1. Current Runtime Contract

Treat the live parent inquiry flow as a real runtime contract, not a simple embedded form.

| Contract area | Current value / rule |
|---|---|
| Parent inquiry route | `/inquire-form/?location=<school_uuid>&title=<school_slug>` |
| Form system | Gravity Forms |
| Form ID | `4` |
| Front-end shell | Elementor-wrapped page shell |
| School-entry model | One shared backend Gravity Form reused across schools |
| School locking | URL-driven, especially `location=<school_uuid>` |
| Custom plugin | `cefa-school-journey-code-manager` |
| Business delivery | Direct post-submission delivery to KinderTales by the custom plugin |

### Responsibilities that must not be broken

Any replacement, adapter, or cutover must preserve or intentionally replace these current plugin responsibilities:

- load front-end behavior only on page slug `inquire-form`
- bind server-side logic specifically to Gravity Form `4`
- read `location` from the query string and write selected school UUIDs into hidden school fields
- populate program options based on selected school
- filter days-offered options based on selected school
- clean the title slug before submission
- backfill hidden attribution fields from first-party cookies at submit time
- post the final inquiry to KinderTales after successful submission

## 2. Phase-1 Architecture Rule

Phase 1 should be browser-primary plus webhook-collector, not full sGTM.

| Layer | Phase-1 responsibility |
|---|---|
| Existing legacy form/plugin | Preserve school selection, program/day logic, submit behavior, and KinderTales delivery. Do not refactor this first. |
| New measurement layer/plugin | Guarantee `event_id`; expose school and landing context; populate hidden tracking fields; provide server fallback for missing IDs. |
| First-party attribution script | Capture UTMs, click IDs, landing URL, referrer, landing school context, timestamps, and TTL/overwrite state outside GTM. |
| Browser tags | Fire GA4 `generate_lead`, Google Ads conversion, and Meta Pixel event with shared `event_id`. |
| Gravity Forms webhook | Send submitted payload plus hidden fields to the collector without blocking the parent form submission. |
| Collector | Validate, normalize, dedupe by `event_id`, persist audit records, and trigger Meta CAPI as the main phase-1 server-side recovery channel. |
| Warehouse / BigQuery | Store raw webhook payloads, normalized events, validation outcomes, and reconciliation outputs. Do not use BigQuery as a request-time uniqueness validator. |

### Phase-2 / deferred

- full server-side GTM deployment
- broader server-side Google Ads uploads
- advanced enhanced-conversion expansion
- advanced enrichment and routing across multiple CEFA properties
- stricter multi-platform event governance after phase-1 parity is proven

## 3. Conversion Source-Of-Truth Rules

| Use case | Primary source | Notes |
|---|---|---|
| Business CPL and budget decisions | Deduped, non-test paid Form 4 target leads | This is the defensible business layer for May 2026. |
| Delivery diagnostics | Meta Ads and Google Ads platform conversions | Useful, but not final business truth. |
| Web analytics trend layer | GA4 `generate_lead` | Better than broad `form_submit`; still lower than Form 4 in May paid evidence. |
| CRM quality / lifecycle | KinderTales / GreenRope / CRM | Blocked for May 2026 CPL until complete access and identity reconciliation are restored. |
| Audit and reconciliation | Collector plus warehouse | Should persist raw and normalized payloads. |

## 4. Event Model

### Core parent inquiry events

| Event | Where it fires | Required status | Purpose |
|---|---|---|---|
| `parent_inquiry_form_view` | Browser | Recommended | Identify landing school context and form availability. |
| `parent_inquiry_start` | Browser | Recommended | Optional micro-conversion when the visitor starts the form. |
| `generate_lead` | GA4 browser tag | Required | Primary GA4 conversion event. |
| `parent_inquiry_submit_attempt` | Browser or measurement layer | Optional | Debug event before final submission; should not be used as the lead conversion. |
| `parent_inquiry_submitted` | Collector / warehouse | Required | Server-side normalized lead event after Form 4 webhook is received. |
| `parent_inquiry_success` | Browser thank-you or post-submit confirmation | Recommended | Used for browser reconciliation against webhook receipt. |
| `meta_capi_lead` | Collector to Meta CAPI | Required in phase 1 | Server-side recovery and dedupe partner for browser Meta Pixel. |

### Franchise conversion surfaces

| Surface | Event recommendation | Notes |
|---|---|---|
| Franchise Canada submit inquiry | `franchise_inquiry_submitted` | Separate from parent enrollment leads. |
| Franchise Canada market unavailable | `franchise_market_unavailable` | Do not mix with successful franchise inquiries. |
| Franchise Canada submit a site | `franchise_site_submitted` | Separate conversion action. |
| Franchise USA submit inquiry | `franchise_inquiry_submitted` with `country=us` | Separate property/country parameter required. |
| Franchise USA submit a site | `franchise_site_submitted` with `country=us` | Separate conversion action. |

## 5. Required Event Parameters

Every successful parent lead event should carry these parameters where technically possible.

| Parameter | Required? | Example / rule | Notes |
|---|---|---|---|
| `event_id` | Yes | UUID v4 or strong random ID | Shared across browser, webhook, collector, Meta CAPI, GA4, and warehouse. |
| `event_name` | Yes | `generate_lead`, `parent_inquiry_submitted` | Destination-specific names can differ but must map back to a normalized internal name. |
| `form_id` | Yes | `4` | Required during legacy runtime. |
| `form_name` | Recommended | `parent_inquiry` | Stable internal name. |
| `school_uuid` | Yes when available | Verified UUID from `location` | Do not infer UUIDs from slugs. |
| `landing_school_slug` | Yes | `markham-esna-park` | From landing page or query/title context. |
| `selected_school_slug` | Yes | `markham-esna-park` | From hidden school field or submitted selection. |
| `campaign_target_school_slug` | Required for paid reporting | `markham-esna-park` | Derived from paid campaign or UTM mapping. |
| `school_context_match` | Recommended | `true` / `false` | False when landing, selected, and campaign target disagree. |
| `program_selected` | Recommended | Program value | Must preserve current program population logic. |
| `days_offered_selected` | Recommended | Days/week values | Must preserve current days-offered filtering. |
| `lead_type` | Yes | `parent_enrollment`, `open_house`, `summer_camp`, `weekend_care`, `franchise_inquiry`, `franchise_site` | Required to avoid mixed CPL. |
| `utm_source` | Required for paid links | `google`, `meta`, `facebook`, `instagram` | Lowercase only. |
| `utm_medium` | Required for paid links | `cpc`, `paid_social` | Lowercase only. |
| `utm_campaign` | Required for paid links | See naming doc | Must include enough to map to school and lead type. |
| `utm_content` | Recommended | creative/ad identifier | Use stable creative/ad variant context. |
| `utm_term` | Google Search recommended | keyword/search theme | Do not use for Meta unless needed. |
| `gclid` | Capture when present | Google click ID | Paid evidence priority. |
| `gbraid` / `wbraid` | Capture when present | Google iOS/web click IDs | Paid evidence priority. |
| `fbclid` | Capture when present | Meta click ID | Paid evidence priority. |
| `landing_page_url` | Yes | Full first landing URL | Store before redirects where possible. |
| `conversion_page_url` | Yes | Form or thank-you URL | Useful for QA. |
| `referrer` | Recommended | Document referrer | Store when available. |
| `submitted_at` | Yes | ISO timestamp | Store site timezone and UTC where possible. |

## 6. Legacy Form Field Contract

Known Form 4 fields from the live inventory:

| Field | Meaning |
|---|---|
| `input_26` | Guardian first name |
| `input_27` | Guardian last name |
| `input_3` | Relationship |
| `input_23` | Relationship other; conditional when relationship is `Other` |
| `input_6` | Email |
| `input_7` | Phone |
| `input_28` | Child first name |
| `input_29` | Child last name |
| `input_52.*` | Site address |
| `input_10` | Gender |
| `input_9` | Date of birth |
| `input_11` | Requested start date |
| `input_22` | Program dropdown |
| `input_50.*` | Days per week |
| `input_13.*` | Postal code |
| `input_18` | Source |
| `input_19` | Source other; conditional when source is `Other` |
| `input_20` | Comments |
| `input_24.*` | Consent |
| Field `30` | Location UUID |
| Field `31` | Title slug |
| Field `32[]` | Hidden school multiselect used by the custom plugin |
| Fields `33-39`, `45-49` | Hidden attribution and landing-context fields |

Rules:

- Do not rename, remove, or repurpose hidden fields until the legacy plugin and webhook mapping are ported or replaced.
- The new measurement layer may add fields, but it must not break existing field IDs used by `cefa-school-journey-code-manager`.
- Client-side hidden-field population should run before submit and after Gravity Forms re-render events.
- Server-side fallback should generate missing `event_id` and preserve the submitted attribution payload, but PHP must not be expected to read browser `localStorage` at render time.

## 7. Attribution Capture Rules

Use a first-party capture layer outside GTM.

Recommended storage pattern:

- `localStorage` primary
- first-party cookie fallback
- explicit TTL
- overwrite rules by parameter type

Paid evidence priority:

1. click IDs: `gclid`, `gbraid`, `wbraid`, `fbclid`
2. UTMs: source, medium, campaign, content, term
3. source/medium fallback
4. referrer / organic / direct fallback

Recommended TTL and overwrite rules:

| Data type | Recommended TTL | Overwrite rule |
|---|---:|---|
| Click IDs | 90 days | Overwrite when a newer click ID exists from the same platform; preserve original first-touch separately if implemented. |
| UTMs | 90 days | Overwrite with a new explicitly tagged campaign. |
| Landing school context | 90 days | Do not overwrite selected school on form submit; track landing and selected separately. |
| Referrer | 30 days | Only use when no click ID or UTM exists. |
| Direct/unknown | Session only | Never overwrite known paid evidence with direct/unknown. |

## 8. Destination Rules

| Destination | Phase-1 rule |
|---|---|
| GA4 | Use browser `generate_lead` as the primary GA4 lead signal. Include shared `event_id` and school/lead-type parameters. |
| Google Ads | Keep browser-side conversion in phase 1. Do not make server-side Google Ads uploads a launch blocker. |
| Meta Pixel | Fire browser lead event with shared `event_id`. |
| Meta CAPI | Fire from collector with the same `event_id` as browser Meta event for dedupe. |
| KinderTales | Preserve existing direct post-submission delivery until replacement is fully validated. Measurement work must not interrupt this. |
| Warehouse / BigQuery | Audit and reconciliation only; not request-time idempotency. |
| GTM | May orchestrate browser tags, but must not be the only attribution capture layer. |
| sGTM | Phase 2 unless a specific launch blocker proves it must be earlier. |

## 9. Deduplication And Reconciliation Rules

- `event_id` is the durable join key across browser, form webhook, collector, ad platforms, and warehouse.
- Collector should reject or mark duplicates by `event_id` without blocking the customer-facing form submission.
- Browser-only events without matching Form 4/webhook lead should be considered diagnostic until reconciled.
- Platform counts should be compared to GA4 and Form 4 but not used alone for business CPL.
- Cross-school inquiries must be preserved, not hidden. Track `landing_school_slug`, `selected_school_slug`, and `campaign_target_school_slug` separately.

May 2026 reconciliation facts:

| Check | Value |
|---|---:|
| Clean May Form 4 rows | 2,586 |
| Paid Form 4 rows | 610 |
| Paid rows with click-id evidence | 606 |
| Paid rows with UTM/source-medium evidence | 4 |
| Paid target missing | 52 |
| Paid selected school missing | 12 |
| Cross-school paid inquiries | 196 |

## 10. Cutover Strategy

Recommended cutover stance: wrap or adapter first, controlled retirement later.

1. Preserve the existing parent Form 4 and KinderTales path.
2. Add measurement-only logic outside the legacy school-journey plugin.
3. Populate hidden attribution fields without changing business form behavior.
4. Add webhook delivery to collector and verify it does not block submissions.
5. Dual-run browser events, webhook records, and platform conversions.
6. Reconcile at least one controlled submission per paid channel and a sample of real paid submissions.
7. Only then retire or replace legacy plugin responsibilities.

## 11. Launch Validation Checklist

### Browser and form checks

- Load `/inquire-form/?location=<valid_school_uuid>&title=<school_slug>` and confirm Gravity Form `4` renders.
- Confirm school lock, program dropdown, and days-offered filtering still work.
- Confirm missing `location` fails safely instead of causing JS failure.
- Confirm `event_id` exists before submit.
- Confirm UTMs and click IDs are written into hidden fields before submit.
- Confirm hidden fields still include location UUID, title slug, school multiselect, and attribution fields.

### Conversion checks

- GA4 receives `generate_lead` with `event_id`, school slug, lead type, and source/medium/campaign context.
- Google Ads receives browser-side conversion for paid Google test or recent real lead.
- Meta Pixel receives browser event with `event_id`.
- Meta CAPI receives server event with the same `event_id` and dedupes correctly against Pixel.
- The collector receives the Gravity Forms webhook and stores both raw and normalized records.

### Data quality checks

- Paid lead with `gclid` maps to Google paid.
- Paid lead with `fbclid` maps to Meta paid.
- UTM-only lead maps correctly when no click ID exists.
- Direct/unknown does not overwrite prior paid click evidence.
- Landing school and selected school mismatch is marked, not discarded.
- Open house, summer camp, weekend care, franchise inquiry, and franchise site submissions do not enter the parent enrollment CPL bucket.

### Failure-mode checks

- Duplicate submit uses same or duplicate-safe `event_id` logic.
- Webhook outage does not block customer submission or KinderTales delivery.
- Collector retry does not create duplicate paid leads.
- Ad blocker scenario still preserves first-party captured attribution in submitted Form 4/webhook data.
- Missing `location`, invalid UUID, and invalid school slug are logged and handled safely.

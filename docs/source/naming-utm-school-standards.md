# CEFA Naming, UTM, And School Standards

Prepared: 2026-06-03  
Scope: recommended standard values for campaign naming, UTMs, school slugs, lead types, conversion names, and reporting-safe segmentation.

## 1. Naming Principles

- Use lowercase for machine-readable values.
- Use hyphens for slugs and underscores for UTM/campaign tokens.
- Do not use spaces, title case, emojis, or punctuation in UTM values.
- Keep parent enrollment, open house, summer camp, weekend care, franchise inquiry, and franchise site campaigns separate.
- Every paid school campaign must be mappable to exactly one canonical school slug unless it is intentionally a corporate/non-school campaign.
- Do not use the redesign page map as a school identity crosswalk.
- Do not infer school UUIDs from campaign names, page names, or slugs.

## 2. Canonical School Slug Rule

Use the canonical school slug for:

- UTMs
- GA4 event parameters
- collector normalized records
- warehouse / BigQuery school dimension joins
- campaign and ad group naming
- reporting table joins

Format:

```text
<city-or-area>-<school-or-location-name>
```

Examples:

```text
calgary-beltline
markham-esna-park
north-vancouver-capilano-mall
surrey-panorama
```

Special warning: `South Surrey - Panorama` had a May 2026 naming mismatch. Use `surrey-panorama` as the canonical Form/audit slug until the canonical school identity source says otherwise, and track `south-surrey-panorama` as an alias requiring mapping.

## 3. UTM Taxonomy

### Required UTM parameters

| Parameter | Required? | Allowed / recommended values | Notes |
|---|---|---|---|
| `utm_source` | Yes for paid and tagged links | `google`, `meta`, `facebook`, `instagram`, `google_business_profile`, `email`, `partner`, `referral` | Prefer platform owner over placement when campaign is managed centrally. |
| `utm_medium` | Yes for paid and tagged links | `cpc`, `paid_search`, `paid_social`, `organic_social`, `local_listing`, `email`, `referral`, `display`, `video` | Use `cpc` for Google Search; `paid_social` for Meta. |
| `utm_campaign` | Yes | See campaign naming format below | Must include school or non-school scope and lead type. |
| `utm_content` | Recommended | Creative/ad/asset identifier | Use for creative ID, ad ID, angle, format, or placement. |
| `utm_term` | Google Search recommended | Keyword/theme | Do not overload this for school name; school belongs in campaign and event parameters. |

### Paid source/medium standards

| Platform / source | `utm_source` | `utm_medium` |
|---|---|---|
| Google Search | `google` | `cpc` |
| Google Performance Max | `google` | `cpc` or `paid_search` only if the reporting standard already uses it consistently; choose one and keep it fixed. |
| Meta managed campaigns | `meta` | `paid_social` |
| Facebook-specific paid link | `facebook` | `paid_social` |
| Instagram-specific paid link | `instagram` | `paid_social` |
| Google Business Profile | `google_business_profile` | `local_listing` |
| Email | `email` | `email` |
| Organic social | platform name | `organic_social` |

## 4. UTM Campaign Naming Format

Recommended default:

```text
cefa_<property>_<country>_<province-or-region>_<school_slug-or-scope>_<lead_type>_<objective>_<yyyymm>
```

Examples:

```text
cefa_parent_ca_ab_calgary-beltline_parent_enrollment_search_202606
cefa_parent_ca_on_markham-esna-park_open_house_traffic_202606
cefa_parent_ca_bc_surrey-panorama_summer_camp_conversion_202606
cefa_franchise_ca_on_corp_franchise_inquiry_leadgen_202606
cefa_franchise_us_us_corp_franchise_site_leadgen_202606
```

### UTM campaign token definitions

| Token | Allowed examples | Rule |
|---|---|---|
| `property` | `parent`, `franchise` | Identifies the website/business line. |
| `country` | `ca`, `us` | Use ISO-style lowercase two-letter country. |
| `province-or-region` | `bc`, `ab`, `on`, `corp`, `us` | Use province for parent school campaigns; use `corp` only for non-school corporate scope. |
| `school_slug-or-scope` | `calgary-beltline`, `corp`, `ontario-corp` | Use canonical slug for school campaigns. |
| `lead_type` | `parent_enrollment`, `open_house`, `summer_camp`, `weekend_care`, `franchise_inquiry`, `franchise_site` | Required to prevent mixed CPL. |
| `objective` | `search`, `conversion`, `traffic`, `leadgen`, `video`, `pmax` | Must reflect platform objective/channel. |
| `yyyymm` | `202606` | Campaign launch or active month. |

## 5. Campaign Naming Standards

### Meta campaign format

Recommended:

```text
CEFA | Parent | CA | <Province> | <School Name> | <Lead Type> | <Objective> | <YYYY-MM>
```

Example:

```text
CEFA | Parent | CA | ON | Markham - Esna Park | Parent Enrollment | Conversions | 2026-06
```

Rules:

- Avoid legacy ad hoc names such as `beltline | LSM | conversions (updated)` for new builds.
- Use a fresh campaign/ad naming structure for every replacement build.
- Keep Open House traffic campaigns separate from enrollment campaigns.
- Keep fresh creative IDs and do not reuse old post/story IDs when replacing Meta ads.
- Do not enable Advantage+ media/music/multi-text unless explicitly approved and QA'd against the creative-scramble risk.

### Meta ad set format

```text
<School Name> | <Audience/Geo> | <Age or Parent Segment> | <Placement or Auto> | <YYYY-MM>
```

Example:

```text
Markham - Esna Park | Local 10km | Parents | Advantage Placements | 2026-06
```

### Meta ad format

```text
<School Slug> | <Lead Type> | <Angle> | <Format> | <Creative ID or Date>
```

Example:

```text
markham-esna-park | parent_enrollment | early-years-school | video | 202606-a
```

## 6. Google Ads Naming Standards

### Google Search campaign format

```text
CEFA | Parent | CA | <Province> | <School Name> | Search | <Lead Type> | <YYYY-MM>
```

Example:

```text
CEFA | Parent | CA | BC | Surrey - Sunnyside | Search | Parent Enrollment | 2026-06
```

### Google ad group format

```text
<School Slug> | <Intent Theme> | <Match Type or Theme> | <YYYY-MM>
```

Examples:

```text
surrey-sunnyside | private-preschool | phrase-exact | 2026-06
calgary-northland | early-learning-school | phrase-exact | 2026-06
```

### RSA naming / labels

Use labels or naming metadata to capture:

- school slug
- intent theme
- RSA refresh date
- ad strength status
- final URL / landing slug

Poor ad strength alone is not an automatic pause rule. In May 2026, some Poor RSAs still converted, so treat Poor strength as a copy/relevance repair cue.

## 7. Final URL And Query Parameter Rules

Parent school inquiry URL pattern:

```text
https://cefa.ca/inquire-form/?location=<school_uuid>&title=<school_slug>&utm_source=<source>&utm_medium=<medium>&utm_campaign=<campaign>&utm_content=<content>&utm_term=<term>
```

Rules:

- `location` must be a verified school UUID.
- `title` should resolve to the canonical school slug. Legacy title casing may appear in live URLs, but reporting should normalize to lowercase slug.
- UTMs must not replace `location`; the plugin relies on `location` for school locking.
- UTMs must not be the only source of selected-school truth; preserve selected school separately.

## 8. Conversion Naming Standards

| Destination | Conversion/event name | Notes |
|---|---|---|
| GA4 | `generate_lead` | Primary GA4 lead event for parent inquiry. Add parameters for school and lead type. |
| Internal normalized event | `parent_inquiry_submitted` | Collector/warehouse canonical parent lead event. |
| Meta Pixel | `Lead` or platform-standard lead event | Must include shared `event_id`. |
| Meta CAPI | `Lead` | Must use same `event_id` as Pixel. |
| Google Ads | Existing/approved lead conversion action | Keep browser-side in phase 1; do not rename without migration plan. |
| Franchise inquiry | `franchise_inquiry_submitted` | Separate from parent enrollment. |
| Franchise site | `franchise_site_submitted` | Separate from franchise inquiry. |
| Market unavailable | `franchise_market_unavailable` | Do not count as a successful inquiry unless explicitly defined. |

## 9. Lead Type Values

Use these normalized values:

| Value | Meaning | Reporting bucket |
|---|---|---|
| `parent_enrollment` | Standard school inquiry / enrollment lead | Parent enrollment CPL |
| `open_house` | Open house traffic or inquiry | Separate event/bucket; do not mix with enrollment CPL |
| `summer_camp` | Summer camp campaign/submission | Separate event/bucket unless leadership explicitly merges it |
| `weekend_care` | Weekend care campaign/submission | Separate event/bucket |
| `franchise_inquiry` | Franchise prospect inquiry | Franchise CPL |
| `franchise_site` | Franchise submit-a-site | Franchise site lead CPL |
| `unknown` | Missing or unmapped | QA bucket, not budget-decision bucket |

## 10. Reporting Naming Rules

- `business_cpl` = school paid spend divided by deduped, non-test paid Form 4 target leads.
- `platform_cpl` = platform spend divided by platform-reported leads/conversions.
- `ga4_cpl` = platform spend divided by GA4 `generate_lead` count assigned to the school/campaign.
- `form_paid_leads` = paid Form 4 rows with paid evidence and school target mapping.
- `cross_school_inquiry` = selected school differs from paid campaign target, or row is flagged cross-school.
- `unresolved_target` = paid row exists but campaign target school cannot be assigned.

## 11. QA Rules For Names And UTMs

Before launch or bulk upload, check:

- campaign name includes property, country, province/region, school/scope, lead type, objective, and date
- `utm_campaign` includes school slug or approved non-school scope
- `utm_source` and `utm_medium` use allowed values
- final URL contains verified `location=<school_uuid>` for school inquiry campaigns
- `title=<school_slug>` maps to the canonical slug list
- Open House / Summer Camp / Weekend Care are separated from Parent Enrollment
- franchise and parent school campaigns are not merged
- `surrey-panorama` vs `south-surrey-panorama` alias is normalized before reporting

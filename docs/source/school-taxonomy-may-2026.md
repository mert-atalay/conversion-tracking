# CEFA School Taxonomy And May 2026 School Reference

Prepared: 2026-06-03  
Scope: canonical active paid-media school list, campaign IDs, school slugs, observed paid target slugs, school-alias warnings, and UUID handling rules.

## 1. Canonical Active School List For May 2026 Paid-Media Rollup

This table covers the 16 schools in the May 2026 parent paid-media school CPL audit.

| School | Canonical slug | Meta campaign ID | Google campaign ID | May budget | May spend | Form paid leads | Business CPL | Priority | June action |
| --- | --- | --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| Calgary - Beltline | calgary-beltline | 120230793807800400 | 23854771408 | $4,000.00 | $3,992.14 | 47 | $84.94 | P1 | Fix |
| Calgary - Cornerstone | calgary-cornerstone | 120230564571010400 | 23850247439 | $1,500.00 | $1,404.20 | 29 | $48.42 | P1 | Continue |
| Calgary - Northland | calgary-northland | 120248376493090400 | 23341832523 | $3,000.00 | $3,009.73 | 38 | $79.20 | P1 | Fix |
| Surrey - Campbell Heights | surrey-campbell-heights | 120248376490050400 | 23850199820 | $3,000.00 | $3,041.76 | 17 | $178.93 | P0 | Fix / watch |
| White Rock | white-rock | 120231838861630400 | 23850265670 | $3,000.00 | $2,990.05 | 20 | $149.50 | P1 | Fix / watch |
| Richmond South | richmond-south | 120248376490750400 | 22884384921 | $3,000.00 | $3,006.75 | 41 | $73.34 | P1 | Continue |
| Chilliwack - Cottonwood | chilliwack-cottonwood | 120248488192580400 | 23854771579 | $3,000.00 | $2,991.92 | 17 | $176.00 | P0 | Fix / limit |
| North Vancouver - Capilano Mall | north-vancouver-capilano-mall | 120248488193960400 | 23854771861 | $3,000.00 | $3,028.03 | 36 | $84.11 | P1 | Continue / validate |
| Burlington - South Service Road | burlington-south-service-road | 120248488191880400 | 17290399592 | $1,500.00 | $1,500.91 | 43 | $34.90 | P1 | Continue |
| Oakville - Eighth Line | oakville-eighth-line | 120248488191060400 | 23854771600 | $1,500.00 | $1,608.46 | 28 | $57.45 | P1 | Budget watch |
| Markham - Esna Park | markham-esna-park | 120229052675680400 | 23854769503 | $3,000.00 | $2,848.94 | 36 | $79.14 | P1 | Continue / fix RSA |
| Mississauga - Meadowvale | mississauga-meadowvale | 120230794740250400 | 23850265577 | $3,000.00 | $2,954.77 | 78 | $37.88 | P1 | Continue |
| Victoria - University Heights | victoria-university-heights | 120248376493980400 | 23844877563 | $3,000.00 | $3,039.15 | 32 | $94.97 | P1 | Fix / watch |
| South Surrey - Panorama | surrey-panorama | 120248376489040400 | 23854716415 | $3,000.00 | $3,023.96 | 20 | $151.20 | P1 | Continue / fix slug |
| Surrey - Sunnyside | surrey-sunnyside | 120248376488200400 | 23854771846 | $3,000.00 | $3,035.43 | 15 | $202.36 | P0 | Fix / limit |
| Kelowna - Spall | kelowna-spall | 120242283263490400 | 23844877386 | $3,000.00 | $2,988.95 | 12 | $249.08 | P0 | Fix / limit |

## 2. Active School Action Notes

| School | Slug | Priority | Action | Evidence note |
| --- | --- | --- | --- | --- |
| Calgary - Beltline | calgary-beltline | P1 | Fix | Legacy Meta naming, high Google CPA, and paid-form cross-school leakage need cleanup before aggressive June scaling. |
| Calgary - Cornerstone | calgary-cornerstone | P1 | Continue | Both platforms are comparatively efficient; keep weekend-care/enrollment UTMs separated and validate quality. |
| Calgary - Northland | calgary-northland | P1 | Fix | Meta is productive, but Google search-term waste around broad daycare intent needs campaign-level mining. |
| Surrey - Campbell Heights | surrey-campbell-heights | P0 | Fix / watch | High Meta spend, low attributed Form 4 target volume, weak Google CPA, and missing Google GA4 campaign-target lead rows. |
| White Rock | white-rock | P1 | Fix / watch | High total spend versus attributed paid form volume; clean geo leakage and query terms before raising June budgets. |
| Richmond South | richmond-south | P1 | Continue | Google is one of the strongest school Search campaigns; Meta has good platform volume but needs business-lead reconciliation. |
| Chilliwack - Cottonwood | chilliwack-cottonwood | P0 | Fix / limit | High paid spend with weak business-lead volume; search terms show Chilliwack-specific zero-conversion pockets. |
| North Vancouver - Capilano Mall | north-vancouver-capilano-mall | P1 | Continue / validate | Meta platform performance is strong, but prior creative-scramble risk means replacement creative IDs must stay verified. |
| Burlington - South Service Road | burlington-south-service-road | P1 | Continue | Efficient Google and healthy Form 4 target volume; open-house traffic spend is separate and should not be judged as enrollment CPL. |
| Oakville - Eighth Line | oakville-eighth-line | P1 | Budget watch | Campaigns were paused during May but paid Form 4 target volume exists; watch total budget before reactivating. |
| Markham - Esna Park | markham-esna-park | P1 | Continue / fix RSA | Business paid-form volume is solid; Google RSAs/search terms need relevance work before additional budget. |
| Mississauga - Meadowvale | mississauga-meadowvale | P1 | Continue | Best combined paid Form 4 volume; keep enrollment and summer-camp UTMs and reporting separate. |
| Victoria - University Heights | victoria-university-heights | P1 | Fix / watch | Google CPA is high and Meta frequency risk existed in earlier checks; repair query/RSA quality before scaling. |
| South Surrey - Panorama | surrey-panorama | P1 | Continue / fix slug | Performance is usable, but GA4/Form slug naming differs between `surrey-panorama` and `south-surrey-panorama`. |
| Surrey - Sunnyside | surrey-sunnyside | P0 | Fix / limit | High platform CPL/CPA and low attributed paid-form target volume; needs search and creative/tracking review before budget growth. |
| Kelowna - Spall | kelowna-spall | P0 | Fix / limit | Lowest GA4 paid lead coverage and weak Google CPA; add negatives and validate landing/conversion path. |

## 3. School Identity Rules

- Canonical reporting key is the lowercase school slug.
- Do not infer school UUIDs from slugs, campaign names, or page names.
- The live route uses `location=<school_uuid>` and `title=<school_slug>`, so the UUID and slug must both be preserved.
- One verified live example exists in the repo evidence: `location=812379b4-bcad-11ef-8bcb-028d36469a89&title=Markham-Esna-Park`. Treat this as a verified example, not as a complete UUID map.
- A school UUID crosswalk must come from a verified CEFA school identity source or the current plugin/database state.

## 4. Canonical Slug And Alias Warnings

| Topic | Rule |
|---|---|
| South Surrey / Panorama | Use `surrey-panorama` as the current canonical Form/audit slug. Track `south-surrey-panorama` as an alias until fixed in the canonical school identity source. |
| Open House campaigns | Keep open house traffic spend separate from parent enrollment CPL. |
| Ontario CORP PMAX | Keep separate from school CPL until asset/URL/UTM mapping proves school-level allocation. |
| Franchise campaigns | Keep out of parent school CPL unless UTM/form evidence proves overlap. |
| Duplicated source inventory rows | Reconcile against CEFA school identity sources before UUID mapping. |

## 5. Observed Paid Form 4 Target Slugs In May 2026

These slugs appeared in paid Form 4 target evidence. Some are active paid-media schools; others are observed outside the active 16-school May rollup and require confirmation before school CPL allocation.

| Slug | Paid Form 4 rows | Status |
| --- | ---: | --- |
| mississauga-meadowvale | 78 | Active paid-media school target in May 2026. |
| unresolved_target | 52 | Unresolved paid target; must be repaired before school CPL allocation. |
| calgary-beltline | 47 | Active paid-media school target in May 2026. |
| burlington-south-service-road | 43 | Active paid-media school target in May 2026. |
| richmond-south | 41 | Active paid-media school target in May 2026. |
| calgary-northland | 38 | Active paid-media school target in May 2026. |
| markham-esna-park | 36 | Active paid-media school target in May 2026. |
| north-vancouver-capilano-mall | 36 | Active paid-media school target in May 2026. |
| victoria-university-heights | 32 | Active paid-media school target in May 2026. |
| calgary-cornerstone | 29 | Active paid-media school target in May 2026. |
| oakville-eighth-line | 28 | Active paid-media school target in May 2026. |
| white-rock | 20 | Active paid-media school target in May 2026. |
| surrey-panorama | 20 | Active paid-media school target in May 2026. |
| chilliwack-cottonwood | 17 | Active paid-media school target in May 2026. |
| surrey-campbell-heights | 17 | Active paid-media school target in May 2026. |
| surrey-sunnyside | 15 | Active paid-media school target in May 2026. |
| kelowna-spall | 12 | Active paid-media school target in May 2026. |
| meadowtown | 6 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| north-vancouver-lions-gate | 5 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| vancouver-cambie | 5 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| calgary-beacon-hill | 5 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| burnaby-brentwood | 4 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| kelowna-mckay | 3 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| calgary-south | 3 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| langley-walnut-grove | 2 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| vancouver-commercial-drive | 2 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| surrey-guildford | 2 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| new-westminster-uptown | 2 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| south-surrey-morgan-crossing | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| vancouver-kitsilano | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| nanaimo | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| richmond-jacombs | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| ubc | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| victoria-westshore | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| south-delta | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| burnaby-kingsway | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| surrey-cloverdale | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |
| burnaby-canada-way | 1 | Observed paid target outside the 16-school active spend table; do not allocate to active school CPL without confirmation. |

## 6. Province / Region Inference For Active Schools

Use this only for naming and UTM region tokens, not for UUID mapping.

| Province / region | Active schools |
|---|---|
| Alberta (`ab`) | Calgary - Beltline; Calgary - Cornerstone; Calgary - Northland |
| British Columbia (`bc`) | Surrey - Campbell Heights; White Rock; Richmond South; Chilliwack - Cottonwood; North Vancouver - Capilano Mall; Victoria - University Heights; South Surrey - Panorama; Surrey - Sunnyside; Kelowna - Spall |
| Ontario (`on`) | Burlington - South Service Road; Oakville - Eighth Line; Markham - Esna Park; Mississauga - Meadowvale |

## 7. Required School Parameters In Events

| Parameter | Required? | Description |
|---|---|---|
| `school_uuid` | Required when known | The verified UUID from `location`. |
| `landing_school_slug` | Required | School context from landing URL/page/campaign. |
| `selected_school_slug` | Required | School submitted in the form or hidden school field. |
| `campaign_target_school_slug` | Required for paid reporting | School the paid campaign was intended to drive. |
| `school_context_match` | Recommended | Boolean comparing landing/selected/campaign-target school contexts. |
| `school_alias_used` | Recommended | Original alias when a normalized slug differs from submitted/source value. |

## 8. Safe Use Guidance

- Use the active school table to build naming, UTM, and reporting joins for the May 2026 paid-media scope.
- Use the observed paid target table for QA and leakage detection.
- Do not expand budgets or allocate CPL to observed non-active slugs without verifying campaign scope, selected school, and current school identity.
- Fix unresolved paid targets before relying on automation for school-level budget decisions.

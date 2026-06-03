# CEFA May 2026 Paid-Media And Tracking Reference

Prepared: 2026-06-03  
Audit window: 2026-05-01 to 2026-05-31  
Mode: read-only; no account, copy, creative, keyword, budget, or tracking changes were made.

## 1. Executive Rules From The May Audit

- Business CPL should use the redacted Gravity/Form 4 attribution export because it contains the actual May inquiry submissions and paid evidence.
- Platform conversion counts are useful for delivery diagnostics, but they overstate or understate the business layer by channel.
- GA4 `generate_lead` is the best GA4 lead signal for this audit; `form_submit` is too broad.
- CRM/GreenRope/KinderTales were not complete enough to calculate a May CRM CPL.
- Meta platform leads are not safe enough for budget decisions without Form 4 reconciliation.
- Google Search-term cleanup must be split by campaign because the May search-term pull hit the 10,001-row cap.

## 2. May 2026 Topline Totals

| Metric | Value |
|---|---:|
| Meta school spend | $31,125.96 |
| Google school Search spend | $13,339.19 |
| Total 16-school spend | $44,465.15 |
| Total budget | $44,500.00 |
| Meta platform leads | 810 |
| Google platform conversions | 262.42 |
| Total platform leads/conversions | 1,072.42 |
| GA4 paid generate_lead rows assigned to school campaigns | 446 |
| Form 4 paid leads assigned to the 16 school targets | 509 |

## 3. Layer Reconciliation

| Channel | Layer | Lead count |
| --- | --- | ---: |
| Meta paid social | Platform | 810 |
| Meta paid social | GA4 | 293 |
| Meta paid social | Form 4 | 338 |
| Google paid search | Platform | 262.42 |
| Google paid search | GA4 | 204 |
| Google paid search | Form 4 | 272 |
| Google Ontario CORP PMAX | Platform | 49.13 |
| Google Ontario CORP PMAX | GA4 | 32 |

Interpretation:

- Meta platform reported 810 leads, while GA4 showed 293 paid-social leads and Form 4 showed 338 Meta paid submissions.
- Google Ads reported 262.42 conversions, while GA4 showed 204 Google CPC leads and Form 4 showed 272 Google paid submissions.
- Google Ontario CORP PMAX is real spend/conversion volume, but it is not school-clean enough to allocate into school CPL without asset, URL, and UTM mapping.

## 4. Form 4 Attribution Snapshot

| Check | Value |
|---|---:|
| Raw Form 4 rows | 2,590 |
| May Form 4 rows | 2,590 |
| Clean non-test May rows | 2,586 |
| Test rows | 4 |
| Paid rows | 610 |
| Paid rows with click ID evidence | 606 |
| Paid rows with UTM/source-medium evidence | 4 |
| Paid target missing | 52 |
| Paid selected school missing | 12 |
| Cross-school paid inquiries | 196 |

Source buckets:

| Source bucket | Clean Form 4 rows |
|---|---:|
| google_business_profile | 888 |
| organic_search | 601 |
| meta_paid | 338 |
| direct_or_unknown | 295 |
| google_paid | 272 |
| website_navigation | 99 |
| referral_or_tracked_source | 68 |
| ai_or_chat_assisted | 18 |
| email | 7 |

## 5. School Summary

| School | Canonical slug | May budget | May spend | Form paid leads | Business CPL | Priority | June action |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| Calgary - Beltline | calgary-beltline | $4,000.00 | $3,992.14 | 47 | $84.94 | P1 | Fix |
| Calgary - Cornerstone | calgary-cornerstone | $1,500.00 | $1,404.20 | 29 | $48.42 | P1 | Continue |
| Calgary - Northland | calgary-northland | $3,000.00 | $3,009.73 | 38 | $79.20 | P1 | Fix |
| Surrey - Campbell Heights | surrey-campbell-heights | $3,000.00 | $3,041.76 | 17 | $178.93 | P0 | Fix / watch |
| White Rock | white-rock | $3,000.00 | $2,990.05 | 20 | $149.50 | P1 | Fix / watch |
| Richmond South | richmond-south | $3,000.00 | $3,006.75 | 41 | $73.34 | P1 | Continue |
| Chilliwack - Cottonwood | chilliwack-cottonwood | $3,000.00 | $2,991.92 | 17 | $176.00 | P0 | Fix / limit |
| North Vancouver - Capilano Mall | north-vancouver-capilano-mall | $3,000.00 | $3,028.03 | 36 | $84.11 | P1 | Continue / validate |
| Burlington - South Service Road | burlington-south-service-road | $1,500.00 | $1,500.91 | 43 | $34.90 | P1 | Continue |
| Oakville - Eighth Line | oakville-eighth-line | $1,500.00 | $1,608.46 | 28 | $57.45 | P1 | Budget watch |
| Markham - Esna Park | markham-esna-park | $3,000.00 | $2,848.94 | 36 | $79.14 | P1 | Continue / fix RSA |
| Mississauga - Meadowvale | mississauga-meadowvale | $3,000.00 | $2,954.77 | 78 | $37.88 | P1 | Continue |
| Victoria - University Heights | victoria-university-heights | $3,000.00 | $3,039.15 | 32 | $94.97 | P1 | Fix / watch |
| South Surrey - Panorama | surrey-panorama | $3,000.00 | $3,023.96 | 20 | $151.20 | P1 | Continue / fix slug |
| Surrey - Sunnyside | surrey-sunnyside | $3,000.00 | $3,035.43 | 15 | $202.36 | P0 | Fix / limit |
| Kelowna - Spall | kelowna-spall | $3,000.00 | $2,988.95 | 12 | $249.08 | P0 | Fix / limit |

## 6. June Action Matrix

| School | Priority | Action | Evidence note |
| --- | --- | --- | --- |
| Calgary - Beltline | P1 | Fix | Legacy Meta naming, high Google CPA, and paid-form cross-school leakage need cleanup before aggressive June scaling. |
| Calgary - Cornerstone | P1 | Continue | Both platforms are comparatively efficient; keep weekend-care/enrollment UTMs separated and validate quality. |
| Calgary - Northland | P1 | Fix | Meta is productive, but Google search-term waste around broad daycare intent needs campaign-level mining. |
| Surrey - Campbell Heights | P0 | Fix / watch | High Meta spend, low attributed Form 4 target volume, weak Google CPA, and missing Google GA4 campaign-target lead rows. |
| White Rock | P1 | Fix / watch | High total spend versus attributed paid form volume; clean geo leakage and query terms before raising June budgets. |
| Richmond South | P1 | Continue | Google is one of the strongest school Search campaigns; Meta has good platform volume but needs business-lead reconciliation. |
| Chilliwack - Cottonwood | P0 | Fix / limit | High paid spend with weak business-lead volume; search terms show Chilliwack-specific zero-conversion pockets. |
| North Vancouver - Capilano Mall | P1 | Continue / validate | Meta platform performance is strong, but prior creative-scramble risk means replacement creative IDs must stay verified. |
| Burlington - South Service Road | P1 | Continue | Efficient Google and healthy Form 4 target volume; open-house traffic spend is separate and should not be judged as enrollment CPL. |
| Oakville - Eighth Line | P1 | Budget watch | Campaigns were paused during May but paid Form 4 target volume exists; watch total budget before reactivating. |
| Markham - Esna Park | P1 | Continue / fix RSA | Business paid-form volume is solid; Google RSAs/search terms need relevance work before additional budget. |
| Mississauga - Meadowvale | P1 | Continue | Best combined paid Form 4 volume; keep enrollment and summer-camp UTMs and reporting separate. |
| Victoria - University Heights | P1 | Fix / watch | Google CPA is high and Meta frequency risk existed in earlier checks; repair query/RSA quality before scaling. |
| South Surrey - Panorama | P1 | Continue / fix slug | Performance is usable, but GA4/Form slug naming differs between `surrey-panorama` and `south-surrey-panorama`. |
| Surrey - Sunnyside | P0 | Fix / limit | High platform CPL/CPA and low attributed paid-form target volume; needs search and creative/tracking review before budget growth. |
| Kelowna - Spall | P0 | Fix / limit | Lowest GA4 paid lead coverage and weak Google CPA; add negatives and validate landing/conversion path. |

## 7. Meta Guardrails

- Use Form 4 for budget decisions until Meta Pixel/CAPI/custom conversion mapping is revalidated against a controlled successful Form 4 inquiry.
- Beltline had legacy/non-standard live campaign naming in May: `beltline | LSM | conversions (updated)`. Do not use that as the future naming model.
- Open House traffic rows for Burlington, Oakville, Markham, and Sunnyside need separate treatment from enrollment CPL.
- For new/replacement Meta ads, use unique uploads, unique hashes, fresh ad creative IDs, and no old post/story reuse.
- Do not enable Advantage+ media/music/multi-text unless explicitly approved and QA'd.

## 8. Google Ads Guardrails

- Split search-term pulls by campaign before writing final negatives because the May pull hit the 10,001-row cap.
- Treat Poor RSA strength as a copy/relevance repair cue, not an automatic pause rule.
- Review weak/irrelevant query themes for negatives: competitor daycare names, wrong geography, Montessori, YMCA, 10-dollar/day daycare, broad review queries, and unrelated private-school intent.
- Ontario CORP PMAX must remain separate until school-level asset/URL/UTM mapping is proven.

## 9. Budget / Scaling Guardrails

- Do not scale P0 schools until business CPL and query/tracking issues are fixed.
- Protect efficient schools but still validate lead quality: Mississauga - Meadowvale, Burlington - South Service Road, Calgary - Cornerstone, Richmond South, and North Vancouver - Capilano Mall.
- Schools marked `Fix / limit` or `Fix / watch` need tracking, query, creative, or mapping repair before budget increases.

## 10. Open Items From The Audit

- CRM/GreenRope/KinderTales access is not complete enough for a CRM CPL.
- Google Search-term mining needs campaign-split pulls.
- Meta currency field was not included in the Supermetrics campaign pull; account context and GA4 indicate CAD, but Meta cost rows should be treated as account-currency values.
- South Surrey/Panorama naming variation must be fixed before applying automated UTM/name joins.
- PMAX school allocation is blocked until asset and URL mapping is proven.

# Plugin Hook Map

This file captures the most important runtime behaviors from the verified plugin review, without publishing the proprietary plugin source itself.

## Gravity Forms Core Sequence

Verified execution order:

1. `gform_pre_submission`
2. `gform_pre_submission_filter`
3. core submission handler
4. `gform_after_submission`

## School Journey Plugin Hooks

The current custom plugin binds to Gravity Form `4` through:

- `gform_pre_render_4`
- `gform_pre_validation_4`
- `gform_admin_pre_render_4`
- `gform_pre_submission_filter_4`
- `gform_pre_submission_4`
- `gform_after_submission_4`

## Key Runtime Functions

### Form-population behavior

- `populate_programs`
- `populate_school_dropdown`
- `get_programs_by_school`
- `get_offer_days_by_school`

### Submit-time behavior

- `cefa_pre_submission_clean_and_tracking`
- `send_to_kindertales_api`

## Front-End Behavior Summary

The current front-end script:

- reads `location` from the query string
- splits it into one or more UUIDs
- writes those UUIDs into the hidden school field
- calls program and days-offered AJAX actions
- repopulates after Gravity Forms `gform_post_render`

## Important Findings

### Direct KinderTales delivery

The current runtime posts directly to KinderTales after submission.

### Hidden attribution field writeback

The current runtime fills hidden attribution fields from cookies at submit time.

### Public AJAX surface

The current program and days-offered lookup actions are public and unauthenticated.

### Front-end bug

The current JS attempts to call `split()` on the `location` query parameter before verifying it exists.

If the page loads without `location=...`, the script can fail early.

# Parent Inquiry Runtime

## Final Call

The current parent inquiry path is still a legacy Gravity Forms plus custom-plugin implementation.

It is not just a simple form embed.

## Verified Runtime Shape

- Live route pattern:
  - `/inquire-form/?location=<school_uuid>&title=<school_slug>`
- Current form:
  - Gravity Form `4`
- Current school-entry model:
  - one shared backend Gravity Form reused across schools
  - the school is locked on the front end by the URL parameters, especially `location`
- Current page shell:
  - Elementor-wrapped
- Current supporting plugin:
  - `cefa-school-journey-code-manager`

## What The Custom Plugin Currently Does

Based on verified plugin inspection, the custom plugin currently:

- loads front-end logic only on page slug `inquire-form`
- binds server-side hooks specifically to Gravity Form `4`
- writes selected school UUIDs into the hidden school field
- populates program options based on school selection
- filters days-offered checkboxes based on school selection
- cleans the title slug field before submission
- backfills hidden attribution fields from cookies at submit time
- posts the final inquiry directly to KinderTales after successful form submission

## Why This Matters

A redesign cannot assume that Gutenberg alone will preserve the current business logic.

If the new build changes:

- the page slug
- the form ID
- the query-parameter school-binding contract
- the hidden field structure
- the school selection model

then the current runtime contract will break unless the legacy responsibilities are intentionally ported or replaced.

## Highest-Signal Risks

### 1. Page-slug coupling

The custom front-end behavior only loads on `inquire-form`.

### 2. Form-ID coupling

The current server-side logic is hard-wired to form `4`.

### 3. Database coupling

The custom plugin expects its own school/program/journey tables to already exist.

### 4. Hidden attribution writeback

The current runtime does not rely only on visible form fields. It also fills hidden attribution fields at submit time from cookies.

### 5. Direct downstream delivery

The current KinderTales path is implemented as a direct post-submission request from the custom plugin.

## Review Guidance

Any replacement plan should answer:

- what gets ported
- what gets retired
- what moves into a new plugin
- what moves into GTM
- what must remain server-side

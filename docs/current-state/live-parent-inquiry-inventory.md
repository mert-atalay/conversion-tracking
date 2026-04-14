# Live Parent Inquiry Inventory

## Verified Live Example

- `https://cefa.ca/inquire-form/?location=812379b4-bcad-11ef-8bcb-028d36469a89&title=Markham-Esna-Park`

## Verified Stack

- form wrapper: `#gform_wrapper_4`
- form element: `#gform_4`
- Gravity Forms assets load on page
- Elementor assets load on page
- `cefa-school-journey-code-manager` front-end JS loads on page

## Visible Fields

- guardian first name: `input_26`
- guardian last name: `input_27`
- relationship: `input_3`
- relationship other: `input_23`
- email: `input_6`
- phone: `input_7`
- child first name: `input_28`
- child last name: `input_29`
- site address: `input_52.*`
- gender: `input_10`
- date of birth: `input_9`
- requested start date: `input_11`
- program dropdown: `input_22`
- days per week: `input_50.*`
- postal code: `input_13.*`
- source: `input_18`
- source other: `input_19`
- comments: `input_20`
- consent: `input_24.*`

## Hidden Or Defaulted Fields

- field `30`:
  - location UUID
- field `31`:
  - title slug
- field `32[]`:
  - hidden school multiselect used by the custom plugin
- fields `33-39` and `45-49`:
  - hidden attribution and landing-context fields

## Live Conditional Logic

- field `23` appears when relationship is `Other`
- field `19` appears when source is `Other`

## Runtime Interpretation

The live parent inquiry page is a Gravity Forms submission surface wrapped in extra custom runtime behavior.

That means any redesign review should inspect:

- visible fields
- hidden fields
- submit-time field writeback
- post-submission delivery

not just the rendered front-end form.

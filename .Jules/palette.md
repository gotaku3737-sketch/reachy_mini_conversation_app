## 2024-05-25 - [Aria-describedby pattern for inputs with descriptions]
**Learning:** Tool descriptions presented alongside checkboxes were visually associated but programmatically separated. Adding an `id` to the description and `aria-describedby` to the input ensures screen readers provide full context during keyboard navigation.
**Action:** When adding helper text or descriptions to form inputs, always generate a unique ID and link it using `aria-describedby`.

## 2026-09-15 - [Dynamic accessible form validation for Vanilla JS]
**Learning:** In this vanilla JS architecture, error messages are rendered dynamically into existing `settings-status` elements rather than unmounting/mounting DOM nodes. To make form validation errors accessible, the error element must be explicitly linked back to the input on failure and unlinked upon user correction.
**Action:** When handling form submission errors (like invalid tool space slugs), dynamically add `aria-invalid="true"` and append the status element's ID to the field's `aria-describedby` attribute. Ensure these are cleaned up on the next `input` event so the screen reader doesn't keep announcing old errors.

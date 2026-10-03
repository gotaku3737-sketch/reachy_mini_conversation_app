## 2024-05-24 - Contextual Disabled States via `title` Attribute
**Learning:** Adding a `title` attribute to explicitly describe *why* an element is disabled (e.g. "Only applicable in Local mode", "Loading…", "Tool Space editing is locked") improves UX and accessibility for users who might otherwise be confused why they can't interact with a specific UI component.
**Action:** When a UI component switches into a disabled state dynamically or due to specific configurations, dynamically update a `title` attribute on that element to provide context to the user. Ensure to remove the title when the element is re-enabled to prevent misleading tooltips.
## 2026-09-26 - Dynamic aria-labels for State-Bearing Buttons
**Learning:** Using a static `aria-label` on a button whose inner text changes dynamically (e.g., to show a selected profile or state) completely hides the dynamic text from screen readers, as the `aria-label` overrides the element's entire content.
**Action:** When a button acts as both an action trigger and a state display, dynamically update its `aria-label` via JavaScript whenever the state changes so that screen reader users hear both the action and the current state (e.g., `Change personality. Current: Zen Master`).
## 2026-09-27 - Inline Validation Context via aria-invalid and aria-describedby
**Learning:** Adding a generic status message below a form fails to give screen reader users context about which specific fields were rejected by backend validation.
**Action:** Always dynamically toggle `aria-invalid="true"` on the offending input fields upon submission failure, and append the error message's ID to the field's `aria-describedby` attribute (e.g. `aria-describedby="hint-id error-id"`). Crucially, bind `input` and `change` event listeners to immediately clean up `aria-invalid`, `aria-describedby`, and the error text as soon as the user starts correcting the fields.
## 2026-09-28 - Explicitly Clear Error Text on Input Events
**Learning:** Screen readers may read the text content of error nodes even if visually hidden via CSS classes if they are left in the DOM. Removing visual error classes alone is insufficient.
**Action:** When clearing form validation errors on `input` or `change` events, ensure that you explicitly clear the text content of the error element (e.g. `errorBox.textContent = ""`) alongside removing visual classes like `is-visible` or `is-error`.
## 2024-11-13 - Redundant aria-label Overriding Visible Label
**Learning:** Using an `aria-label` on an input element that is correctly wrapped inside a `<label>` (with visible text) completely overrides the visible text for screen readers, breaking WCAG 2.5.3 (Label in Name). Voice dictation users rely on saying the visible label, and if the accessible name differs (or is completely overridden), dictation fails.
**Action:** When a form element has a visible label (e.g. wrapped in a `<label>` containing text, or linked via `id` and `for`), avoid adding an `aria-label` that duplicates or overrides that text. Let the element derive its accessible name from the native label instead.

## 2024-05-15 - Missing Initial Tooltips on Disabled Elements
**Learning:** We dynamically manage tooltips for disabled elements (adding a reason when disabled, removing when enabled), but elements that render in a disabled state immediately on mount (like those waiting for initial async data) were missing their initial `title`. Without this initial tooltip, screen reader and mouse users lack context for why the element is disabled until its state changes.
**Action:** When a UI component includes elements that are disabled by default (e.g., during an initial fetch), ensure they are instantiated with a `title` attribute explaining the loading/disabled state.

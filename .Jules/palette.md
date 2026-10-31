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

## 2026-10-10 - WCAG 2.5.3 Label in Name for Voice Dictation
**Learning:** Adding an `aria-label` to elements (like buttons or links) that already have visible text can override that text for assistive technologies. This breaks WCAG 2.5.3 (Label in Name), making it impossible for Voice Dictation users to target the element by speaking its visible text, because the accessible name is entirely different.
**Action:** Never use `aria-label` on an element that has visible, descriptive text content unless it's strictly necessary to append context, and even then, the accessible name must start with the visible text. Rely on the visible text for the accessible name wherever possible.
## 2026-10-15 - Dynamic Visible Text vs aria-label (WCAG 2.5.3)
**Learning:** Using `aria-label` to provide extra context (e.g., "Change personality. Current: X") on a button that already contains visible text ("Personality X") overrides the visible text for assistive technologies. This breaks WCAG 2.5.3 (Label in Name), meaning Voice Dictation users who speak the visible text will fail to activate the button.
**Action:** When a button's visible text already conveys its purpose and state, rely on the visible text for the accessible name and avoid `aria-label`. Use the `title` attribute to provide tooltips for mouse users without breaking voice control.

## 2024-05-18 - Missing Tooltips on Actions
**Learning:** Icon-only buttons with an `aria-label` for screen readers should also mirror that text in a `title` attribute to provide a visual tooltip for mouse users.
**Action:** When adding or auditing icon-only buttons, check for a `title` attribute.
## 2026-10-24 - Preserving Accessible Names with title Tooltips
**Learning:** When trying to add visual tooltips to buttons via the `title` attribute, removing the `aria-label` can cause a severe accessibility regression. For buttons with generic visible text (like "Manage tools" or "Remove"), the `aria-label` provides essential context to screen reader users navigating out of context.
**Action:** When adding supplementary `title` tooltips for mouse users, ensure the existing `aria-label` remains intact to preserve context for assistive technologies. Additionally, ensure the `aria-label` always *starts* with the visible text to comply with WCAG 2.5.3 (Label in Name), which avoids breaking voice control tools.
## 2024-05-24 - Restoring Tooltips on Re-enabled Elements
**Learning:** When dynamically managing disabled states, using `removeAttribute('title')` unconditionally when re-enabling an element can permanently destroy any original, static tooltips (like those required for icon-only buttons).
**Action:** When a component is re-enabled, check if it has an `aria-label`. If so, restore the `title` attribute from the `aria-label`. Otherwise, safely remove it.

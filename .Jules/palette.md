## 2024-05-24 - Contextual Disabled States via `title` Attribute
**Learning:** Adding a `title` attribute to explicitly describe *why* an element is disabled (e.g. "Only applicable in Local mode", "Loading…", "Tool Space editing is locked") improves UX and accessibility for users who might otherwise be confused why they can't interact with a specific UI component.
**Action:** When a UI component switches into a disabled state dynamically or due to specific configurations, dynamically update a `title` attribute on that element to provide context to the user. Ensure to remove the title when the element is re-enabled to prevent misleading tooltips.

## 2024-05-18 - Missing Tooltip on Async Disable
**Learning:** During initial UI rendering of settings views, buttons tied to async data fetches (like voice lists) are often initialized in a disabled state but without a tooltip explaining why (e.g., "Loading voices..."). This creates an unhelpful "dead UI" moment before the async operation resolves or errors out.
**Action:** Always explicitly add a `title` explaining the loading/waiting state to buttons that are initialized as `disabled` pending an async operation, and ensure the code that enables them removes the title (which the codebase already correctly does).

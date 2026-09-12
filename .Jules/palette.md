## 2024-05-25 - [Aria-describedby pattern for inputs with descriptions]
**Learning:** Tool descriptions presented alongside checkboxes were visually associated but programmatically separated. Adding an `id` to the description and `aria-describedby` to the input ensures screen readers provide full context during keyboard navigation.
**Action:** When adding helper text or descriptions to form inputs, always generate a unique ID and link it using `aria-describedby`.

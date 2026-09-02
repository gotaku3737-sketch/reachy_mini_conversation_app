## 2024-03-01 - Hide decorative emojis from screen readers
**Learning:** Emojis used as decorative icons (like 🎤 for "Microphone" or 🤖 for "Robot") are often read aloud by screen readers with their literal unicode descriptions, which adds noise and can be very confusing when placed next to actual descriptive text.
**Action:** Always add `aria-hidden="true"` to emojis that are purely decorative or redundant with adjacent text, especially in feature grids, lists, or headers.

## 2024-09-02 - Use title attributes for discoverability on interactive icon-only elements
**Learning:** For interactive UI elements lacking visible text labels (like the conversation orb that acts as a microphone toggle, or icon-only edit/delete buttons), standard ARIA labels help screen readers but do not provide visual feedback on hover. This leads to poor discoverability of features for sighted mouse users.
**Action:** Always add `title` attributes on interactive icon-only elements (unless a custom tooltip component is used) to provide native hover tooltips. These `title` attributes should generally match the `aria-label` text to keep the accessible name and visual tooltip consistent.

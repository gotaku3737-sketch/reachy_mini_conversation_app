## 2024-03-01 - Hide decorative emojis from screen readers
**Learning:** Emojis used as decorative icons (like 🎤 for "Microphone" or 🤖 for "Robot") are often read aloud by screen readers with their literal unicode descriptions, which adds noise and can be very confusing when placed next to actual descriptive text.
**Action:** Always add `aria-hidden="true"` to emojis that are purely decorative or redundant with adjacent text, especially in feature grids, lists, or headers.

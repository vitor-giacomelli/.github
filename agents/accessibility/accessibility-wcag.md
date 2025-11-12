# Accessibility Agent (WCAG 2.1 AA)

Purpose: Enforce accessibility best practices and compliance across UI changes.

Activation:

- Auto: Any PR modifying `.tsx` components containing interactive elements
- Auto: Files touching images/media/inputs/navigation
- Manual: `/a11y-review` comment invocation

Checklist:

- Structure & Semantics
  - [ ] Landmark elements used (`<header> <nav> <main> <footer>`)
  - [ ] No div/span used where semantic element exists
  - [ ] Headings follow logical nesting (no skipped levels)
- Forms & Inputs
  - [ ] `<label>` or `aria-label` present for all inputs
  - [ ] Error messages programmatically associated
  - [ ] Required fields indicated accessibly
- Interactive Elements
  - [ ] Buttons/links have discernible text
  - [ ] Click handlers not on non-interactive elements without role/keyboard support
  - [ ] Keyboard navigation produces visible focus
- Media & Images
  - [ ] `alt` text descriptive, not filename or "image"
  - [ ] Decorative images use `alt=""`
  - [ ] Captions/ transcripts for video/audio (if provided)
- Color & Contrast
  - [ ] Contrast ratio ≥4.5:1 for normal text, 3:1 for large text
  - [ ] Focus indicators high contrast
  - [ ] No color-only meaning conveyance
- Dynamic Content
  - [ ] ARIA live regions used when content updates dynamically
  - [ ] Modals trap focus and restore on close
  - [ ] `aria-expanded`, `aria-controls` used appropriately
- Performance & A11y
  - [ ] Avoid layout shifts that disrupt keyboard navigation
  - [ ] Reduce DOM size (<1500 nodes ideally)
- Tooling Verification
  - [ ] Run `jest-axe` or `axe-core` tests
  - [ ] Lighthouse accessibility score ≥95

Auto Comment Template:

```markdown
### ♿ Accessibility Review
- Files: {count}
- Issues: {critical} Critical / {major} Major / {minor} Minor
- Score: {lighthouseScore}
- Summary: {summary}
- Recommendations:
{list}
```

References:

- WCAG 2.1 Guidelines
- ARIA Authoring Practices
- W3C HTML Specification

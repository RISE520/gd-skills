# RISE AI Landing Page - Development Guidelines

## Project Overview

**RISE** is a modern, visually rich landing page for an AI technology company. The entire application is contained in a single `index.html` file with embedded CSS and JavaScript.

### Key Characteristics
- **Type**: Single-file landing page (HTML + CSS + JS)
- **Purpose**: Premium AI company marketing website
- **Primary Features**: Animations, multi-language support, responsive design
- **Target Platforms**: Desktop (primary), mobile (responsive)
- **Languages Supported**: English (en), Simplified Chinese (zh)

---

## Project Structure

```
guangzhou-ai-tech/
├── index.html              # Main application file (all HTML/CSS/JS combined)
├── workspace.code-workspace # VS Code workspace config
├── .git/                    # Version control
└── .github/
    └── copilot-instructions.md (this file)
```

### File Architecture
- **HTML**: Semantic structure with data attributes for i18n
- **CSS**: ~1200 lines using CSS variables for theming
- **JavaScript**: Event handlers, animations, particle systems, translations

---

## Key Technologies & Patterns

### Design System
- **Color Scheme**: Dark theme with indigo/purple accents
  - Primary: `#030308` (dark bg)
  - Accent: `#4f46e5` (indigo)
  - Light Accent: `#818cf8`
- **CSS Variables**: Defined in `:root` for easy customization
- **Typography**: Inter (EN), Noto Sans SC (Chinese)

### Animation Systems

1. **Loader Animation** (initial page load)
   - Particle system with 60 particles
   - Expanding rings
   - Progress bar with text updates
   - Different loading text in both languages

2. **Hero Section Animations**
   - Floating orbs with radial gradients
   - 80 animated particles with connections
   - Mouse-following particle effects
   - Slogan stagger animations

3. **Custom Cursor System**
   - Ring cursor with scale transformation
   - Particle trail effect
   - Hover states for interactive elements

4. **About Section**
   - Node-based network visualization
   - Center node with pulsing glow
   - Dynamic connections between nodes

### Multi-Language Support (i18n)
- Translation object with `en` and `zh` keys
- Data attributes: `data-i18n` for content, `data-i18n-placeholder` for form inputs
- Language toggle button switches between EN/Chinese
- Current language: `currentLang` variable (defaults to 'en')
- Loader text updates based on language

### Responsive Design Breakpoints
- Desktop: Default (cursor effects, full nav)
- Tablet/Mobile (≤768px):
  - Custom cursor hidden
  - Hamburger menu for navigation
  - Single-column layout
  - Adjusted section padding

---

## Common Development Tasks

### Adding New Sections
1. Add HTML section with `id` and semantic structure
2. Use `data-i18n` attributes for translatable text
3. Add CSS styling following existing patterns
4. Add animations if needed (use existing particle classes)
5. Update translations object in JavaScript
6. Add nav link with `data-i18n` attribute

### Updating Animations
- **Particle classes**: `HeroParticle`, `LoaderParticle`, `TrailParticle`, `AboutNode`
- All use `update()` and `draw(ctx)` methods
- Canvas animations use `requestAnimationFrame` loops
- Modify `pulseSpeed`, `speed`, `amp` for timing adjustments

### Language Integration
- Add new translation keys to both `en` and `zh` objects
- Use `data-i18n="category.key"` in HTML
- Use `data-i18n-placeholder="category.key"` for form placeholders
- Call `applyTranslations()` after language change

### Form Handling
- Currently alerts on submit in `handleSubmit(event)`
- Form reset triggered after submission
- Can be extended to send data to backend API

---

## Code Quality Standards

### Naming Conventions
- **Functions**: camelCase (`animateLoader`, `handleSubmit`)
- **Classes**: PascalCase (`HeroParticle`, `TrailParticle`)
- **Variables**: camelCase (`currentLang`, `cursorX`)
- **CSS Classes**: kebab-case (`.hero-tag`, `.service-card`)

### Performance Considerations
- Canvas animations use `requestAnimationFrame` for smooth 60fps
- Particle cleanup prevents memory leaks
- Intersection Observer for scroll-triggered animations
- CSS transforms used for performance (no layout thrashing)

### Accessibility
- Semantic HTML structure
- Mobile menu with proper toggle
- Form inputs have placeholders
- Color contrast meets WCAG standards

---

## Git Workflow

### Commit Message Pattern
- Feature-focused commits with clear descriptions
- Recent examples:
  - `Add mouse trail effect - Enhanced cursor with particle trails`
  - `Fix mobile language toggle visibility with !important`
  - `Set English as default language`

### Branching
- Primary branch: `main`
- Remote: `origin`

---

## Common Tasks & Solutions

### Disable Custom Cursor Globally
- Set `display: none` on `.cursor` and `.cursor-dot` classes
- This is already done on mobile (media query at 768px)

### Adjust Animation Speed
- Canvas animations: Change multipliers in update loops (e.g., `loadProgress += 0.008`)
- Particle speed: Modify `speedX`, `speedY`, `pulseSpeed` properties
- CSS transitions: Adjust timing values (e.g., `0.6s ease`)

### Modify Color Scheme
- Update CSS variables in `:root` block
- Changes propagate throughout the app
- Particle colors use HSL for easy adjustments

### Add Form Validation
- Currently basic HTML5 validation (`required` attributes)
- Extend `handleSubmit()` for custom validation logic
- Add error messages or feedback

### Mobile Menu Behavior
- Toggle managed by `.active` class
- Overflow hidden applied to body when active
- Click handler closes menu (`onclick="toggleMobileMenu()"`)

---

## Performance Metrics

### Key Optimizations
✓ Single HTTP request (no external JS libraries)
✓ Google Fonts loaded asynchronously
✓ Canvas rendering for animations
✓ CSS-in-head for faster FCP
✓ Lazy translation loading
✓ Particle cleanup in animation loops
✓ Mobile detection prevents unnecessary cursor effects

### Load Time Milestones
1. Loader visible: ~0.5s
2. Loader completes: ~6-8s (progress bar driven)
3. Hero content visible: Immediately after loader completes
4. Full page interactive: ~10s

---

## Extension Ideas

- Search engine optimization (meta tags, structured data)
- Analytics integration (Mixpanel, Segment, etc.)
- Form backend integration (SendGrid, Webhook services)
- Multi-page routing (if converted to JS framework)
- Dark/Light theme toggle
- Video backgrounds for sections
- Client testimonials carousel
- Blog or resource center

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Cursor not showing | Check media queries; custom cursor hidden on mobile |
| Animations laggy | Reduce particle count or check CPU in DevTools Performance tab |
| Language not updating | Verify translation key exists in both `en` and `zh` objects |
| Form not submitting | Check `handleSubmit()` logic and console for errors |
| Mobile nav not closing | Ensure all nav links have `onclick="toggleMobileMenu()"` |
| Particles not animating | Verify canvas is resizing (check ResizeObserver) |

---

## Resources & References

- [Canvas API Docs](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
- [requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)
- [CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)
- [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)

---

## Quick Start for AI Agents

When helping with this project:

1. **Understand the file structure**: Single `index.html` contains all code
2. **Locate translations**: Search for `translations = { en: {...}, zh: {...} }`
3. **For animations**: Look for `animate*()` functions and particle `class` definitions
4. **For styling**: CSS is in `<style>` tag; uses custom properties
5. **For responsive changes**: Modify `@media (max-width: 768px)` block
6. **For language keys**: Add to both language objects
7. **For new features**: Follow existing patterns (classes, naming, structure)

**Never**: Extract code into separate files (single-file architecture is intentional)

---

*Last updated: 2026-04-04*
*Git status: main branch*

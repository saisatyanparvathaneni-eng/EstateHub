# EstateHub Implementation Plan

## Product scope
EstateHub is a responsive, accessible, frontend-only property discovery demo for fictional Indian listings. The home page will let visitors explore listings, search by free text, combine filters, sort results, open details, save favorites, compare up to three properties, prepare a contact inquiry, open demo login/registration and list-property forms, toggle light/dark theme, and review honest FAQ/limitations copy.

## Implementation approach
- Use semantic HTML5 in a single-page layout with anchored sections for navigation.
- Use a small data layer in `script.js` with stable IDs and explicit `listingType`, `priceBasis`, location, facilities, and demo metadata.
- Render property cards and comparison rows from data rather than duplicating markup.
- Keep all interactions in vanilla JavaScript: search, combined filtering, sorting, favorites, comparison, modal focus management, forms, toast notices, local image previews, FAQ accordion, mobile menu, theme persistence, and localStorage recovery.
- Use browser-native validation plus custom messages and avoid storing passwords or sensitive form contents.
- Use responsive CSS Grid/Flexbox with reduced-motion support, visible focus rings, high-contrast states, and graceful image fallbacks.
- Use local generated visual assets for the hero and listing cards so the site has no fragile third-party image dependency.

## Project structure
```
estatehub/
├── index.html
├── styles.css
├── script.js
├── README.md
├── plan.md
├── TODO.md
├── public/
│   └── manus-routes.json
└── assets/
    ├── hero-estate.svg
    └── property-*.svg
```

## Design direction

### Style options considered
- **Editorial property journal — 0.06 probability:** gallery-led, quiet, typographic, with warm paper surfaces and sharp data details.
- **Modern brokerage dashboard — 0.87 probability:** structured, high-trust, utility-first interface with crisp filters and compact cards.
- **Soft lifestyle catalog — 0.07 probability:** lighter, airy, image-forward browsing with gentle rounded components.

**Chosen style: Editorial property journal.**

### Design movement
Contemporary editorial real-estate publishing: a magazine-like narrative hero paired with a practical marketplace toolset.

### Core principles
1. Make discovery feel calm and intentional, not like a noisy classifieds feed.
2. Pair expressive imagery with precise pricing and property metadata.
3. Treat demo limitations as part of the product's trust story.
4. Make every action reversible, keyboard reachable, and obvious.

### Color philosophy
Warm limestone backgrounds make the interface feel residential and tactile; deep ink/navy provides authority and contrast; terracotta is the ownable EstateHub signature color, suggesting brick, soil, and human warmth; sage and muted gold support status and premium cues without becoming decorative noise.

### Layout paradigm
Use an asymmetrical, editorial composition: a wide hero narrative paired with a floating search instrument, section headers aligned on a strong left rail, and listing cards that alternate between image-led and data-led emphasis. Avoid a uniformly centered SaaS grid.

### Signature elements
- Terracotta corner mark and monogram-style `EH` logo.
- Pill-shaped filter controls set into a dark ink search rail.
- Small uppercase metadata labels and fine rules inspired by a property magazine.

### Interaction philosophy
Interactions should feel like turning pages and annotating a shortlist: filters update calmly, saved state is immediate, and modal details preserve context. Toasts explain demo boundaries instead of pretending backend actions occurred.

### Animation
Use short opacity/translate transitions for cards, menus, modals, and toast notices. Avoid looping motion. Respect `prefers-reduced-motion` by removing transforms and transition durations.

### Typography system
Use `DM Sans` for readable UI copy and `Playfair Display` for the editorial display headline, both loaded from Google Fonts with system fallbacks. Use uppercase 11–12px labels with increased letter spacing for metadata; use clamp-based headings for fluid responsive hierarchy.

### Brand essence
EstateHub is a calm, transparent property discovery studio for people comparing their next place before they commit. Personality: grounded, discerning, human.

### Brand voice
Headlines are confident but not salesy; CTAs are clear and practical; microcopy is transparent about demo behavior.
- Example headline: “Find the place that makes sense next.”
- Example microcopy: “Illustrative listings, thoughtful tools — no invented promises.”

### Wordmark & logo
A compact `EH` monogram in a terracotta outlined square sits beside a serif EstateHub wordmark. The mark is implemented as accessible inline SVG/CSS rather than relying on an external logo file.

### Signature brand color
Terracotta `#c86645`, used for primary actions, active states, and the hero monogram.

## Build and delivery workflow
1. Create the HTML shell, SVG assets, data model, and primary styles.
2. Add interaction logic and localStorage-safe state handling.
3. Add the exam-ready README and route manifest.
4. Configure host diagnostics for HTML, CSS, and JavaScript, then run focused syntax checks.
5. Declare the static dev command on port 3000 and verify the preview endpoint plus route manifest.
6. Capture desktop/mobile screenshots for visual QA, fix any concrete issues, then commit the completed project to `origin/main` for checkpointing.

## Material constraints
- No React or frontend framework.
- Fictional demo listings only; no claims of verified listings, live availability, or real agent receipt.
- No password or unnecessary personal data persistence.
- No exact fictional addresses or fake contact details.

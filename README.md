# EstateHub — Find a Place to Call Home

EstateHub is a polished, responsive real-estate marketplace frontend demonstration built with semantic HTML5, CSS3, and vanilla JavaScript. The experience is designed for an engineering college practical, portfolio presentation, and viva: it demonstrates searching, combined filtering, sorting, property details, favorites, comparison, forms, LocalStorage, theme persistence, accessibility, and honest product limitations.

> **Important:** Every property, price, location, contact detail, and verification flag in this project is fictional demo content. This website is not a brokerage service and does not send inquiries, publish listings, create accounts, verify ownership, or provide live availability.

## Problem statement

People browsing property websites often need to compare many kinds of information at once: price basis, city, locality, rooms, area, furnishing, facilities, and intended use. EstateHub demonstrates how a frontend can bring those signals into one calm, understandable browsing flow without pretending that a static demo is a real marketplace.

## Objectives

The project aims to create a modern and accessible interface; represent property data as reusable JavaScript objects; allow case-insensitive free-text search and multiple filters; keep sale and rental pricing semantically distinct; support saved properties and three-item comparison; validate inquiry, authentication, and listing forms; persist safe demo preferences; and document the limitations that would need backend services in a production product.

## Technologies used

- HTML5 semantic elements such as `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `dialog`, `form`, `fieldset`, and `details`.
- CSS3 with custom properties, Grid, Flexbox, `clamp()`, responsive media queries, `color-mix()`, transitions, and reduced-motion support.
- Vanilla JavaScript using arrays, objects, DOM rendering, event delegation, native form validation, `Intl.NumberFormat`, FileReader, and LocalStorage.
- Local SVG editorial property illustrations are bundled under `assets/`, so the project runs from a GitHub checkout or a local file server without Manus storage access.

## Features

The home page contains EstateHub branding, a hero search, illustrative statistics, category filters, featured property cards, a budget-led discovery section, amenity education, product principles, saved properties, FAQ, and a footer. The listing area supports full-text search, listing type, city, property type, sale/monthly price band, bedrooms, bathrooms, area, furnishing, amenity, demo-verification, and sort filters.

Each property card shows the listing type, price basis, location, property type, room details when applicable, area, facilities, status, favorite action, details action, contact action, and comparison action. The details dialog adds a gallery preview, descriptive copy, facilities, a demo location placeholder, save, compare, and contact actions.

The favorites badge, Saved Properties section, and comparison drawer update immediately. Comparison is limited to three properties and preserves the distinction between a purchase total and monthly rent. Contact, login, account creation, and List Your Property are intentionally honest demo flows.

## Folder structure

```text
estatehub/
├── index.html              # Semantic page shell and accessible dialogs/forms
├── styles.css              # Theme, responsive layout, components, states
├── script.js               # Data, rendering, filters, modals, persistence
├── README.md               # Setup, architecture, limitations, viva questions
├── plan.md                 # Implementation and design plan
├── TODO.md                 # Acceptance-oriented project checklist
├── public/
│   └── manus-routes.json   # Route manifest for the managed preview
├── assets/                 # Portable local SVG property illustrations
└── screenshots/            # Desktop and mobile preview captures
```

## Installation and running locally

No package manager or build step is required. Download or clone the project, then open `index.html` in a modern browser. For a more realistic local server, run one of the following from the project folder:

```bash
python3 -m http.server 3000
# or
npx serve .
```

Then visit `http://localhost:3000`. The managed EstateHub project uses the same static command on port 3000 for Preview.

## Search and filtering logic

The `DEMO_PROPERTIES` array contains all fictional listings. `matchingProperties()` derives a filtered copy using the current `state` object. Search lowercases a combined string containing title, city, locality, property type, description, and facilities, so a single query can match any of those fields.

Other predicates are applied together: listing type, city, property type, category, price, rooms, area, furnishing, selected facilities, and the optional demo-verification flag. The displayed array is then sorted by featured status, date, price, area, or bedrooms. A rental price is represented with `basis: "monthly"`; a sale listing uses `basis: "sale"`. `formatMoney()` uses `Intl.NumberFormat('en-IN')` and appends `/mo` to monthly prices.

## Property data structure

A typical listing has the following shape:

```js
{
  id: 'eh-001',
  title: 'Greenview Residency',
  listingType: 'Buy',
  type: 'Apartment',
  city: 'Hyderabad',
  locality: 'Kondapur',
  price: 4800000,
  basis: 'sale',
  bedrooms: 2,
  bathrooms: 2,
  area: 1240,
  furnishing: 'Semi-furnished',
  facilities: ['Covered parking', 'Elevator', 'Security'],
  description: 'Fictional demo description',
  date: '2026-11-14',
  featured: true,
  verifiedDemo: true,
  image: '/manus-storage/...'
}
```

Stable IDs keep favorites and comparison records associated with the correct listing.

## LocalStorage implementation

The app uses safe JSON helpers so malformed stored JSON does not crash the page. The keys are `estateHubTheme`, `estateHubFavorites`, `estateHubComparison`, `estateHubPreferences`, and `estateHubDemoListings`. Theme, favorite IDs, comparison IDs, basic search preferences, and a limited set of non-sensitive user-submitted demo listings may be restored.

Passwords, inquiry contents, and unnecessary personal information are never written to LocalStorage. LocalStorage is browser-specific, can be cleared by the user, is not a secure database, and should not be used as the storage layer for a real marketplace.

## Favorites and comparison

Clicking a heart toggles the stable property ID in `state.favorites`, then writes the ID array to LocalStorage and re-renders cards, the navigation badge, and the Saved Properties section. Comparison uses the same pattern but rejects duplicates and refuses a fourth property. The comparison table is generated from selected property objects and uses explicit labels such as “monthly rent” or “asking price”.

## Form validation

Contact, login, registration, and listing forms use required fields, email types, phone patterns, minimum password length, consent checkboxes, numeric minimums, and `reportValidity()`. Registration adds a custom password-match rule. The contact form identifies the selected property and ends with a toast explaining that nothing was sent. The listing form produces a local preview, supports a FileReader image preview, and marks submitted listings “User-submitted demo · not verified”.

## Demo authentication limitations

The authentication modal is interface-only. It does not call a server, create an account, hash a password, manage a session, or persist credentials. A production implementation would use a secure backend, HTTPS, server-side validation, salted password hashing or a trusted identity provider, session rotation, rate limiting, and clear privacy/consent handling.

## Property submission limitations

A submitted listing is appended to the current browser's demo state only. It is not uploaded, moderated, published, legally verified, or delivered to an agent. The optional image file is previewed locally and is not sent to a server. A production flow would require authenticated ownership, image storage, moderation, abuse protection, address privacy rules, and server-side validation.

## Security and privacy considerations

The project keeps HTML, CSS, and JavaScript separate; escapes dynamic text before injecting it into generated card and modal markup; does not expose API keys; avoids exact fictional addresses and fake agent contacts; does not claim that frontend validation is security; and avoids saving passwords. A real product would need a backend, secure authentication, database access controls, content security policy, audit logging, and privacy/legal review.

## Accessibility features

The project includes a skip link, semantic headings, labels for inputs, meaningful image alt text, visible focus styles, keyboard-friendly buttons, native `dialog` modal behavior, Escape closing, accessible status messages, confirmation copy, details/summary FAQ semantics, screen-reader-friendly count updates, touch-friendly controls, no color-only status, and `prefers-reduced-motion` support. A full production audit should still be performed with assistive technologies.

## Testing checklist

- [ ] Open the page at desktop and mobile widths; confirm there is no unintended horizontal scroll.
- [ ] Use hero search, quick search links, categories, listing chips, price/area/room filters, amenity filters, and sorting together.
- [ ] Confirm the result count, clear buttons, and empty state update correctly.
- [ ] Open details, change gallery image, favorite, compare, contact, and close with the close control and Escape.
- [ ] Save a property, refresh the browser
- [ ] Refresh after favoriting and confirm the favorite badge and Saved Properties section persist.
- [ ] Add three comparison properties; try a fourth and confirm the limit message. Clear comparison.
- [ ] Open contact from a card or details dialog; test required fields, email, phone, consent, and demo confirmation.
- [ ] Open login and registration; confirm tab switching, password visibility, password mismatch validation, and no password storage.
- [ ] Open List Your Property; test numeric validation, preview text, local image preview, and the unverified listing label.
- [ ] Toggle dark mode, refresh, and confirm the theme preference persists.
- [ ] Use keyboard focus, Escape to close dialogs, and reduced-motion settings.
- [ ] Inspect the console and network behavior; there should be no avoidable JavaScript errors.

## Known limitations

This is a frontend-only project. It has no production database, secure authentication, agent inbox, email/SMS delivery, payment process, live maps, real coordinates, live inventory, legal verification, ownership verification, moderation workflow, image upload service, or server-side validation. LocalStorage is browser-specific and can be removed at any time. Generated images are visual assets for the demo and do not prove that a property exists.

The price range controls intentionally use one numeric value at a time. The UI labels the value as either a sale total or monthly rent through the listing's pricing basis, but a production product should offer separate sale and rental filter models so users cannot accidentally compare unlike values. A production map would require valid addresses or coordinates and an approved map provider configuration.

## Future enhancements

A production version could add a secure user and agent backend, PostgreSQL/MySQL persistence, role-based access, moderation and verification states, image storage, map integration, saved searches, alerts, appointment scheduling, real contact delivery, analytics, SEO route metadata, server-side filtering, currency/unit preferences, and an audit log. Automated tests could cover reducers or pure filter functions separately from DOM rendering.

## Engineering viva questions and answers

### 1. Why use semantic HTML?
Semantic elements communicate the meaning of a page to browsers, assistive technologies, and future developers. They improve structure, accessibility, and maintainability compared with using generic `div` elements everywhere.

### 2. Why is CSS Grid useful here?
Grid is useful for two-dimensional layouts such as the category cards, listing layout, budget cards, and footer. It lets the design describe columns and gaps directly and adapt them at responsive breakpoints.

### 3. Where is Flexbox used?
Flexbox handles one-dimensional alignment such as navigation rows, button groups, card metadata, badges, footer links, and the hero statistics. Grid and Flexbox complement each other.

### 4. What is the purpose of `DEMO_PROPERTIES`?
It is the single structured data source for fictional listings. The rendering, filters, details dialog, favorites, and comparison table all use the same objects, which reduces duplicated markup and inconsistency.

### 5. How does DOM rendering work?
Functions such as `renderListings()` calculate the visible property array and assign escaped HTML to the property grid. Rendering is repeated after a state change so the visible interface always reflects the current state.

### 6. What is event delegation?
Instead of attaching a listener to every dynamically generated card button, the app listens on the Listings and Saved sections and checks which `data-*` control was clicked. This continues to work after re-rendering.

### 7. Why are arrays and objects important in this project?
Objects represent one property; arrays hold the collection, facility lists, favorite IDs, comparison IDs, and filter results. Array methods such as `filter`, `sort`, `map`, and `every` express the discovery logic clearly.

### 8. How does search work?
The selected query is lowercased and compared with a lowercased string containing each property's title, city, locality, type, description, and facilities. If the combined text includes the query, the property remains in the result set.

### 9. How do combined filters work?
Each active filter creates a boolean condition inside one `Array.filter()` callback. A property must satisfy every active condition, so listing type, price, rooms, area, furnishing, and amenities can be used together.

### 10. How does sorting work?
After filtering, the code compares two properties based on the selected sort mode. Numeric price and area use subtraction; dates are converted to `Date` values; featured sorting uses a boolean priority before the listing date.

### 11. What is LocalStorage?
LocalStorage is a browser-provided key-value store that survives page refreshes. This project stores only suitable demo state such as theme, stable IDs, preferences, and limited fictional listings. It is not a secure database.

### 12. Why use JSON with LocalStorage?
LocalStorage stores strings, while the app needs arrays and objects. `JSON.stringify()` converts a JavaScript value to a string, and `JSON.parse()` reconstructs it. The safe helper catches malformed JSON so the page does not crash.

### 13. How are rental and sale prices kept distinct?
Each property has a `basis` field with either `sale` or `monthly`. Currency formatting appends `/mo` for monthly values and the UI labels sale values as asking prices. The comparison copy also calls out this distinction.

### 14. How does the modal work?
The app uses the native HTML `dialog` element and calls `showModal()`. The dialog can be closed with its close control, a backdrop click, or Escape. Focus is remembered before opening and returned after closing.

### 15. How does form validation work?
HTML attributes such as `required`, `type="email"`, `pattern`, `min`, and `minlength` provide baseline validation. JavaScript adds the registration password-match rule and prevents the submit handler when `reportValidity()` fails.

### 16. Why should passwords not be stored in LocalStorage?
LocalStorage is accessible to scripts running in the page and is not designed for secrets. Real authentication must hash credentials on a secure server or use a trusted identity provider, with secure session handling.

### 17. What is responsive design?
Responsive design lets one interface adapt to different screen sizes. This project changes navigation, grids, filters, form columns, typography, and the comparison drawer at tablet and mobile breakpoints.

### 18. How are accessibility requirements addressed?
The project uses labels, headings, alt text, focus-visible styles, skip navigation, semantic `details`, dialog semantics, live counts, button labels, keyboard closing, contrast-aware colors, and reduced-motion rules. These are practices rather than a substitute for a full audit.

### 19. How would an API be integrated?
A production frontend could use `fetch()` to request listing data from a backend API. The app would handle loading, error, pagination, authentication, server-side validation, and response normalization instead of relying on a local constant array.

### 20. Why is a backend needed for real listings?
A backend provides durable storage, account identity, moderation, permissions, secure form delivery, verification workflows, map configuration, and server-side validation. A frontend-only page cannot reliably provide those services.

### 21. What is the purpose of `escapeHTML()`?
It replaces characters that could be interpreted as HTML with safe entities before user-controlled or dynamic text is inserted into markup. This reduces injection risk in a demo that supports user-submitted listing text.

### 22. What is the FileReader API used for?
The FileReader API reads a locally selected image as a data URL so the form can show a preview. The file is not uploaded or persisted as a server asset in this project.

### 23. How could testing be improved?
Pure functions such as filtering, price formatting, and sorting could be unit tested with a test runner. Browser tests could exercise keyboard navigation, modal focus, forms, LocalStorage recovery, and responsive layouts with Playwright.

### 24. What is progressive enhancement in this project?
The core content is present as regular HTML, while JavaScript adds richer search, rendering, dialogs, and persistence. If scripting fails, the static page and explanatory content remain understandable even though advanced interactions are unavailable.

### 25. How could SEO be improved?
A production release could add per-route metadata, canonical URLs, Open Graph cards, structured data where truthful, a sitemap, robots rules, and crawler-visible server-rendered listing pages. This demo intentionally remains a single-page frontend.

## GitHub packaging

The repository is self-contained. Open `index.html` directly for a quick check, or serve the folder with `python3 -m http.server 3000` for the most reliable browser behavior. The `assets/` folder contains local illustrations and `screenshots/` contains preview captures. No framework install or build command is required.

# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project overview

This repository is a small, static implementation of a sign-up form UI based on The Odin Project example design. The reference screenshot URL is recorded in `README.md` and the detailed implementation checklist is in `IMPLEMENTATION_PLAN.md`.

- `index.html` defines the full page structure and form markup.
- `styles.css` contains all layout and visual styling.
- `IMPLEMENTATION_PLAN.md` documents a multi-phase plan for enhancing structure, styling, validation, accessibility, and responsiveness.

There is no build system, dependency manager, or test framework configured; everything runs directly in the browser from these static files.

## Development commands

There are no project-specific scripts (no `package.json`, build tool, or test runner). Development is done by editing the static files and viewing `index.html` in a browser.

From the repository root:

- Serve the site locally with a simple HTTP server (recommended over using the `file://` protocol):

  ```bash path=null start=null
  python3 -m http.server 8000
  ```

  Then open `http://localhost:8000/index.html` in a browser.

Currently, there are no automated lint or test commands defined for this project.

If you add tooling later (e.g., npm scripts, linters, or tests), update this section with the exact commands.

## Code structure and layout

### HTML structure (`index.html`)

The page is a single HTML document with a flexbox-based three-column layout and a centered form.

Key structural elements:

- Root container: `<div class="container">` wraps the entire layout.
  - `.left-side`: a narrow black column on the left (visual framing only).
  - `.image`: center column with the background photograph and Odin logo banner.
    - `.logo-text`: overlay containing the Odin logo image and the text "ODIN".
  - `.form-container`: main content area containing the copy, form, and submit section.
  - `.right-side`: a narrow black column on the right (visual framing only).

Inside `.form-container`:

- `.intro-section`: three introductory paragraphs explaining the (fictional) service.
- `.form-section`: card-like container for the actual form.
  - `<p class="form-title">` – section heading ("Let's do this!").
  - `<form id="signup-form">` – main form element.
    - Three `.form-row` elements, each grouping two `.form-group` blocks side by side:
      - Row 1: first name, last name (text inputs).
      - Row 2: email (type `email`), phone (type `tel`).
      - Row 3: password, confirm password (type `password`).
    - Each `.form-group` contains a `<label>` and its corresponding `<input>`.
- `.submit-section`: placed after the form and associated to it via `button[type="submit"]` with `form="signup-form"`.
  - Primary "Create Account" button.
  - "Already have an account? Log in" copy with a placeholder link.

At the top of the document, a `<script src="script.js"></script>` tag is included, but there is currently no `script.js` file in the repository. Any future client-side validation or interactivity should be implemented in `script.js` (or the reference updated if a different structure is chosen).

### Styling (`styles.css`)

All presentation is handled with a single CSS file.

Global and layout rules:

- Global reset via the universal selector: removes default margin/padding and sets `box-sizing: border-box`.
- `body` sets the base font (Arial, sans-serif), full viewport height, and allows scrolling.
- `.container` is a flex container spanning full viewport height (`height: 100vh`).
- `.left-side` and `.right-side` are side rails with `flex: 0.3` and solid black backgrounds.
- `.image` is a fixed-width center column (`flex: 0 0 40%`) with:
  - Background image from Unsplash.
  - `background-size: cover` and `background-position: center`.
  - Flexbox centering for its contents, plus `position: relative` to support the overlaid logo.
- `.logo-text` is positioned within `.image` as an overlaid banner:
  - Semi-transparent black background, large typography, and horizontal layout with the Odin logo and text.

Form area styling:

- `.form-container` fills the remaining horizontal space (`flex: 1`), uses a light gray background, and is a column flex container with vertical centering and `overflow-y: scroll` to keep the layout usable on smaller viewports.
- `.intro-section` provides top copy with bold typography and vertical spacing between paragraphs.
- `.form-section` is the main card:
  - White background, padding, and subtle box shadow for elevation.
  - `.form-title` defines the heading size and spacing.
- `.form-row` is a flex container with a fixed gap to align two `.form-group` columns per row.
- `.form-group` is a column flex container that:
  - Stretches inputs to fill available width.
  - Styles labels with small, uppercase-like typography and letter spacing.
- Input states:
  - Base styles: padding, border, border-radius, and default outline removal.
  - Focus styles: highlighted border color and light box-shadow.

Submit section styling:

- `.submit-section` adds padding below the form card.
- The submit `button` uses a green background, white text, rounded corners, and hover state with a darker shade.
- The "Log in" link uses the same accent color and an underline on hover.

There are currently no explicit responsive breakpoints or media queries; behavior on small screens is governed by the base flexbox layout and `overflow-y: scroll` on `.form-container`.

### Implementation plan (`IMPLEMENTATION_PLAN.md`)

`IMPLEMENTATION_PLAN.md` is a detailed checklist for a more complete version of this project. It covers:

- Building out full semantic HTML structure and form controls.
- Progressive styling of the layout, form elements, and interactive states.
- HTML5 validation attributes and planned JavaScript-based password matching and custom validation messages.
- Responsive design for mobile, tablet, and desktop.
- Accessibility considerations (labels, ARIA attributes, keyboard navigation, screen reader support).
- Final polish, cross-browser testing, and optional performance optimizations.

Not all phases are implemented yet. Use this plan as the canonical guide when extending HTML, CSS, or eventually adding JavaScript behavior.

## Notes for future Warp agents

- If you implement client-side validation or interactivity, either create `script.js` in the repository root (to match the existing `<script src="script.js"></script>` reference) or update the HTML to point to the new script location.
- If you introduce a build system (e.g., bundler, asset pipeline) or add automated tests/linting, add the exact commands and any important workflow notes to the **Development commands** section above.

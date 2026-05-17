# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page personal portfolio site for Rhutik Chaudhari, built on the "Khanas"
static HTML template (ThemeSine) with jQuery + Bootstrap 3. There is **no build
step, no framework, no test runner, and no active linting** — `package.json` only
pulls in `bootstrap-icons`.

## Running / deploying

- Develop by opening `index.html` directly or via any static server
  (e.g. `npx serve .` or `python3 -m http.server`).
- Deployment is GitHub Pages off the `main` branch (note the CNAME-related
  commit history). There is no deploy script — pushing to `main` publishes.

## Architecture

- **`index.html`** is the entire site. All content (about text, education,
  skills, experience, portfolio items, contact info) is **hardcoded markup**.
  Editing the portfolio means editing this HTML by hand — there is no CMS or
  data file. Sections are `<section id="...">` blocks; the fixed navbar links to
  them by anchor.
- **`assets/js/custom.js`** holds all custom behavior, wrapped in a single
  jQuery `ready()`: scroll-to-top button, smooth-scroll spy nav, skill
  progress-bar fill (triggered on scroll via `jquery.appear`), Owl carousel,
  and the welcome hero animation. It assumes the vendor scripts in
  `index.html` (jQuery → bootstrap → bootsnav → sticky → progressbar → appear →
  owl carousel) are loaded **before** it, in that order. Reordering or removing
  those `<script>` tags will silently break features.
- **`assets/css/`** is template CSS. Site-specific overrides go in `style.css`
  and `responsive.css`; the rest (`bootstrap.min.css`, `animate.css`,
  `owl.*`, `bootsnav.css`, `flaticon.css`, `font-awesome.min.css`) are vendor
  files — avoid editing them.
- Resume PDF lives at `assets/download/Rhutik_Resume.pdf` and is linked from the
  hero "download resume" button.

## Known gotchas

- `index.html` links bootstrap-icons from
  `./assets/node_modules/bootstrap-icons/...`, but the npm `node_modules` is
  actually at the **repo root** (`./node_modules`), and `.gitignore` ignores
  `/assets/node_modules`. As written, the bootstrap-icons stylesheet 404s and
  the `bi bi-*` icons in the "profiles" section won't render. Fix the path to
  `./node_modules/bootstrap-icons/font/bootstrap-icons.min.css` (or relocate the
  package) rather than working around it.
- The contact form is intentionally non-functional (it has no backend); the
  page itself tells visitors to use email/phone. Don't wire up form-submit
  logic unless explicitly asked.
- Icons come from two different sets: Font Awesome 4 (`fa fa-*`) in most
  sections and Bootstrap Icons (`bi bi-*`) only in the "profiles" section.

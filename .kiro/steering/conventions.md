# Project Conventions

## When to Apply
Always apply when editing any file in this repository.

## Rules
- Site is static HTML/CSS/JS — no build tools, no frameworks
- All JavaScript is vanilla (no jQuery, no React, no bundlers)
- CSS uses custom properties (variables) defined in :root
- Bilingual support: all user-facing text must have EN and ES translations
- Member photos go in `assets/members/` as JPG
- Badge images go in `assets/badges/` as PNG
- Config values (API URLs, Cognito IDs) live in `config.js` — never hardcode in HTML
- Keep the site lightweight — no external JS libraries unless absolutely necessary
- Member cards use a consistent HTML structure with `card-number` attribute for ordering

## Cursor Cloud specific instructions

This is a static HTML/CSS/JS restaurant website (Part & Parcel). There is no build system, package manager, or backend.

### Running the dev server

Serve the site with Python's built-in HTTP server from the workspace root:

```
python3 -m http.server 8000
```

The site is then available at `http://localhost:8000/`. All 4 pages (`index.html`, `menus.html`, `about.html`, `visit.html`) plus assets are served directly.

### Key notes

- **No build step, no dependencies to install.** The site is pure HTML/CSS/JS with CDN-loaded libraries (GSAP, Lenis, Google Fonts).
- **No linter or test framework is configured.** There are no `package.json`, `eslint`, or test files.
- **Page transitions** use a CSS wash overlay with JS-driven delays (~500ms) on internal link clicks. If navigation seems slow during testing, this is by design.
- **GSAP animations and Lenis smooth scroll** are loaded from CDNs and require internet access to function fully.
- Image assets (`.png`, `.webp`) are committed to the repo root alongside HTML files.

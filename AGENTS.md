# AGENTS.md

## Project

Static single-page portfolio (Indonesian copy, `lang="id"`). No build step, package manager, tests, lint, or CI. Entry point `index.html`; all styling in `css/style.css`; behavior in `js/script.js`.

## Run and verify

- Open `index.html` directly in a browser (Laragon also serves this folder). Nothing to install or build.
- Internet is required at runtime: Tailwind Play CDN and GSAP 3.12.5 + ScrollTrigger come from CDNs.
- Verify manually at desktop and mobile (~320px), plus keyboard focus and reduced-motion, as required by `README.md`.
- Do not add tooling or dependencies unless the user explicitly asks.

## Architecture and quirks

- Styling is mostly hand-written CSS with `block__element` and `is-*` state classes. Tailwind is only loaded via an inline config in `index.html` (custom `paper`/`ink`/`moss`/`clay` colors); do not convert existing CSS to utility classes.
- Design tokens live in `:root` in `css/style.css` and are duplicated in the Tailwind config and `<meta name="theme-color">`. They are currently not identical (`--paper` is `#ffbf00`); confirm intent before "fixing" the palette.
- `js/script.js` handles the loader intro, ScrollTrigger reveals, scroll spy, and copy-email. GSAP is optional by design: keep the `typeof gsap === "undefined"` / ScrollTrigger guards so the page degrades without CDNs.
- Some JS selectors do not match the current HTML (JS targets `.site-header-wrap`, `#copyEmailBtn`, `#copyToast`; HTML uses `.site-header` and has no copy-email markup). Features no-op safely, so do not assume a feature is wired just because JS exists.
- Scroll spy automatically covers every `section[id]` and `footer[id]` matched to `.main-nav a[href^="#"]`. Adding a section requires a matching nav link and `id`.
- Respect `prefers-reduced-motion`: there is a global CSS override near the end of `style.css` and a JS early-return. New animations must degrade there.
- Do not invent portfolio content or personal data. Current copy is placeholder/inconsistent (Fahdin vs Fajar, two different emails, "Sukabumi, Amerika", © 2025). Get approved content from the facilitator per `README.md`.

## Git and contribution

- `github-guide-global.md` is the authoritative Git SOP; `semantic-versioning-guide.md` defines SemVer and branch naming. Read both before any branch, commit, or PR work.
- Mandatory session setup: ask the user for workflow style (1/2/3), target version/base branch, optional issue number, and PR format before creating branches or PRs. Do not infer the style from the repo (remote has `develop/1.0.0`, `master`, and `main`).
- One task = one PR. After opening a single PR, stop; do not start the next branch/commit/PR without explicit user instruction.
- Never run the destructive/force Git commands listed in the guide. Never touch stashes.
- Discuss new dependencies or design-direction changes first (README rule).

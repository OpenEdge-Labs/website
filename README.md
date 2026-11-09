<!-- SPDX-License-Identifier: Apache-2.0 -->
<!-- Copyright (c) OpenEdge Labs -->
# OpenEdge Labs website

Source of <https://openelabs.online>, the home of the OpenEdge Labs community and its projects, [wEdge](https://github.com/OpenEdge-Labs/wedge) and [APIEdge](https://github.com/OpenEdge-Labs/APIEdge).

Plain HTML and CSS. No build step, no scripts, no cookies, no analytics, no third-party requests; every asset is in this repository. Licence: Apache-2.0 (see `LICENSE`).

## Layout

| Path | Purpose |
|---|---|
| `index.html`, `*/index.html` | pages (one folder per page) |
| `404.html` | not-found page |
| `assets/` | stylesheet, OpenEdge Labs mark, wEdge icon |
| `_headers` | security response headers (Cloudflare Pages) |
| `robots.txt`, `sitemap.xml`, `.well-known/security.txt` | crawler and security contact files |

The pages share the same header and footer, which are copied into each file. When changing the navigation, edit every page.

## Preview locally

```sh
python -m http.server 8000
```

then open <http://localhost:8000/>. This serves the files but not the `_headers` file, so the security headers are not shown locally. Root-relative links (`/assets/...`) need the server to run from the repository root.

## Facts and upkeep

Project facts (features, versions, download names, supported versions) are taken from each project's README, releases and security policy. On every project release, update the versions, download links and news here. Each project page states the date its facts were last checked.

## Reporting a problem

Use <https://github.com/OpenEdge-Labs/website/security/advisories/new> for security problems and the issue tracker for everything else.

## Checks (measured 2026-11-10)

CI (`.github/workflows/checks.yml`) runs the first two on every push.

| Check | Tool | Result |
|---|---|---|
| HTML, CSS and SVG validation | Nu validator, `ghcr.io/validator/validator:latest` (`vnu`) | 0 errors, 0 warnings on all pages, `site.css` and the SVGs. A deliberately broken file is reported, so the check does detect errors. |
| Links and fragments | lychee (Docker), local files plus external links | all links resolve except one: GitHub answered HTTP 500 for the unauthenticated download of `wedge-0.2.0-x86_64-unknown-linux-musl.tar.gz` (the same file downloads fine with `gh release download` and matches `SHA256SUMS`). `openelabs.*` URLs are skipped until the domains are live. |
| No inline script or style, no third-party requests | grep in CI | none found |
| Lighthouse 12 (local Chrome, no `_headers`) | Accessibility, Best Practices, SEO, mobile and desktop presets, 8 pages | 100 / 100 / 100 on every page run |
| Manual look, light and dark theme | Chrome headless screenshots | dark and light render correctly; at 360 px wide the layout wraps without page-wide horizontal scrolling (wide tables scroll inside their own box); desktop 1280 px checked |

Not yet checked: the response headers (`_headers` is only applied by Cloudflare Pages), HTTP Observatory and SSL Labs. These belong to the deployment step.

<!-- SPDX-License-Identifier: Apache-2.0 -->
<!-- Copyright (c) OpenEdge Labs -->
# OpenEdge Labs website

Source of <https://openelabs.com>, the home of the OpenEdge Labs community and its projects, [wEdge](https://github.com/OpenEdge-Labs/wedge) and [APIEdge](https://github.com/OpenEdge-Labs/APIEdge).

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

<p align="center">
  <img src="https://img.shields.io/badge/Chrome%20extension-MV3-4285F4" alt="Chrome extension MV3">
  <img src="https://img.shields.io/badge/JavaScript-plain-F7DF1E" alt="JavaScript">
  <img src="https://img.shields.io/badge/status-private-lightgrey" alt="status: private">
</p>

# AISIS Scraper

**A Chrome extension that pulls your own AISIS records into a clean dashboard you can export — for Ateneo students tired of clicking through AISIS page by page.**

AISIS (Ateneo Integrated Student Information System) spreads a student's grades, schedule, curriculum and enrollment across a dozen slow, separate pages. This extension logs in with your own credentials, visits the pages you pick, and gathers them in one place.

- **Dashboard** — overview, grades, schedule, student info and program of study in one window.
- **Scraper popup** — choose which pages to fetch, watch progress live, read a colour-coded log.
- **Export** — JSON, CSV, HTML snapshots, a HAR file of the requests, and the log.
- **Local only** — data stays in the browser; nothing is sent to another server.

The repo also carries notes and a patched TypeScript module (`server-scraper-fixes/`) for people running a server-side AISIS scraper that fails with "invalid HTTP header parsed".

## Quick start

1. Open `chrome://extensions/` and switch on **Developer mode**.
2. Click **Load unpacked** and pick the `chrome-extension/` folder.
3. Click the extension icon, enter your AISIS credentials, choose pages, and run.

No build step and no dependencies — the extension is plain HTML and JavaScript.

## How it works

```
popup (pick pages) ──▶ background.js (service worker)
                         login + CSRF token ──▶ aisis.ateneo.edu
                         fetch each page, retry on failure
                         parse HTML ──▶ chrome.storage ──▶ dashboard / export
```

Schedule of Classes, Official Curriculum and View Grades are parsed into structured rows; the other pages are kept as raw HTML.

## Links

- [docs/internals.md](docs/internals.md) — the full previous README: file list, supported-page tables, AISIS URLs, design spec, server-fix notes
- [docs/QUICK_START.md](docs/QUICK_START.md), [docs/CHANGELOG.md](docs/CHANGELOG.md)
- [docs/SCRAPING_CODE.md](docs/SCRAPING_CODE.md) and [docs/PARSING_LOGIC.md](docs/PARSING_LOGIC.md) — request and parsing internals
- [server-scraper-fixes/scraper_analysis.md](server-scraper-fixes/scraper_analysis.md)

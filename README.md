# Everything I Wish I Knew Before Shipping a PWA

A production-grade field guide to Service Workers , covering common failure modes, caching traps, browser quirks, and update challenges. Every claim is labelled as spec fact, browser-observed behaviour, or field experience.

## Contents

| # | Section |
|---|---------|
| 01 | Mental Model & Lifecycle |
| 02 | Real Production Failures |
| 03 | Caching Strategy Deep Dive |
| 04 | Update Mechanism — Precisely |
| 05 | Storage & Limits Reality |
| 06 | Security Risks |
| 07 | Debugging & Observability |
| 08 | Cross-Browser Differences |
| 09 | Advanced Patterns |
| 10 | Practical Tips |

## How Claims Are Labelled

Not all production engineering claims carry the same weight. This guide uses three labels:

- **`SPEC`** — directly traceable to the WHATWG Service Worker spec, W3C, or IETF. True by definition across compliant engines.
- **`BROWSER`** — observed and version-confirmed in specific browsers. May differ in other engines or future releases.
- **`FIELD`** — real production failure patterns. Widely reproduced but not a guaranteed rule; context matters.

## Verified Against

- Chrome 124
- Firefox 126
- Safari 17.4
- iOS 17

Last reviewed: **March 2026**

## Usage

Open `index.html` in any modern browser. No build step or dependencies required — all fonts are loaded from Google Fonts via CDN.

## Key Failures Documented

- **The Long-Lived Broken Build** — users stuck on a broken deploy because the SW precached it
- **The Offline Loop** — stale API data served after connectivity returns
- **The CDN + SW Double-Cache Conflict** — two independent caching layers with no coordination
- **Safari iOS Silent Storage Eviction** — origin storage wiped without warning under storage pressure
- **The `skipWaiting()` Version Mismatch Crash** — white screen from lazy-loaded chunk 404s after a forced SW takeover
- **OAuth Callback Interception** — hash fragments stripped by the SW, stale HTML served to auth callbacks

## Notable Topics

- Why service workers are programmable proxies, not caches
- The precise mechanics of the "24-hour rule" (two separate mechanisms, commonly conflated)
- When every caching strategy (`Cache First`, `Network First`, `SWR`, etc.) will cause a production incident
- Safari iOS storage isolation and PWA quirks
- A safe, user-confirmed update pattern with `skipWaiting()` + `controllerchange`
- Production logging from the SW thread
- Navigation preload, Background Sync, and streaming response patterns
- Honest assessment of Workbox — what it solves and where it becomes a liability

---

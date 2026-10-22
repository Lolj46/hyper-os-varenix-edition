# Smoke-test report · 0.1.0

Date: 2026-10-22

## Passed

- `node --check app.js` and `node --check sw.js` completed without syntax errors.
- The local Python HTTP server returned HTTP 200 for `index.html`, `styles.css`, `app.js`, `manifest.webmanifest`, `sw.js`, and this README.
- Chromium runtime check: the lock screen and home screen rendered; 27 application screens opened with their expected title and content container, without JavaScript exceptions in the exercised UI paths.
- Mobile viewport at 430 × 932 CSS pixels: home screen rendered 16 grid items plus a four-app dock; no horizontal overflow was detected.
- Unlock, two-page home layout, synthetic touch swipes between pages, and swipe-up return from an app were checked.
- The control centre rendered 13 quick tiles. Wi-Fi state toggled; tile editor hid a tile and it disappeared from the control centre; dark theme toggle updated the root and document classes.
- Notification removal, note creation/editing, timer activity in HyperIsland and its completion notification, calculator `7 + 8 = 15`, and calendar event creation were checked.
- Browser UI accepted `https://example.com`, updated the iframe URL, added a bookmark, created a second tab and closed a tab.

## Not fully verified in this environment

- The browser test environment intercepted direct navigation to local URLs with a managed-browser policy. Therefore service-worker activation and real-origin `localStorage`/IndexedDB persistence across an actual browser reload were not independently end-to-end verified, even though the local server served the files successfully and the storage code is implemented.
- Real external website rendering depends on internet access and the destination site's iframe/CSP rules; the UI provides an “open separately” link and does not bypass those protections.
- Camera, microphone, user-media import/playback and live Open-Meteo requests depend on user permissions, hardware, browser origin security, and network availability. They were not end-to-end tested with physical hardware or an open network.
- Native Android controls, cellular radios, SMS, phone calls, APK installation, sensor readings, screen recording and health tracking are simulations, not real device integrations.

This report records only the checks above. It does not claim every feature or device-dependent path has been exhaustively tested.

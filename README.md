# HyperOS 4 · Interactive web simulation

A standalone mobile-first simulation inspired by the publicly described visual language of Xiaomi HyperOS 4. It is **not** Xiaomi software, not a device ROM, and does not have operating-system privileges on Android.

## Run it

Requirements: a modern browser. No npm packages, build step, API key or backend are required.

### On a computer

```bash
cd hyperos4-sim
python3 -m http.server 4173
```

Open <http://localhost:4173>. On Windows, `py -m http.server 4173` may be used instead.

### On an Android phone

Put the folder on a computer or Android device that can run Python, start the same server, and open the server URL in the phone browser. If serving from another device, use that device's LAN IP instead of `localhost` and ensure both are on the same Wi-Fi network. The browser needs to be allowed to access the server. Microphone/camera access normally requires `localhost` or HTTPS, so those hardware features may be unavailable when using a plain LAN HTTP address.

Opening `index.html` directly may work for the basic UI, but an HTTP origin is recommended for service-worker/offline support and browser media permissions.

## Controls

- Lock screen: tap **Разблокировать** or swipe up.
- Home pages: swipe left/right; long-press an app icon for its context menu.
- From an app: swipe up from the bottom edge or tap the home indicator.
- Control center: choose **Изменить плитки** to hide or restore quick toggles.
- Control center: swipe down from the right side of the status bar, or tap the right status area.
- Notifications: swipe down from the left side of the status bar, or tap the left status area.
- HyperIsland: tap the island to expand active tasks; tap the task to open the relevant app.
- Home indicator: tap to return home.

## App catalogue

27 simulation apps are included: Phone, Contacts, Messages, Browser, Camera, Gallery, Music, Video, Settings, Weather, Calendar, Clock, Calculator, Notes, Recorder, Files, Downloads, Themes, Security, Recent apps, Search, App Store, Mail, Health, Games, Help, and System Update.

Data is persisted locally in the browser. IndexedDB stores imported media, and localStorage stores the UI state. Clearing browser site data can remove this saved content. The browser may not persist large media files if storage is exhausted or browser policy clears site data.

## Real vs simulated

- Browser navigation opens external sites in a new tab/window rather than bypassing site iframe restrictions. Browser security policies remain in force.
- The Weather app requests public forecast data from Open-Meteo without an API key; forecast availability depends on network access.
- Camera and microphone features request permission from the browser and may be unavailable without HTTPS/localhost or hardware permission. Demo mode is provided where appropriate.
- Phone calls, SMS, app installs, security checks, screen recording and health sensors are simulated. They do not call numbers, deliver SMS, install APKs, inspect the Android device, or read real sensors.
- Wi-Fi/Bluetooth/cellular/battery indicators and most quick toggles are internal simulation state, not actual Android radio controls.
- An offline shell is cached through a service worker after the app is first visited on a supported HTTP(S) origin. Real websites and current weather need network connectivity.

## Reference notes

Visual decisions use publicly available descriptions of HyperOS 4 on the official Xiaomi OS site and Xiaomi Community. This prototype does not claim every simulated screen or feature matches an official firmware screenshot. Items not independently confirmed in official reference materials are visual/behavioral approximations. The Xiaomi wordmark and proprietary assets are not included.

## Smoke checks

The JavaScript is plain browser JavaScript, so `node --check app.js` can be used as a quick syntax check. Start the local server and open the page in a Chromium-based browser to verify runtime behavior. Browser policy-dependent features (camera, microphone, external websites, weather) must be tested in the user's browser/network and with explicit permissions.

See [`TEST_REPORT.md`](./TEST_REPORT.md) for the checks that were run and the paths that remain dependent on browser/device permissions or could not be end-to-end verified in the test environment.

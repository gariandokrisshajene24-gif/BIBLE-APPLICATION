# WordPath — deployment-ready PWA starter

This folder contains your existing WordPath app with the PWA files added.

## Files
- `index.html`, `styles.css`, `app.js`: your app, updated for PWA install and safer local-storage writes.
- `manifest.webmanifest`: app name, display mode, colors, and icon declarations.
- `service-worker.js`: caches the app shell so the interface can open offline after its first successful load.
- `icons/`: generated WordPath app icons in the sizes needed by common browsers.

## Run locally
Do not test PWA installation by double-clicking `index.html` (`file://`). Use a local HTTP server instead. If Python is installed, open a terminal in this folder and run:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`. For install testing, use Chrome/Edge desktop or Chrome on Android. Check DevTools → Application → Manifest and Service Workers.

## Deploy
1. Keep this folder structure intact.
2. Upload the folder contents to a static host such as Netlify, Vercel, or GitHub Pages. For a simple Netlify deployment, drag the *contents* of this folder into Netlify Drop, or deploy this folder from a Git repository.
3. Use the HTTPS URL the host gives you.
4. Open the deployed URL and verify the app, icons, manifest, and service worker.
5. On Android/desktop Chromium, use the browser's Install app option. On iPhone/iPad, open the site in Safari, tap Share, then Add to Home Screen. Browser UI varies by device.

## Important behavior and limits
- Bookmarks, journal entries, reading-plan progress, theme preference, and quiz best score use `localStorage`. They remain in the same browser profile on the same device and are not synced to other devices. Clearing browser/site data can erase them. They do not automatically transfer from a local `file://` copy to the deployed HTTPS origin.
- The service worker caches the app shell only. Bible chapter text still comes from external sources in `app.js`, so reading a chapter for the first time or loading uncached chapters still requires internet. This is not a complete offline Bible download.
- The service worker deliberately does not cache external Bible API responses or private journal data.
- Before public release, confirm that every Bible translation and external API you use permits your intended use and attribution. Do not place private API secrets in browser JavaScript.
- An installable PWA is not automatically a Play Store/App Store listing. Store distribution requires a separate packaging and store submission process.

## Updating the cache
When you make a release with major app-shell changes, change `wordpath-shell-v1` in `service-worker.js` to `wordpath-shell-v2` (increment the version) so the browser replaces the cached shell.

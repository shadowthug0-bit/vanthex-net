# VANTHEX NET — Prototype 0.2

## What is included
- Responsive installable web app (PWA).
- Offline app shell and local saved entries.
- Search, save, remove, and connection instructions.
- Optional Firebase Firestore shared directory.
- Firestore rules that expose only approved listings and keep submissions pending until reviewed.
- Android packaging guidance.

## Important limits
This app is a directory only. It does not generate internet, reveal Wi-Fi passwords, bypass captive portals/payment, scan nearby networks, or silently connect to Wi-Fi. Users must use Android Wi-Fi settings and have permission.

## 1. Test locally
For service workers and installation, host the folder on HTTPS. Opening index.html directly as a file will show the interface but offline/PWA features will not fully work.

## 2. Publish the PWA
Upload the contents of this folder to an HTTPS static host such as GitHub Pages, Netlify, or Cloudflare Pages. Keep all files in the same published folder. Test the public HTTPS URL on Android Chrome.

## 3. Enable the shared directory (Firebase)
1. Create a Firebase project using your own Google account.
2. Add a Web App in Project settings and copy its Firebase web configuration.
3. Replace the placeholders in `firebase-config.js`. This config is designed to be public; never put private service-account keys in the app.
4. Create a Cloud Firestore database.
5. Open Firestore Rules and publish the contents of `firestore.rules`.
6. In Firestore Data, open the `hotspots` collection. Review submissions and change `status` from `pending` to `approved` only after checking that the place exists and the owner permits public listing.
7. The app reads approved entries and sends new entries as pending.

Firebase may require billing/account verification depending on current Google policies and usage. Do not enable paid services unless an adult account owner understands the costs. Set budget alerts if billing is enabled.

## 4. Install on Android
After publishing on HTTPS:
1. Open the website in Chrome on Android.
2. Open Chrome's menu and choose **Install app** or **Add to Home screen** (wording varies).
3. Confirm. This installs the PWA on the phone.

This is an installable app experience, but it is not yet a signed standalone APK. For an APK, use a trusted Android packaging workflow such as PWABuilder after the HTTPS site and manifest are live. APK signing requires a signing key; keep that key private and backed up. Never share it in chat or upload it to an unknown site.

## 5. Before public launch
- Ask venue owners for explicit permission before listing their Wi-Fi.
- Do not collect or publish passwords.
- Avoid exact home addresses and personal contact details.
- Review submissions before approving them.
- Add a report/removal process and a privacy policy before inviting the public.
- Test on more than one Android device and with slow/offline connections.

## Files
- `index.html` — app interface and logic
- `manifest.webmanifest` — install metadata
- `sw.js` — offline app shell
- `icon.svg` — app icon
- `firebase-config.js` — optional public Firebase web config placeholders
- `firestore.rules` — shared directory security rules

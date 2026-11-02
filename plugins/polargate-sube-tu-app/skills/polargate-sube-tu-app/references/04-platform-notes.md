# Platform Notes

Lovable-to-mobile gotchas and CI/CD baseline. Read when working on a Lovable-generated codebase, or setting up release pipelines for a Capacitor app.

---

## Lovable-to-mobile gotchas (10 recurring issues)

Lovable generates fast, but ships a few patterns that need cleanup before App Store submission. Run this checklist on any Lovable project before TestFlight.

### 1. Bundle ID defaults to `app.lovable.<project-uuid>`

This will work for TestFlight uploads but is a red flag for reviewers and a nightmare to migrate later. Change to your branded FQDN (e.g., `com.yourcompany.yourapp`) BEFORE the first build that you'll ever submit. Bundle ID changes after first submission are doable but messy.

### 2. Duplicate native wrappers (`src/lib/native.ts` vs `src/lib/nativePlugins.ts`)

Lovable sometimes scaffolds two coexisting wrapper files. Pick ONE canonical wrapper path (`src/lib/capacitor/*` is a clean convention) and delete or delegate the other. Otherwise plugin imports drift across the codebase.

### 3. Scattered plugin imports in UI components

`import { Camera } from '@capacitor/camera'` inside a JSX component is debt. Refactor each plugin into a service module under `src/lib/capacitor/` and expose a typed hook (`useCamera()`, `useShare()`, etc.). This is mandatory before submission; otherwise testing native fallbacks becomes impossible.

### 4. `public/sw.js` minimal scaffold

Lovable's default service worker is barebones. For App Store native-feel requirements (offline behavior counted toward Guideline 4.2), upgrade to:
- Network-first for HTML.
- Stale-while-revalidate for API JSON.
- Cache-first for images and fonts.
- Versioned cache name so old caches purge on deploy.

### 5. Native folders need re-generation after Bundle ID change

After changing `appId` in `capacitor.config.ts`:
```bash
rm -rf ios android
npx cap add ios
npx cap add android
npx cap sync
```
You'll lose any manual Info.plist or AndroidManifest changes, so commit those changes separately or apply via Capacitor's config plugins.

### 6. Placeholder `TEAM_ID` and `SHA256` in `.well-known`

If `public/.well-known/apple-app-site-association` or `assetlinks.json` exists in Lovable scaffolds, they often have placeholder values like `TEAM_ID.com.example.app` or `AA:BB:...`. These MUST be filled with the real Team ID (Apple Developer → Membership) and SHA-256 (Play Console → App Integrity) before Universal Links / App Links work.

### 7. Generic PWA icons in `manifest.json`

`public/manifest.json` ships with the Lovable default icon. Replace with branded icons at all required sizes:
- 192x192, 512x512 (PWA minimum)
- iOS: 1024x1024 master, generated to all sizes via `npx capacitor-assets generate`.
- Android: 512x512 + adaptive layers (foreground PNG + monochrome PNG for Android 13+ themed icons).

### 8. `window.open` for external links

Lovable's React patterns sometimes use `window.open(url, '_blank')` for external navigation. In a Capacitor WebView this either fails silently or opens a broken in-WebView tab. Replace with:
```ts
import { Browser } from '@capacitor/browser';
await Browser.open({ url, presentationStyle: 'popover' });
```
This opens SafariViewController on iOS and Chrome Custom Tabs on Android, the only approved pattern for external URLs.

### 9. `localStorage` for everything

`localStorage` is synchronous, limited to ~5-10MB, and gets cleared by iOS aggressively when storage pressure rises. For anything beyond user preferences:
- React Query (or TanStack Query) with `persistQueryClient` + IndexedDB persister.
- `idb-keyval` for simple key-value at scale.
- Supabase / SQLite local mirror for offline-first apps.

### 10. Keyboard not handled

Lovable apps default to fixed-position bottom buttons that get hidden by the iOS keyboard. Wire `@capacitor/keyboard`:

```ts
import { Keyboard } from '@capacitor/keyboard';

useEffect(() => {
  const showSub = Keyboard.addListener('keyboardWillShow', (info) => {
    document.body.style.setProperty('--keyboard-height', `${info.keyboardHeight}px`);
  });
  const hideSub = Keyboard.addListener('keyboardWillHide', () => {
    document.body.style.setProperty('--keyboard-height', '0px');
  });
  return () => {
    showSub.then(s => s.remove());
    hideSub.then(s => s.remove());
  };
}, []);
```

Then in CSS: `padding-bottom: calc(env(safe-area-inset-bottom) + var(--keyboard-height, 0px))` on the bottom container.

---

## CI/CD baseline (recommended pipeline)

The goal: every release tag produces a TestFlight build and an Internal Testing AAB without manual macOS labor.

### Recommended split

```
GitHub Actions
├── PR pipeline (every push)
│   ├── lint (eslint + prettier check)
│   ├── typecheck (tsc --noEmit)
│   ├── test (unit + integration)
│   └── build verification (vite build)
│
├── Main branch (on merge)
│   ├── npm run build
│   └── npx cap sync
│
└── Release pipeline (on `v*` tag)
    ├── iOS:
    │   ├── Fastlane: match (certs from private repo) + gym (build IPA) + pilot (TestFlight)
    │   └── Or: EAS-equivalent for Capacitor (e.g., Ionic Appflow, Capgo)
    └── Android:
        ├── Gradle: ./gradlew bundleRelease
        ├── Sign with Play App Signing upload key
        └── Upload to Internal Testing via Google Play Developer API or gradle-play-publisher
```

### Choosing the build host

| Option | When to pick |
|---|---|
| GitHub Actions macOS runner + Fastlane | Standard, free quota covers ~2-3 builds/day. Best fit for most teams. |
| Self-hosted macOS runner | High build frequency, custom signing, or sensitive corporate setup. |
| Ionic Appflow | Solo developer or small team, willing to pay for managed cloud builds. Free tier exists. |
| Capgo | Capacitor-specific cloud builds + live updates. Free for small apps. |
| Bitrise / Codemagic | Mobile-CI specialists, generous free tiers, polished mobile-specific tooling. |

### Secrets to store in CI

- `APPLE_API_KEY` (App Store Connect API key, .p8 file as base64)
- `APPLE_API_KEY_ID` + `APPLE_API_ISSUER_ID`
- `APPLE_TEAM_ID`
- `MATCH_PASSWORD` (if using Fastlane Match)
- `MATCH_GIT_PRIVATE_KEY` (deploy key for the certs repo)
- `GOOGLE_PLAY_SERVICE_ACCOUNT_JSON` (Play Console service account)
- `ANDROID_KEYSTORE_BASE64` + `ANDROID_KEYSTORE_PASSWORD` + `ANDROID_KEY_ALIAS` + `ANDROID_KEY_PASSWORD`

### Version bumping

Tie `versionName` (Android) and `CFBundleShortVersionString` (iOS) to the git tag. `versionCode` and `CFBundleVersion` should auto-increment on every build (e.g., from the run number).

A clean pattern:
```bash
# In a release script
TAG_VERSION=$(git describe --tags --abbrev=0 | sed 's/^v//')
BUILD_NUMBER=${GITHUB_RUN_NUMBER:-1}

# iOS: agvtool new-marketing-version $TAG_VERSION
# iOS: agvtool new-version -all $BUILD_NUMBER
# Android: edit android/app/build.gradle, versionName "$TAG_VERSION", versionCode $BUILD_NUMBER
```

### Smoke gate before letting CI auto-publish

Don't let CI push to production without a human gate. Recommended:

```
Tag push → CI builds → uploads to TestFlight + Internal Testing → Slack/email notification
                                                                         ↓
                                                            Human runs 30-min smoke test
                                                                         ↓
                                                  Promote to production via store UI (manual)
```

Automatic production rollouts are tempting but every rejection cycle that surfaces in production-only costs the team 5 to 10 days of recovery. Keep the human gate.

### Live updates (post-launch)

For OTA updates of the web bundle (CSS/JS changes without store re-review):
- **Capgo** (Capacitor-specific, free tier)
- **AppFlow Live Updates** (Ionic)
- **Self-hosted**: Capacitor's `@capacitor/live-updates` plugin pointing at a CDN

Rules:
- Live updates are for JS/CSS/HTML only. Native code or permission changes still require store re-submission.
- Apple allows JS-only updates that don't change app functionality fundamentally. Be conservative; if the update adds a new permission flow, ship through the store.
- Always keep a kill-switch flag so you can disable a bad live update without forcing users to wait for the next OTA.

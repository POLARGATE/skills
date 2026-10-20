# Production Templates

Paste-ready code for Capacitor + iOS + Android + auth + push + account deletion. Adjust strings, IDs, and colors per app. Every template here is platform-generic and not tied to any vertical.

---

## 1. `capacitor.config.ts` baseline

```ts
import type { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.company.app', // FQDN reverse, lowercase, no underscores, no hyphens at boundaries
  appName: 'AppName',
  webDir: 'dist',
  // NEVER ship with server.url pointing at dev. Comment out before any production build.
  // server: { url: 'http://192.168.X.X:8080', cleartext: true },
  ios: {
    contentInset: 'always',
    limitsNavigationsToAppBoundDomains: false,
    backgroundColor: '#0a0a0a', // match your splash + first paint
  },
  android: {
    backgroundColor: '#0a0a0a',
    allowMixedContent: false,
    captureInput: true,
    webContentsDebuggingEnabled: false, // MUST be false in production
  },
  plugins: {
    SplashScreen: {
      launchShowDuration: 1500,
      launchAutoHide: true,
      backgroundColor: '#0a0a0a',
      androidScaleType: 'CENTER_CROP',
      splashFullScreen: true,
      splashImmersive: true,
    },
    StatusBar: {
      style: 'DARK', // or 'LIGHT' based on first-paint background
      backgroundColor: '#0a0a0a',
      overlaysWebView: false,
    },
    Keyboard: {
      resize: 'body',
      style: 'DARK',
      resizeOnFullScreen: true,
    },
    App: { launchUrl: '' },
  },
};

export default config;
```

---

## 2. `PrivacyInfo.xcprivacy` (iOS, mandatory since May 2024 for flagged APIs)

Path: `ios/App/App/PrivacyInfo.xcprivacy`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>NSPrivacyTracking</key>
  <false/>
  <key>NSPrivacyTrackingDomains</key>
  <array/>
  <key>NSPrivacyCollectedDataTypes</key>
  <array>
    <!-- Add one dict per data type collected. See Apple's data types reference. -->
  </array>
  <key>NSPrivacyAccessedAPITypes</key>
  <array>
    <dict>
      <key>NSPrivacyAccessedAPIType</key>
      <string>NSPrivacyAccessedAPICategoryUserDefaults</string>
      <key>NSPrivacyAccessedAPITypeReasons</key>
      <array><string>CA92.1</string></array>
    </dict>
    <dict>
      <key>NSPrivacyAccessedAPIType</key>
      <string>NSPrivacyAccessedAPICategoryFileTimestamp</string>
      <key>NSPrivacyAccessedAPITypeReasons</key>
      <array><string>C617.1</string></array>
    </dict>
    <!-- Add entries for any other required-reason API you (or your SDKs) use. -->
  </array>
</dict>
</plist>
```

Reason codes catalog: developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api

Privacy Nutrition Labels in App Store Connect MUST match this file + actual runtime behavior. Mismatches are auto-flagged.

---

## 3. Universal Links: `public/.well-known/apple-app-site-association`

No extension. MIME `application/json`. Served at the apex domain over HTTPS, no redirects.

```json
{
  "applinks": {
    "details": [
      {
        "appIDs": ["TEAM_ID.com.company.app"],
        "components": [
          { "/": "/path/*" }
        ]
      }
    ]
  },
  "webcredentials": { "apps": ["TEAM_ID.com.company.app"] }
}
```

`TEAM_ID` is found in Apple Developer → Membership.

---

## 4. App Links: `public/.well-known/assetlinks.json`

```json
[{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "com.company.app",
    "sha256_cert_fingerprints": ["AA:BB:CC:..."]
  }
}]
```

SHA-256 from Play Console → App Integrity → App Signing key certificate (after enrolling in Play App Signing).

---

## 5. Vercel hosting for `.well-known` (most teams miss this)

`vercel.json`:

```json
{
  "headers": [
    {
      "source": "/.well-known/apple-app-site-association",
      "headers": [
        { "key": "Content-Type", "value": "application/json" },
        { "key": "Cache-Control", "value": "public, max-age=3600" }
      ]
    },
    {
      "source": "/.well-known/assetlinks.json",
      "headers": [
        { "key": "Content-Type", "value": "application/json" }
      ]
    }
  ]
}
```

Verify:
```bash
curl -I https://yoursite.com/.well-known/apple-app-site-association
# Expect: 200, Content-Type: application/json, NO redirect (no 301/302).
```

If you're on Netlify, equivalent goes in `_headers`. If Cloudflare Pages, in `_headers` too.

---

## 6. Supabase auth deep-link setup

Dashboard → Authentication → URL Configuration:

```
Site URL: https://yoursite.com
Redirect URLs:
  https://yoursite.com/auth/callback
  com.company.app://auth/callback
```

In `capacitor.config.ts`:

```ts
plugins: { App: { launchUrl: 'com.company.app://' } }
```

iOS `Info.plist`:

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array><string>com.company.app</string></array>
  </dict>
</array>
```

Android `AndroidManifest.xml` (inside the main `<activity>`):

```xml
<intent-filter>
  <action android:name="android.intent.action.VIEW"/>
  <category android:name="android.intent.category.DEFAULT"/>
  <category android:name="android.intent.category.BROWSABLE"/>
  <data android:scheme="com.company.app"/>
</intent-filter>
```

Wire `@capacitor/app` `appUrlOpen` event in your auth bootstrap. Call `supabase.auth.exchangeCodeForSession(url)` with the URL received.

The same pattern works for any OAuth provider that supports custom schemes (Auth0, Firebase, Clerk, WorkOS).

---

## 7. Sign in with Apple impl (when Guideline 4.8 applies)

Trigger: if the app offers ANY third-party social login (Google, Facebook, Twitter, LinkedIn, Meta, GitHub, etc.), Apple Sign-in is REQUIRED with at least equal prominence.

```tsx
// React + Supabase example. Adapt to your auth provider.
import { SignInWithApple, SignInWithAppleOptions } from '@capacitor-community/apple-sign-in';

async function signInWithApple() {
  const options: SignInWithAppleOptions = {
    clientId: 'com.company.app.signin', // services ID, not bundle ID
    redirectURI: 'https://yoursite.com/auth/callback',
    scopes: 'email name',
    state: crypto.randomUUID(),
    nonce: crypto.randomUUID(),
  };
  const result = await SignInWithApple.authorize(options);
  await supabase.auth.signInWithIdToken({
    provider: 'apple',
    token: result.response.identityToken!,
    nonce: options.nonce,
  });
}
```

Visual: button must NOT be smaller, lower in the stack, or styled less prominently than Google/Facebook. Same width, same vertical position priority.

---

## 8. Account deletion pattern (mandatory both stores)

```
Settings → Account → Delete Account
  Step 1: Warning screen with explicit consequences
          (what data is lost, what stays, any retention period)
  Step 2: Re-auth (password or biometric)
  Step 3: Final confirm with destructive button styling
  Step 4: Either immediate deletion OR scheduled deletion in N days
          (Apple accepts both; document the choice in your Privacy Policy)
  Step 5: Confirmation toast + automatic sign-out + redirect to landing
```

Backend rules:
- Hard-delete personal data OR anonymize (replace PII with `deleted_user_<id>`).
- Soft-delete is allowed if a recovery window is disclosed in the Privacy Policy and the user can hard-delete within the app.
- Cascading deletes: user-generated content the user authored can be either deleted, anonymized, or kept if it has third-party value (e.g., comments on others' posts). Document the choice.
- Server retention exceptions (legal, financial, fraud) MUST be disclosed.

Anti-patterns that get rejected:
- Email-only deletion ("email us at...")
- Web-only deletion when the user can create an account in-app
- Deletion gated behind a paid plan
- More than 5 taps from Settings

---

## 9. Push opt-in choreography (NEVER on first launch)

Sequence:

```
1. Onboarding completes WITHOUT asking for push.
2. User performs an action where push notifications add concrete value
   (saves an item, follows a topic, books a slot, joins a thread, completes a workflow).
3. App shows a custom pre-prompt sheet:
   Title:   "Stay in the loop on [the thing they just engaged with]"
   Body:    "We'll only notify you about [user-selected categories] and critical changes.
             You can change this anytime in Settings."
   Buttons: [Activate]  [Not now]
4. ONLY if user taps Activate, call the native permission API
   (@capacitor/push-notifications requestPermissions()).
5. Provide granular opt-out in Settings → Notifications, with category toggles
   (transactional, marketing, social, system alerts, etc.).
```

Why pre-prompt: the system dialog can be shown once on iOS. If the user denies, you must send them to Settings. The pre-prompt filters out denials BEFORE the OS prompt fires, preserving your ability to ask again later.

Default OFF for marketing pushes. Apple 4.5.4 rejects marketing pushes that lack explicit, granular opt-in.

---

## 10. Android `AndroidManifest.xml` minimal permissions block

Declare ONLY what you actually use. Every extra permission is a Data Safety mismatch waiting to happen.

```xml
<!-- Network (almost universal, fine) -->
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

<!-- Notifications (Android 13+ requires runtime prompt) -->
<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>

<!-- Camera (justify in Play Console if used) -->
<uses-permission android:name="android.permission.CAMERA"/>
<uses-feature android:name="android.hardware.camera" android:required="false"/>

<!-- Location: pick ONE -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<!-- ACCESS_BACKGROUND_LOCATION requires a Permissions Declaration form. Avoid unless core. -->
```

`targetSdkVersion`: set to the current Google Play required level. Below that = rejected updates.

For full permission strings (the human-readable explanations), see `02-permissions.md`.

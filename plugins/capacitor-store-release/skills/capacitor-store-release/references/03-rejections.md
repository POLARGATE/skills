# Rejection Codes Reference

Apple's top 15 and Google Play's top 10 rejection categories with symptoms and exact fixes. Use when triaging an actual rejection email, or pre-flighting submission to avoid known traps.

If the user has just pasted a rejection, follow the **Rejection Triage Protocol** in the main SKILL.md before consulting this file.

---

## Apple App Review: Top 15 rejection categories

### 1. Guideline 2.1 Performance: App crashes on launch

Symptom: reviewer opens the app, white screen or crash, immediate reject.

Fix:
- Test cold start on a real physical device, not just simulator.
- Add Sentry or equivalent crash reporting.
- Catch all unhandled promise rejections in the JS bridge.
- Audit the splash → first paint transition for race conditions.

### 2. Guideline 2.3.1 Accurate Metadata: "Beta", "Test", "WIP" strings

Symptom: app name, subtitle, screenshots, description, or in-app UI contains development markers.

Fix: full grep across UI, screenshots, and store metadata for: `beta`, `test`, `WIP`, `TODO`, `staging`, `demo`, `lorem`, `placeholder`, `coming soon`, `Lovable`, `Vercel`, framework names.

### 3. Guideline 2.3.3 Screenshots: Screenshots don't match the app

Symptom: screenshots show features the app doesn't have, or an older UI.

Fix: take fresh screenshots from the EXACT build you're submitting, on a real device, in 5 standard iOS sizes (6.5", 6.7", 5.5", iPad Pro 12.9" 2nd gen, 12.9" 6th gen). No mockups, no aspirational UI.

### 4. Guideline 4.0 Design: "App functions like a website"

Symptom: reviewer says it's basically a web app, no native value.

Fix:
- Wire haptics on every primary CTA.
- Native share via `@capacitor/share`.
- `@capacitor/browser` (SafariViewController) for external links.
- Real offline mode (cached data viewable in airplane mode, not just shell).
- Push notifications with actual value.
- At least one platform-exclusive feature: Wallet pass, Live Activity, Widget, Shortcut, App Intent, Lock Screen widget.
- In the review notes, EXPLICITLY list the native features and why the experience differs from the web.

### 5. Guideline 4.2 Minimum Functionality: "Limited functionality"

Symptom: "Most of this content is available in your browser."

Fix: same as 4.0, plus emphasize app-exclusive content or features in the review notes. If you genuinely can't justify native presence, the answer is PWA + Bubblewrap for Android only, skip iOS App Store.

### 6. Guideline 4.8 Login Services: Sign in with Apple missing

Symptom: app offers Google or Facebook login but no Apple option.

Fix: add Sign in with Apple at LEAST as prominent as the other options. See `01-templates.md` section 7 for implementation.

Carve-out: email/password alone does NOT trigger 4.8. Adding even ONE third-party provider does.

### 7. Guideline 5.1.1(v) Account Deletion: No in-app deletion path

Symptom: "Apps that support account creation must let users delete their accounts in-app."

Fix: implement Settings → Account → Delete Account, max 3 taps from Settings root. See `01-templates.md` section 8 for the pattern.

Tip: leave a comment in review notes: "Delete account is at Settings > Account > Delete Account. Use the demo account credentials provided."

### 8. Guideline 5.1.1(i) Data Collection: Asking for data before showing value

Symptom: app prompts for sign-up, push permission, ATT, or location on first launch.

Fix: defer ALL permission and data prompts until the user has experienced core value. Push and ATT especially should be contextual (after the user does the action that needs it).

### 9. Guideline 3.1.1 IAP: External payment link for digital goods

Symptom: "Subscribe at company.com/pro" link inside the iOS app for a digital subscription.

Fix:
- Remove the external link, OR
- Convert to IAP (StoreKit / RevenueCat / Glassfy), OR
- Confirm the carve-out (Guideline 3.1.3 a-f for reader apps, multiplatform services, person-to-person services, etc.). If a carve-out applies, document it in review notes.

### 10. Guideline 5.1.2 Data Use & Sharing: Privacy Manifest missing or inaccurate

Symptom: build flagged for required-reason API usage with no `PrivacyInfo.xcprivacy`, OR Privacy Nutrition Labels in App Store Connect don't match runtime behavior.

Fix:
- Add `ios/App/App/PrivacyInfo.xcprivacy` (template in `01-templates.md` section 2).
- Audit every third-party SDK for its own privacy manifest. Major SDKs (Firebase, Sentry, RevenueCat, Adjust, Amplitude, Mixpanel, etc.) ship one. If you use an SDK that doesn't, replace it.
- In App Store Connect → App Privacy, declare every data type your app collects (and what your SDKs collect on your behalf). Mismatches with the manifest are auto-flagged.

### 11. Guideline 5.1.5 Location: Background location without strong justification

Symptom: app requests `NSLocationAlwaysAndWhenInUseUsageDescription` for a vague use case.

Fix: move to When-In-Use only. If the use case truly requires background (workout tracking continuation, family sharing, asset tracking), write a SPECIFIC justification in the Info.plist string AND in review notes.

### 12. Guideline 2.5.1 Software: Uses private API or undocumented framework

Symptom: build flagged for non-public symbols (e.g., `_UIDeviceUniqueIdentifier`).

Fix: identify the offending dependency. Often an outdated analytics or ads SDK. Replace or upgrade.

### 13. Guideline 4.5.4 Push Notifications: Marketing push without explicit opt-in

Symptom: app sends promotional pushes without granular consent.

Fix:
- Default OFF for marketing.
- Add Settings → Notifications with category toggles (Transactional, Account alerts, Marketing, Social, etc.).
- Document the granularity in review notes.

### 14. Guideline 1.1.6 Safety: Inaccurate or misleading health/medical/financial info

Symptom: app makes claims it can diagnose, treat, predict outcomes, or guarantee returns.

Fix:
- Add explicit disclaimers: "Not medical advice", "Not financial advice", "Educational purposes only".
- Restrict to general information; never personalize a diagnosis or recommendation as definitive.
- For health apps, reference HealthKit guidelines and Apple's Health app integration where appropriate.

### 15. Guideline 3.2.2 Business: Bait-and-switch or unclear pricing

Symptom: subscription terms unclear, free trial converts without warning, price shown without tax, cancellation hidden.

Fix:
- Show full price BEFORE the purchase action, including currency and billing cycle.
- Free trial: show "$X/month after Y-day free trial".
- Link cancellation instructions clearly (deep link to subscription settings).

---

## Google Play: Top 10 rejection categories

### 1. Data Safety mismatch

Symptom: Data Safety form declares no data collection, but SDKs (Firebase, Crashlytics, ad networks) collect identifiers, location, or behavioral data.

Fix:
- Re-audit every SDK in your app for what it transmits.
- Re-fill the Data Safety form to match.
- Pay attention to SDK-collected device IDs, advertising IDs, IP addresses, and crash logs.

### 2. Deceptive Behavior

Symptom: screenshots, description, or icon overstate what the app does.

Fix: be honest. If the app doesn't have "AI", don't say "AI-powered". If it doesn't track sleep, don't show a sleep dashboard in screenshots.

### 3. Permissions: Sensitive permissions without core feature

Symptom: app requests `READ_SMS`, `READ_CALL_LOG`, `QUERY_ALL_PACKAGES`, or `BIND_ACCESSIBILITY_SERVICE` without a use case Google accepts.

Fix:
- Remove the permission, OR
- Submit the Permissions Declaration form with strong justification.
- For SMS/Call Log: only default SMS/dialer apps qualify.

### 4. Background Location without justification

Symptom: `ACCESS_BACKGROUND_LOCATION` requested without an obvious need.

Fix: move to foreground location. If background truly needed, submit Permissions Declaration form with concrete justification.

### 5. Target API level below required SDK

Symptom: app targets an older Android API than Play currently requires.

Fix: bump `targetSdkVersion` in `android/app/build.gradle` to the current required level (verify on play.google.com/about/requirements). Resolve any deprecations the bump introduces.

### 6. Account Deletion missing

Symptom: app allows account creation but provides no in-app deletion path.

Fix: same pattern as Apple. Implement in-app deletion AND provide a web URL on the Play Console listing's "Account deletion" field.

### 7. Families Policy violations

Symptom: app appears to appeal to children (cartoon icon, simple gameplay, kid-targeted ads) but doesn't comply with Designed for Families requirements.

Fix:
- Move out of children's category (audience switch), OR
- Fully comply: appropriate ads only, no behavioral targeting of children, COPPA-compliant.

### 8. Health Misrepresentation

Symptom: app claims to diagnose, cure, treat, or prevent diseases without medical evidence.

Fix: same as Apple 1.1.6. Disclaimers and conservative claims.

### 9. Subscription clarity

Symptom: cancellation instructions missing, pricing unclear, auto-renewal hidden.

Fix:
- Display full pricing pre-purchase.
- Link cancellation instructions clearly.
- For trials, show the post-trial price prominently.

### 10. Malware false positive (Play Protect flags)

Symptom: code obfuscation, hidden APKs, suspicious WebView behavior triggers Play Protect.

Fix:
- Disable aggressive Proguard / R8 modes.
- Enroll in Play App Signing.
- Remove any dynamic code loading.
- Avoid WebView assumptions that look like phishing patterns (overlays, system UI mimicry).

---

## Rejection Triage Protocol (when user pastes a rejection email)

1. Extract the exact guideline number or policy area.
2. Translate reviewer language into a concrete code or UX issue (use this file).
3. Classify the rejection:
   - **VALID**, reviewer is right, clear fix path. Most common.
   - **AMBIGUOUS**, reviewer is right in spirit but the fix isn't obvious. Need clarifying info from user.
   - **APPEALABLE**, reviewer misunderstood. Rare, requires strong policy basis. Never appeal as a first move.
4. Output to the user:
   - Diagnosis (what the reviewer means in plain English)
   - Root cause (where in the codebase or store listing)
   - Fix plan (numbered steps, paste-ready)
   - Reviewer reply draft (concise, factual, no defensive tone)
   - Resubmission checklist (what to verify before re-submitting)

Never recommend an appeal without a strong, documented policy basis. Appeals that lose burn 5 to 10 more days and tag the team in Apple's system.

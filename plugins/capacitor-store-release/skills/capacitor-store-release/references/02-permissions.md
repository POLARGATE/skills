# Permission Strings Catalog

Apple and Google both reject vague permission strings. The rule that survives every guideline change: **be specific, be honest, frame in user value, name the feature**.

This catalog gives reusable patterns by app vertical. Pick the one closest to your app and adapt.

---

## The principle (universal)

Every permission string must answer ONE question: **"What does the user get by allowing this?"**

- BAD: "We need camera access." → reject.
- BAD: "For a better experience." → reject (especially on ATT).
- BAD: "Required for app functionality." → reject.
- GOOD: "Camera is used to [specific feature the user just tried to use]."
- GOOD: "Location is used to [concrete user benefit, not company benefit]."

Two extra rules:
- Mention the feature, not the API. The user doesn't care about "camera access", they care about "scanning a receipt".
- Keep under 100 characters where possible. iOS truncates long strings in the prompt.

---

## iOS `Info.plist` strings by app vertical

### Camera: `NSCameraUsageDescription`

| Vertical | String |
|---|---|
| Productivity / Office | `"Camera is used to scan documents, receipts, and business cards."` |
| Social / Profile | `"Camera is used to take photos for your profile, posts, and stories."` |
| Marketplace / E-commerce | `"Camera is used to photograph items when you create a listing."` |
| Fitness / Health | `"Camera is used to scan barcodes on food packaging for nutrition tracking."` |
| Fintech / Banking | `"Camera is used for ID verification and to deposit checks."` |
| Real-estate / Property | `"Camera is used to upload photos of properties you list or view."` |
| Travel / Booking | `"Camera is used to scan boarding passes and travel documents."` |
| Events / Ticketing | `"Camera is used to scan your ticket QR code at venue entrances."` |
| Education / Learning | `"Camera is used to scan worksheets and take photos of your notes."` |

### Photo Library: `NSPhotoLibraryUsageDescription`

Universal pattern: `"Allow access to select a photo for [specific user action]."`

| Vertical | String |
|---|---|
| Social | `"Allow access to choose photos for your profile and posts."` |
| Marketplace | `"Allow access to add photos to the items you sell."` |
| Messaging | `"Allow access to send photos in your conversations."` |
| Fintech | `"Allow access to attach documents like ID copies or receipts."` |

### Photo Library Add: `NSPhotoLibraryAddUsageDescription`

Universal pattern: `"Allow saving [specific output] to your Photos."`

| Vertical | String |
|---|---|
| Ticketing | `"Allow saving your tickets and passes to Photos."` |
| Creator tools | `"Allow saving your edited images and videos to Photos."` |
| QR / receipt apps | `"Allow saving your receipts and confirmations to Photos."` |

### Location When In Use: `NSLocationWhenInUseUsageDescription`

| Vertical | String |
|---|---|
| Delivery / Ride-hail | `"Location is used to deliver your orders and show your driver your pickup point."` |
| Maps / Navigation | `"Location is used to show your position and provide directions."` |
| Local discovery | `"Location is used to recommend places, services, and offers near you."` |
| Fitness / Outdoor | `"Location is used to track your routes and measure distance."` |
| Weather | `"Location is used to provide weather and alerts for your current area."` |
| Real-estate | `"Location is used to show properties and prices near you."` |
| Events | `"Location is used to show events and venues near you."` |

### Location Always: `NSLocationAlwaysAndWhenInUseUsageDescription`

Use ONLY when the app genuinely needs background location. Apple scrutinizes this heavily.

| Use case | String |
|---|---|
| Run/cycle tracking continuing in background | `"Location is used to continue tracking your workout when the app is in the background."` |
| Safety / Family sharing | `"Location is used to share your live location with family members you choose."` |
| Asset / Vehicle tracking | `"Location is used to monitor your tracked vehicles even when the app is closed."` |

If you can solve the use case with When-In-Use + significant location changes, do that instead.

### Microphone: `NSMicrophoneUsageDescription`

| Vertical | String |
|---|---|
| Voice notes / Journaling | `"Microphone is used to record voice notes and memos."` |
| Video / Creator | `"Microphone is used to record audio alongside your videos."` |
| Calling / Conferencing | `"Microphone is used for voice and video calls with other users."` |
| Translation | `"Microphone is used to capture speech for translation."` |
| Music / Audio | `"Microphone is used to record audio for your tracks and projects."` |
| Health / Sleep | `"Microphone is used to detect sounds during your sleep tracking sessions."` |

### Contacts: `NSContactsUsageDescription`

Universal pattern: `"Contacts are used to [specific connector feature]."`

| Vertical | String |
|---|---|
| Social | `"Contacts are used to find friends you already know on the app."` |
| Messaging | `"Contacts are used to sync your address book so you can message people you know."` |
| Marketplace / Referrals | `"Contacts are used to send referrals to friends you choose."` |

### Calendar: `NSCalendarsUsageDescription`

| Vertical | String |
|---|---|
| Productivity | `"Calendar access lets you add tasks and meetings to your schedule."` |
| Booking / Reservations | `"Calendar access lets you add your bookings and reservations."` |
| Events | `"Calendar access lets you add events you save to your personal schedule."` |
| Healthcare | `"Calendar access lets you add appointments and reminders to your schedule."` |

### Tracking: `NSUserTrackingUsageDescription`

Required for any cross-app tracking (IDFA). Apple rejects vague benefit framing here.

Honest pattern: `"Allow tracking to receive ads and content tailored to your interests across other apps and websites."`

Acceptable variants for specific business models:
- Ads-supported app: `"Allow tracking to keep this app free by showing more relevant ads."`
- Attribution-only (no targeting): `"Allow tracking to measure which ads brought you here."`

NEVER: "for a better experience", "to improve the app", "for personalization" (without saying tracking explicitly).

### Bluetooth: `NSBluetoothAlwaysUsageDescription`

| Use case | String |
|---|---|
| Wearable sync | `"Bluetooth is used to connect to your fitness tracker and sync your data."` |
| IoT control | `"Bluetooth is used to control your smart devices from this app."` |
| Contactless payments | `"Bluetooth is used for contactless payments at participating locations."` |
| Audio devices | `"Bluetooth is used to discover and connect to nearby speakers and headphones."` |

### Motion: `NSMotionUsageDescription`

| Use case | String |
|---|---|
| Fitness | `"Motion data is used to count steps and detect your workouts."` |
| AR / Camera effects | `"Motion data is used to align AR content with your environment."` |
| Driving / Safety | `"Motion data is used to detect when you are driving."` |

### Face ID: `NSFaceIDUsageDescription`

| Vertical | String |
|---|---|
| Fintech | `"Face ID is used to securely sign in and authorize transactions."` |
| Password / Vault | `"Face ID is used to unlock your vault and autofill passwords."` |
| Health / Medical | `"Face ID is used to protect access to your health records."` |

### Speech Recognition: `NSSpeechRecognitionUsageDescription`

`"Speech recognition is used to transcribe your voice notes into text."`
`"Speech recognition is used to convert spoken commands into actions."`

### Local Network: `NSLocalNetworkUsageDescription`

`"Local network access is used to discover and connect to [specific devices, e.g., smart speakers, printers, cameras] on your Wi-Fi."`

---

## Android equivalents (where they differ)

Android shows the system permission name plus your app name; you don't write a sentence. But Google Play STILL evaluates whether the in-app justification (pre-prompt, onboarding copy) matches actual use. The Data Safety form is where the equivalent of "permission strings" lives.

Special cases that require Permissions Declaration forms in Play Console:
- `ACCESS_BACKGROUND_LOCATION`, justify why foreground isn't enough.
- `READ_SMS`, `RECEIVE_SMS`, `READ_CALL_LOG`, only for default SMS/dialer apps. Other use cases rejected.
- `QUERY_ALL_PACKAGES`, only for launchers, antivirus, browsers, accessibility apps.
- `MANAGE_EXTERNAL_STORAGE`, file manager apps only (Android 11+).

---

## Pre-prompt copy (custom UI, before the OS dialog)

This is your one chance to set the right expectation. The system dialog comes AFTER.

Template:

```
Headline:   [User-facing feature name]
Subhead:    "To [do X], we need access to your [permission]."
Body:       "We use this only when [scope]. You can change this anytime in Settings."
Buttons:    [Allow]  [Not now]
```

Example for any vertical:

```
Headline:   Get notified when your order arrives
Subhead:    "We use notifications only for delivery updates."
Body:       "You can adjust which notifications you receive in Settings."
Buttons:    [Allow]  [Not now]
```

Always defer the OS prompt until the user taps Allow in the pre-prompt. This protects your ability to ask later.

---

## Quick smell test for any permission string

Ask yourself, would the user write this themselves? If yes, ship. If it reads like a legal disclaimer, rewrite.

- ❌ "We require camera access to enable in-app functionality."
- ✅ "Camera lets you scan receipts so we can extract the total automatically."

The second sounds like a feature description. The first sounds like a privacy policy clause. Reviewers (and users) tell the difference instantly.

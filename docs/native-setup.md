# Native app setup (Capacitor)

## Splash screen

The app uses `@capacitor/splash-screen`. The first screen users see is the **native splash**; the WebView is shown after the app loads and the splash is hidden from `main.tsx`.

### What it looks like

- **iOS**: Full-screen image from the **Splash** asset set (`ios/App/App/Assets.xcassets/Splash.imageset/`). The image is scaled to **fit** the screen (aspect fit). Any letterboxing uses the system background color.
- **Android**: Full-screen drawable `@drawable/splash` (the launch activity uses `AppTheme.NoActionBarLaunch`). Multiple `splash.png` files exist under `android/app/src/main/res/drawable*` for portrait/landscape and densities.

So on both platforms the splash is **image-based** (your logo or artwork), with a **background color** used by the plugin where the image doesn’t cover (e.g. letterboxing).

### Customization

**1. Plugin config** (`capacitor.config.ts` → `plugins.SplashScreen`)

| Option | Current | Description |
|--------|---------|-------------|
| `launchShowDuration` | `2000` | Min time (ms) to show splash when auto-hide is on. We hide from JS when the app is ready, so this is a fallback minimum. |
| `backgroundColor` | `'#1a1a2e'` | Background color (hex). Shown behind/around the splash image. |
| `showSpinner` | `true` | Set `true` to show a loading spinner on top. |
| `spinnerColor` | — | Hex color for the spinner (e.g. `'#ffffff'`). |
| `launchAutoHide` | *(default true)* | If `false`, splash stays until you call `SplashScreen.hide()`. |

**2. iOS – change the image**

- Replace the PNGs in `ios/App/App/Assets.xcassets/Splash.imageset/`:
  - `splash-2732x2732.png` (1x)
  - `splash-2732x2732-1.png` (2x)
  - `splash-2732x2732-2.png` (3x)
- Or in Xcode: open `ios/App/App`, select **Assets.xcassets** → **Splash**, and replace the images. Keep the same names or update `Contents.json` and `LaunchScreen.storyboard` to reference the new image set.

**3. Android – change the image**

- Replace the splash drawables:
  - `android/app/src/main/res/drawable/splash.png`
  - `android/app/src/main/res/drawable-port-*/splash.png` and `drawable-land-*/splash.png` (for orientations/densities)
- Or use a single drawable (e.g. color or vector) and point `res/values/styles.xml` → `AppTheme.NoActionBarLaunch` → `android:background` at it (e.g. `@drawable/splash` or `@color/splash_background`).

## Push notifications

The app uses `@capacitor/push-notifications`. Registration runs only on **native** (not in the browser). On launch, the app requests permission and, if granted, registers and forwards tokens/events to the WebView.

- **Web**: Push registration is skipped when not running as a native app.
- **Native**: In `main.tsx` the app:
  1. Requests permission via `PushNotifications.requestPermissions()`.
  2. If the user grants, calls `PushNotifications.register()` (obtains FCM/APNs token).
  3. Forwards events as custom DOM events:
     - `push-registration` – token (detail: `{ value }`)
     - `push-received` – notification received (detail: notification payload)
     - `push-action` – user tapped the notification (detail: action payload)

To **enable push** you must add the native capabilities and (on Android) Firebase.

### iOS – enable push

1. Open the iOS project in Xcode: `ios/App/App.xcworkspace` (or `ios/App` in Xcode).
2. Select the **App** target in the project navigator.
3. Open **Signing & Capabilities**.
4. Click **+ Capability** and add **Push Notifications**.
5. Add **Background Modes** and enable **Remote notifications** (so the device can receive pushes when the app is in the background).

After this, install on a **real device** (push does not work in the Simulator). The first launch will show the system permission prompt; if the user allows, the app will register and you’ll get the token via the `push-registration` event.

### Android – enable push

1. Create a [Firebase](https://firebase.google.com/) project and add an Android app with your package ID (`io.retrochat.app`).
2. Download `google-services.json` from the Firebase console.
3. Place `google-services.json` in `android/app/`.
4. Ensure the app’s `build.gradle` applies the Google services plugin and the push plugin (Capacitor’s template usually does this after `npx cap sync`).

Listen for `push-registration` in your app to send the token to your backend for sending FCM messages.

## Haptics

The app uses `@capacitor/haptics` for light impact feedback (e.g. send button, tab switches) via `src/lib/haptics.ts` (`hapticLight()`).

- **Web**: No-op; haptics are only used when `Capacitor.isNativePlatform()` is true.
- **iOS**: Haptics work **only on a physical device**. The iOS Simulator has no Taptic Engine, so you will not feel or see any feedback in the simulator. Test on a real iPhone or iPad to confirm.
- **Android**: Vibration/haptics depend on device support; the plugin is wired in the Capacitor Android target.

If haptics don’t work on a real device, ensure the app was built with the Haptics plugin included (`CapacitorHaptics` is listed in `ios/App/CapApp-SPM/Package.swift`) and run `npx cap sync` after any plugin changes.

## Secure storage

`src/lib/secureStorage.ts` provides:

- **Native**: `@capacitor/preferences` (native-backed storage).
- **Web**: `localStorage` with a prefix.

Use `secureStorageGet`, `secureStorageSet`, and `secureStorageRemove` for tokens or other secrets. For **Keychain (iOS) / Keystore (Android)** you can replace the native implementation with a plugin such as:

- [@capawesome-team/capacitor-secure-preferences](https://capawesome.io/plugins/secure-preferences/)
- [capacitor-secure-storage-plugin](https://www.npmjs.com/package/capacitor-secure-storage-plugin)

Then swap the `getPreferences()` / get/set/remove logic in `secureStorage.ts` to use that plugin on native while keeping the same API.

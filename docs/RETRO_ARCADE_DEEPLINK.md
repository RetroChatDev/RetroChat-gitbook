# RetroArcade deep link (iOS)

RetroChat opens ROMs in the RetroArcade app via a custom URL scheme. If the link doesn’t open the app, the app is almost certainly **not registering that scheme** in iOS.

## URL we open

- **Scheme:** `retroarcade` (lowercase)
- **Format:** `retroarcade://play/<encoded-rom-url>?url=...&download=...&rom=...&title=...`
- **Example:** `retroarcade://play/https%3A%2F%2F...supabase...%2Fgame.gba?url=https%3A%2F%2F...&download=...&rom=...&title=My%20Game`

The download URL is provided in two ways so the app can read it reliably:

1. **Path:** The first path component after `/play/` is the ROM URL (percent-encoded once). Decode it and use for download.
2. **Query:** `url`, `download`, and `rom` all contain the same full URL (percent-encoded). `title` is the game title.

## What the RetroArcade app must do (Xcode)

1. **Register the URL scheme**
   - In Xcode: select the **app target** → **Info** tab → **URL Types**.
   - Click **+** to add a URL Type.
   - Set **Identifier** to e.g. `com.you.retroarcade` (or your bundle ID).
   - Set **URL Schemes** to **exactly** `retroarcade` (one value, lowercase).
   - **Role:** Editor (or Viewer).
   - Leave **Document Role** / other fields default.

   Or in **Info.plist** add:

   ```xml
   <key>CFBundleURLTypes</key>
   <array>
     <dict>
       <key>CFBundleTypeRole</key>
       <string>Editor</string>
       <key>CFBundleURLName</key>
       <string>RetroArcade</string>
       <key>CFBundleURLSchemes</key>
       <array>
         <string>retroarcade</string>
       </array>
     </dict>
   </array>
   ```

2. **Handle the URL when the app opens and start the download**
   - In **AppDelegate**: implement `application(_:open:options:)` and read `url`.
   - Get the download URL from **(a) path** or **(b) query** (see Swift example below). Use that URL to start the game file download (e.g. `URLSession.shared.downloadTask`), then open/play the ROM when the file is ready.
   - If you use **SceneDelegate**: implement `scene(_:openURLContexts:)` and get the URL from `URLContexts.first?.url`.

3. **Rebuild and reinstall**
   - After adding the URL type, **clean build** (Product → Clean Build Folder) and run again on the device from Xcode. The scheme is only registered after a fresh install.

## Testing

- Open RetroChat in **Safari** on the device (not in a WebView inside another app).
- Go to Arcade → tap a game (iOS flow).
- Tap **“Open in RetroArcade”**.
- If the scheme is registered, iOS should switch to RetroArcade and deliver the URL. If you see “invalid address” or “cannot open page”, the scheme is still not registered or doesn’t match `retroarcade`.

## Getting the download URL in the app (Swift)

Parse the incoming URL and start the download. Prefer the path so the URL is unambiguous:

```swift
// AppDelegate or SceneDelegate
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    print("Opened with URL: \(url)")

    var downloadURLString: String?
    var title = "Game"

    // 1) Try path: retroarcade://play/<encoded-rom-url>?...
    let comps = url.pathComponents
    if comps.count >= 3 && comps[1] == "play" {
        let encodedSegment = comps[2]
        if let decoded = encodedSegment.removingPercentEncoding, decoded.hasPrefix("http") {
            downloadURLString = decoded
        }
    }

    // 2) Fallback: query params (url, download, or rom)
    if downloadURLString == nil, let comp = URLComponents(url: url, resolvingAgainstBaseURL: false), let items = comp.queryItems {
        downloadURLString = items.first(where: { $0.name == "url" })?.value
            ?? items.first(where: { $0.name == "download" })?.value
            ?? items.first(where: { $0.name == "rom" })?.value
        title = items.first(where: { $0.name == "title" })?.value ?? title
    }

    guard let urlString = downloadURLString, let downloadURL = URL(string: urlString) else {
        return false
    }

    // Start the game file download (e.g. URLSession), then open the ROM when done.
    startDownload(romURL: downloadURL, title: title)
    return true
}
```

If the handler never runs when you tap the link in Safari, the app is not registered for `retroarcade`.

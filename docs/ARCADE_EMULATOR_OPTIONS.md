# Arcade emulator options and mobile refresh

## Why mobile refreshes (~1.5–2 min)

The arcade uses **Nostalgist**, which runs **RetroArch** compiled to **WebAssembly** in the browser. That stack is accurate and supports NES, SNES, GBA, GB, GBC, Genesis, N64 (Nintendo 64), and NDS (Nintendo DS). It is memory-heavy.

**N64 / NDS note:** N64 and NDS are launched via `Nostalgist.launch()` with cores `mupen64plus_next` and `melonds` respectively. The default Nostalgist CDN may not include these cores; if they fail in-browser, configure custom core URLs via `Nostalgist.configure({ resolveCoreJs, resolveCoreWasm })` or use the “open in external app” flow on mobile. On mobile, **Chrome and Safari** (and others) often **reload the tab** under memory pressure after ~1.5–2 minutes of gameplay. This is a **browser/OS limitation**, not something we can prevent from the app.

**Current mitigation:** We auto-save state every 30s on mobile (and on page hide), and after a reload we auto-restore from the last save and show a “Game restored” toast.

---

## Can we use a different emulator to avoid the refresh?

### Short answer

There is **no drop-in replacement** that supports all systems (NES, SNES, GBA, GB, GBC, Genesis, N64, NDS) with meaningfully lower memory. Any change that reduces mobile refresh is a **partial** solution and requires extra integration.

### Options

1. **Keep Nostalgist (current)**  
   - One API for all systems, save/load, good accuracy.  
   - Mobile refresh remains; we mitigate with auto-save/restore.

2. **Use a lighter emulator for NES only on mobile**  
   - **JSNES** is a **pure JavaScript** NES emulator (no WebAssembly). It uses less memory than RetroArch/WASM, so it *might* avoid or delay the mobile refresh for **NES games only**.  
   - Downsides:  
     - NES only; SNES/GBA/GB/GBC/Genesis on mobile would still use Nostalgist and can still refresh.  
     - Different API: we’d need an adapter (frame loop, canvas, buttons, save/load) and two code paths (Nostalgist vs JSNES).  
     - Pure JS can be slower on weak devices; would need testing.  
   - If you want to pursue this: add the `jsnes` npm package and implement a “use JSNES when `system === 'nes' && isMobile`” path in `ArcadeContext`, with the same surface (load, frame, buttons, saveState, loadState, exit).

3. **Other systems (SNES, GBA, etc.)**  
   - There isn’t a well-maintained, clearly lighter (e.g. pure-JS, no WASM) browser emulator that matches Nostalgist’s multi-system support. Most alternatives also use WebAssembly and similar memory usage.

---

## Recommendation

- **Default:** Keep Nostalgist and rely on **auto-save + auto-restore** so that when the mobile browser reloads, the user gets their progress back quickly.  
- **Optional:** If NES is the main use case on mobile and the refresh is unacceptable, add **JSNES for NES on mobile only** and keep Nostalgist for everything else (and for desktop). That would require the adapter work above and testing on real devices.

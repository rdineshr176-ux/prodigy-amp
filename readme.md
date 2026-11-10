# Prodigy Amp (v11.0) — Cross-Device Cloud Music Streaming Platform

**Live Production App:** [https://prodigy-amp.netlify.app](https://prodigy-amp.netlify.app)  
**GitHub Repository:** [https://github.com/rdineshd176-png/Prodigy-Amp-.git](https://www.google.com/search?q=https://github.com/rdineshd176-png/Prodigy-Amp-.git)  
**Google Drive Studio Folder:** [https://drive.google.com/drive/folders/19QCAtbf532sOkXV\_y5fAthRjkoesVIJB](https://www.google.com/search?q=https://drive.google.com/drive/folders/19QCAtbf532sOkXV_y5fAthRjkoesVIJB)  
**Creator:** **R. Dinesh (`@Prodigy`)** — [rdineshd176@gmail.com](mailto:rdineshd176@gmail.com) | [LinkedIn](https://www.linkedin.com/in/dinesh-r-cybersec/)

---

## What's New in v11.0 (Mobile UI Overhaul & Complete 122-Issue Code Audit Fix)

### 1. Mobile UI Overhaul & Song Title Readability
- **Icon-Only Circular Play Buttons (`36×36px`)**: Song cards in the **Songs** catalog and queue rows on **Home** now use compact circular play/pause icon buttons (`▶` / `⏸`) instead of wide text buttons, freeing horizontal space on mobile screens.
- **Full 2-Line Song Title Readability (`.song-title-mobile-wrap`)**: Replaced aggressive 1-line ellipsis truncation (`truncate`) on song cards, queue rows, and the mobile bottom player dock with a clean 2-line wrap (`-webkit-line-clamp: 2`) so long track titles are readable on mobile viewports (`375px+`).
- **2-Row Mobile Header & Full-Width Mobile Search (`UX-H6`)**: On mobile screens (`< 640px`), the top header wraps cleanly so Row 1 houses the brand emblem and quick actions while Row 2 provides a full-width search bar (`#global-search-input`).
- **2-Row Mobile Bottom Audio Dock (`UX-H5`)**: On mobile screens (`< 640px`), Row 1 displays the cover art, 2-line song title/artist, Mute, and Minimize buttons, while Row 2 centers the full transport bar (**Shuffle**, **Previous**, **Play/Pause**, **Next**, **Repeat**).
- **Compact Mobile Songs Header & Horizontal Genre Strip**: Reduced vertical header padding and converted the genre filter pills into a single-row horizontal scroll strip on mobile so song cards appear immediately above the fold.
- **3-Dot (`⋮`) Track Action Menu**: Consolidated **Add to Playlist** and **Edit Song Details** inside each song's `⋮` dropdown menu with automatic outside-click and `Escape` dismissal.

### 2. Security Audit Remediations (`SEC-C1` through `SEC-L6`)
- **Zero Client-Side Password Hash Storage (`SEC-C3`, `SEC-C4`, `SEC-C6`, `SEC-H2`)**: Completely removed `computeAuthHash()`, stopped syncing `__USER_AUTH__` password rows to the public Google Sheet catalog, stopped writing `pass_hash` into Supabase `user_metadata`, and purged any legacy password fields from `localStorage`.
- **Strict HTML & Media URL Sanitization (`SEC-C5`, `UX-M8`, `SEC-L4`)**: Added `escHTML()` and `safeMediaUrl()` across all dynamic `innerHTML` templates (song cards, queue rows, playlists, modals, and contributor profiles) to block Stored and DOM XSS.
- **Webhook Masking & Anti-Enumeration (`SEC-C1`, `SEC-H3`, `SEC-H4`)**: Masked the Google Apps Script deployment URL in the UI, unified login error messages (`Invalid email/username or password.`), and added client-side exponential backoff after 3 failed login attempts.
- **Hardened HTTP Security Headers (`SEC-H5`, `SEC-M1`, `SEC-L6`)**: Updated `netlify.toml` with `Content-Security-Policy`, `X-Frame-Options = "DENY"`, `X-Content-Type-Options = "nosniff"`, `Referrer-Policy = "strict-origin-when-cross-origin"`, `Permissions-Policy`, `Cross-Origin-Opener-Policy = "same-origin"`, and `Cross-Origin-Resource-Policy = "same-origin"` on `/drive-audio/*`.

### 3. JavaScript & Audio Engine Fixes (`JS-C1` through `JS-L17`)
- **Concurrency & Stale Async Guards (`JS-C1`, `JS-H1`, `JS-H2`, `JS-H8`, `JS-H9`, `JS-M6`)**: Added monotonic `activeLoadToken` and `state.loadedTrackId` checks across `loadTrack` (fast and slow paths), `playCurrentTrack`, `resolvePlayableDriveUrl` (`savedTime >= 0` metadata listener), and background prefetching so rapid track switching never corrupts audio sources or restarts playback from `0:00`.
- **Cloud Chunk Upload Reliability (`JS-C4`, `JS-C5`, `JS-H12`, `JS-C6`)**: Persisted `state.cloudChunkedKeys` to `localStorage`, verified HTTP response status on every chunk batch before marking a song as uploaded, deduplicated concurrent chunk uploads via `inFlightChunkUploads`, and added a `syncInProgress` mutex on `syncWithGoogleDrive()`.
- **Hi-Fi Web Audio DSP & Sleep Timer (`JS-H3`, `JS-H4`, `JS-H5`)**: Synchronized `audioEl.volume = 0.88` on startup, initialized EQ/Bass/Preamp nodes from current slider values on first context creation, and wired `#sleep-timer-select` to an active `setTimeout` countdown that pauses playback and resets the selector when elapsed.
- **Non-Destructive Fisher–Yates Shuffle & Playlist Reordering (`JS-H6`, `JS-H7`, `JS-M3`, `JS-M8`)**: Replaced mutating array sorts with non-destructive random selection and mapped filtered playlist rows back to their exact index in `pl.trackIds`.

### 4. Accessibility & DOM Standards (`UX-C1` through `UX-L13`)
- **Pinch-to-Zoom & Keyboard Focus (`UX-C1`, `UX-C5`)**: Removed `maximum-scale=1.0, user-scalable=no` from the viewport meta tag and replaced `outline: none` with a high-visibility `:focus-visible` crimson outline.
- **Accessible Modals & Inert Background (`UX-C2`, `UX-C3`, `UX-H11`, `UX-M4`)**: Added `role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `Escape` key dismissal, backdrop click dismissal, `Tab` focus trapping, focus restoration, and `inert` + `aria-hidden="true"` on `<header>`, `<main>`, and `<nav>` whenever the mandatory auth gate is open.
- **Self-Contained CSS & 50% Smaller Bundle (`UX-H1`, `UX-H2`, `UX-H9`, `UX-M11`)**: Removed the render-blocking Tailwind Play CDN script, deduplicated inline base64 images via `data-init-src`, and removed unused DOM sections, cutting `index.html` from **862 KB** down to **426 KB**.

---

## How to Delete a Song Permanently (Owner/Admin Workflow)

Public visitors and listeners do **not** have a delete button on the website. As the platform owner (`@Prodigy`), you can remove a song in two ways:

1. **Google Drive Studio Folder + Google Sheet**:
   - Delete or move the audio file out of your [Google Drive Studio Folder](https://www.google.com/search?q=https://drive.google.com/drive/folders/19QCAtbf532sOkXV_y5fAthRjkoesVIJB).
   - Delete the corresponding track row (and any `CHUNK::...` rows) from your connected Google Sheet catalog, then click **Refresh Drive Catalog** in the app.
2. **Browser Console Admin Command (While Logged In as `@prodigy`)**:
   - Open DevTools Console (`F12`) on your site to inspect or manage local cache entries via `indexedDB.deleteDatabase("ProdigyAmpCloudDB_v3")` followed by a page refresh.

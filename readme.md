# Prodigy Amp — Universal Cloud Music Streaming Platform (v9.0 Production Release)

**Prodigy Amp** is a zero-cost, cross-device cloud music streaming platform (Spotify alternative) architected by **R. Dinesh** (*Prodigy*) for Windows Desktop and Mobile browsers.

* **Live Production URL**: [https://prodigy-amp.netlify.app](https://prodigy-amp.netlify.app)
* **Creator**: R. Dinesh (`@prodigy` / `rdineshd176@gmail.com`)
* **GitHub Repository**: [https://github.com/rdineshd176-png/Prodigy-Amp-.git](https://www.google.com/search?q=https://github.com/rdineshd176-png/Prodigy-Amp-.git)
* **LinkedIn Profile**: [https://www.linkedin.com/in/dinesh-r-cybersec/](https://www.linkedin.com/in/dinesh-r-cybersec/)
* **Connected Google Apps Script Deployment**: `https://script.google.com/macros/s/AKfycbwQlsKbmJuYwGooyUKSWx4g8zC63BGo6q6yn45i0-j-oVmSoOOM1QpzUNu74viwHIWwbw/exec`
* **Connected Google Drive Studio Folder**: [https://drive.google.com/drive/folders/19QCAtbf532sOkXV\_y5fAthRjkoesVIJB](https://www.google.com/search?q=https://drive.google.com/drive/folders/19QCAtbf532sOkXV_y5fAthRjkoesVIJB)
* **Connected Supabase Project**: `gbvunkkzbohyeqraxokz` (`ap-southeast-1`, Singapore)

---

## New in v9.0: Interactive Playlist Studio, Song Editing & Deletion, and Low-Internet Turbo Engine

### 1. Creating & Altering Songs in Playlists
* **From Any Song Card (`+ Playlist / Edit` button)**:
  * Click **`+ Playlist / Edit`** on any song card (in Home, Songs Library, or Active Queue) to open the **Playlist & Song Studio** modal.
  * Toggle the song in or out of any existing playlist with 1 click, or type a new playlist name and click **`+ Create & Add`**.
  * Alter the song's **Title**, **Artist Name**, or **Genre** directly inside the modal and click **`Save Changes`**.
* **From the Playlists Page (`Playlists` Tab)**:
  * Create a new playlist in the left sidebar (`Create New Playlist` → `+ Create`) and click any custom playlist to open its dedicated **Playlist Editor** view.
  * Use the **`+ Add Song to Playlist`** dropdown bar to add any song from your library to that playlist.
  * Reorder songs inside the playlist using the **Move Up (`↑`)** and **Move Down (`↓`)** buttons, remove individual songs with **`Remove`**, rename the playlist (`Rename`), play or shuffle the entire playlist (`Play All` / `Shuffle`), or delete the playlist (`Delete Playlist`).

### 2. How to Delete a Song in the Website (and in Google Drive)
* **Method A — Delete Directly Inside the Website UI (Syncs Across All Devices)**:
  1. Click the **`+ Playlist / Edit`** button on the song card you want to remove.
  2. At the bottom of the modal, click **`Delete Song`** and then click **`Confirm Delete?`**.
  3. The song is immediately removed from the website catalog, removed from all playlists, cleared from your browser's `IndexedDB`, and a cloud deletion tombstone (`__DELETED_TRACK__`) is pushed to your [Google Apps Script deployment](https://script.google.com/macros/s/AKfycbwQlsKbmJuYwGooyUKSWx4g8zC63BGo6q6yn45i0-j-oVmSoOOM1QpzUNu74viwHIWwbw/exec) so it disappears on every user's Desktop and Mobile browser.
* **Method B — Delete from Google Drive & Registry Spreadsheet (Hard Storage Cleanup)**:
  1. Open your [Google Drive Studio Folder](https://www.google.com/search?q=https://drive.google.com/drive/folders/19QCAtbf532sOkXV_y5fAthRjkoesVIJB).
  2. Delete the audio file from `01_Master_Audio_Tracks` or `02_Community_User_Uploads`, and delete its row in the `Tracks` tab of the **Prodigy Amp - Track & Contributor Registry** Google Sheet.

### 3. Low-Internet & Instant Search Optimizations
* **`0ms` Local Catalog Cache (`prodigy_amp_catalog_cache_v9`)**: Catalog metadata is cached locally so all songs, playlists, and search load instantaneously (`0ms`) even on slow 2G/3G mobile networks before background cloud sync finishes.
* **10x Faster Startup Sync (`?action=catalog`)**: Initial page load queries `?action=catalog` (reading the Google Sheet directly in `<300ms` without scanning Google Drive folders); full Drive folder scanning (`?action=sync`) runs only when you click **Sync Drive**.
* **Low-Net Turbo Mode (`Low-Net Turbo: ON`)**: Prevents background pre-fetching from downloading multiple songs simultaneously on slow connections—pre-fetching only the currently active song and serving cached tracks (`INSTANT` green badge) from `IndexedDB` with zero network traffic.
* **Pre-Indexed `O(1)` Multi-Keyword Search**: Every track's title, artist, genre, and contributor handle are pre-indexed in memory so searching across hundreds of songs happens in `<1ms` with zero network requests.

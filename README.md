# Oli Site

The full web app and marketing/info site for **Oli** — a free, ad-free music player with synced lyrics and offline playback.

This is a rebrand of [Echo Music Site](https://github.com/EchoMusicApp/Echo-Music-Site) (design and copy rewritten from scratch, not a copy of the original files) — see [Credits](#credits).

## Pages

| File | Purpose |
|---|---|
| `index.html` | **The web app** — this is the main page. A genuine browser client covering Home, Search, Library, Equalizer, Settings, and Listen Together — with a desktop-app-style layout on wide screens and an Android-app-style layout on phones. |
| `info.html` | Marketing/about page — hero, features, FAQ, download links. |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |

No build step — plain HTML/CSS/vanilla JS. Open `index.html` directly, or serve the folder with any static file server.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## What's actually in the app

- **Home** — mood chips, genre grid, trending row, search results, queue
- **Search** — live if a backend is connected, otherwise filters the demo catalog
- **Library** — Playlists (create/delete/add tracks), Favorites, History — all persisted in `localStorage`, no account or server needed
- **Equalizer** — a real 5-band graphic EQ using the Web Audio API (`BiquadFilterNode` chain), applies live to whatever's playing, with presets. This only affects this browser tab — it doesn't touch the Android/Desktop apps.
- **Settings** — configurable backend API URL, accent color, quality placeholder, clear-data button
- **Listen Together** — opens a real WebSocket connection to your `oli-server` deployment and reports genuine connection status. **This is intentionally labeled experimental in the UI** — see caveat below.

Two layouts sharing one playback engine, switched via CSS media query at 760px:
- **Desktop (≥760px):** sidebar navigation, persistent bottom transport bar, lyrics side panel
- **Mobile (<760px):** top bar + bottom nav, floating mini-player, full-screen swipe-up Now Playing sheet (mirrors the Android app's layout, including the squiggle play button)

By default the app runs in **demo mode** — freely-licensed [SoundHelix](https://www.soundhelix.com) tracks with placeholder metadata, so everything works with zero setup, including Library/Equalizer/Settings.

### Connecting real search/streaming

Settings → **Backend API URL** → paste your deployed [`oli-web-api`](https://github.com/oli-music/oli-web-api) URL. That's it — no code editing required, it's saved to `localStorage`. Search, thumbnails, and playback all switch over automatically; demo tracks still work as a fallback.

### Honest limitations

- **Listen Together is unverified end-to-end.** It opens a real WebSocket and reports real connection status (connecting/connected/error), which confirms your server is reachable — but the Android app's actual session protocol is Protocol Buffer-encoded (see `oli-proto`), and this web client does **not** implement that wire format. Treat it as a connectivity check, not confirmed cross-platform sync, until someone builds and tests the matching protobuf client.
- **Lyrics** are demo-only — there's no lyrics API wired up, so real (non-demo) tracks show an honest "no synced lyrics yet."
- **Downloads/offline** aren't implemented — browsers can't do this the way a native app can. The download button points users to the native apps instead of pretending to work.
- **Mood chips / genre tiles / trending row** trigger a real search using their label as a query — they're not backed by curated playlists or a charts API.
- **Equalizer** only affects Web Audio API playback in this tab; it's not a system-wide or cross-app setting.

## Why there's no backend-free version

A no-server, no-cookie build that talks to YouTube directly from the browser was tried and abandoned. Search failed immediately with a CORS error — `music.youtube.com`'s search endpoint doesn't send `Access-Control-Allow-Origin` headers permitting requests from arbitrary origins, which the browser enforces before the request even completes. This isn't fixable client-side; it's enforced by YouTube's server response, not anything in the request. It's why every browser-based YouTube frontend that exists (Invidious, FreeTube's web mode, etc.) runs its own backend proxy rather than calling YouTube directly — `oli-web-api` fills that same role here.

## Deploying

Static hosting works fine — GitHub Pages, Netlify, Vercel, Cloudflare Pages, etc. Keep all `.html` files in the same directory, since the pages link to each other with relative paths.

## Credits

Oli is a rebranded fork of the Echo Music project family, created by Aditya Yadav ([@iad1tya](https://github.com/iad1tya)), GPL-3.0 licensed. See the [oli](https://github.com/oli-music/oli) Android repo for full credits.

## License

GPL-3.0 — see [LICENSE](LICENSE).

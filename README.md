# Oli Site

The web player and marketing/info site for **Oli** — a free, ad-free music player with synced lyrics and offline playback.

This is a rebrand of [Echo Music Site](https://github.com/EchoMusicApp/Echo-Music-Site) (design and copy rewritten from scratch, not a copy of the original files) — see [Credits](#credits).

## Pages

| File | Purpose |
|---|---|
| `index.html` | **The web player** — this is the main page. Real search/playback/queue/synced lyrics, with a desktop-app-style layout on wide screens and an Android-app-style layout on phones. |
| `info.html` | Marketing/about page — hero, features, FAQ, download links. This used to be `index.html`; it moved here once the player became the homepage. |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |

No build step — plain HTML/CSS/vanilla JS. Open `index.html` directly, or serve the folder with any static file server.

```bash
# quick local preview
python3 -m http.server 8000
# then open http://localhost:8000
```

## The player (`index.html`)

Two distinct layouts sharing the same playback engine, switched via CSS media query at 760px:

- **Desktop (≥760px):** sidebar navigation, persistent bottom transport bar, lyrics side panel — matching `oli-desktop`'s layout conventions.
- **Mobile (<760px):** top bar + bottom nav, floating mini-player pill, full-screen swipe-up "Now Playing" sheet — matching the Android app's layout (mood chips, mood/genre grid, trending playlists, Now Playing screen with the squiggle play button).

By default it runs in **demo mode** — freely-licensed [SoundHelix](https://www.soundhelix.com) tracks with placeholder metadata, so it works with zero setup.

### Connecting real search/streaming

Set `API_BASE` near the top of the `<script>` block in `index.html`:
```js
const API_BASE = "https://your-deployed-oli-web-api.example.com";
```
That's it — search, thumbnails, and playback all switch to hitting [`oli-web-api`](https://github.com/oli-music/oli-web-api) automatically. Demo tracks still work as a fallback ("Quick picks" stays populated even with a live backend configured).

### What's still demo-only even with a backend connected

- **Lyrics** — there's no lyrics API wired up yet; real (non-demo) tracks show an honest "no synced lyrics yet" instead of fake timed lines.
- **Mood chips / genre tiles / trending row** — these trigger a real search for their label as a query, but aren't backed by curated playlists or an actual charts API.
- **Download button** in the mobile Now Playing sheet — points users to the native apps, since offline storage isn't something a web page can reasonably do.

## Deploying

Static hosting works fine — GitHub Pages, Netlify, Vercel, Cloudflare Pages, etc. Keep all `.html` files in the same directory, since the pages link to each other with relative paths.

## Credits

Oli is a rebranded fork of the Echo Music project family, created by Aditya Yadav ([@iad1tya](https://github.com/iad1tya)), GPL-3.0 licensed. See the [oli](https://github.com/oli-music/oli) Android repo for full credits.

## License

GPL-3.0 — see [LICENSE](LICENSE).

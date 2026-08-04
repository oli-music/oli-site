# Oli Site

The marketing site for **Oli** — a free, ad-free music player with synced lyrics and offline playback.

This is a rebrand of [Echo Music Site](https://github.com/EchoMusicApp/Echo-Music-Site) (design and copy rewritten from scratch, not a copy of the original files) — see [Credits](#credits).

## Pages

| File | Purpose |
|---|---|
| `index.html` | The site — hero, feature grid, platform downloads (Android/Desktop/Source), FAQ |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |

No build step — plain HTML/CSS/vanilla JS, no dependencies beyond Google Fonts. Open `index.html` directly, or serve the folder with any static file server.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Design

Warm, musical visual identity — a spinning vinyl record in the hero, an animated waveform divider, and a scrolling equalizer motif in the closing CTA band. Deep violet/black background with amber and teal accents; Fraunces serif for display type, Inter for body text.

All download links point at the real GitHub release pages for [`oli`](https://github.com/oli-music/oli/releases) (Android) and [`oli-desktop`](https://github.com/oli-music/oli-desktop/releases) (Windows/macOS/Linux).

## Why this is marketing-only

Earlier versions of this repo included a full in-browser player (search, playback, library, equalizer) backed by a companion API. That approach hit a hard wall: YouTube's search/streaming endpoints don't send the CORS headers needed for direct browser-to-YouTube requests, and the backend-proxy alternative ran into YouTube's bot-detection on cloud-hosted IPs. Rather than ship something unreliable, this site now does what it's actually good at — pointing people to the real apps.

## Deploying

Static hosting works fine — GitHub Pages, Netlify, Vercel, Cloudflare Pages, etc.

## Credits

Oli is a rebranded fork of the Echo Music project family, created by Aditya Yadav ([@iad1tya](https://github.com/iad1tya)), GPL-3.0 licensed. See the [oli](https://github.com/oli-music/oli) Android repo for full credits.

## License

GPL-3.0 — see [LICENSE](LICENSE).

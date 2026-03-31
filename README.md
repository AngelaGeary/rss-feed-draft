# Accessible RSS Reader

A fully accessible, speech-enabled RSS reader built as a single HTML file. Designed from the ground up for blind and visually impaired users, with full keyboard navigation, screen reader support, and built-in text-to-speech.

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)
![Single File](https://img.shields.io/badge/size-single%20HTML%20file-orange.svg)

## Why?

Most RSS readers treat accessibility as an afterthought. This one was built for it. No frameworks, no build step, no dependencies — just open the HTML file in a browser and start reading.

It was built with and for a blind user during a conversation about the lack of accessible RSS readers, particularly ones that work well with speech output rather than just tolerating screen readers.

## Features

### Accessibility
- **Full keyboard navigation** — arrow keys to browse lists, Enter to open, Escape to go back, Tab to move between sections
- **Built-in text-to-speech** — toggle speech on and the reader speaks everything: article titles as you browse, full article content when you open one
- **Female voice preference** — automatically selects a friendly female voice (Samantha, Zira, Karen, etc.) from your system's available voices
- **Screen reader compatible** — proper ARIA roles, live regions, landmarks, and labels throughout
- **Three themes** — Dark, Light, and High Contrast (black/white/yellow)
- **Atkinson Hyperlegible font** — designed specifically for low-vision readability
- **Skip-to-content link** — for quick navigation past the header

### Reading
- **Digest view** — the latest 3 articles from every subscribed feed, sorted newest-first, all in one place
- **"Read Headlines" button** — reads all digest headlines aloud in sequence
- **Auto-read on open** — when speech is enabled, articles are read aloud automatically when opened
- **Chunked speech engine** — long articles are split into safe chunks to work around Chrome's speech synthesis bugs
- **Paywall/truncated detection** — articles with very little content are flagged with a "Preview" badge and a warning banner
- **"Open original article" link** — always available at the bottom of every article

### Feed Discovery
- **Keyword search** — type "theology", "cooking", "accessibility", etc. to find feeds from a curated directory plus live Google News RSS topic feeds
- **Website discovery** — enter any URL (e.g. `evangelical-times.org`) and the reader will probe for RSS feeds using the Feedsearch API and common feed paths
- **Add by URL** — paste any RSS or Atom feed URL directly
- **Curated directory** — ~35 feeds covering news, technology, accessibility, Christian/theology, Irish news, cooking, science, and more

### Technical
- **Zero dependencies** — single HTML file, no build step, no npm, no frameworks
- **Multi-strategy feed fetching** — tries rss2json API → allorigins CORS proxy → direct fetch, with full client-side RSS/Atom XML parsing as fallback
- **Persistent subscriptions** — feeds are saved to localStorage
- **Works with Ghost, WordPress, Blogger, Substack** — any standard RSS or Atom feed

## Quick Start

1. Download `accessible-rss-reader.html`
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. Press the **speech toggle button** (🔈) or press **S** to enable speech
4. Go to the **Find Feeds** tab and search for topics or websites
5. Subscribe to feeds, then return to the **Digest** tab

That's it. No installation, no accounts, no server.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Tab` / `Shift+Tab` | Move between elements |
| `↑` / `↓` | Browse through feed/article lists |
| `←` / `→` | Switch between tabs |
| `Enter` | Open selected item |
| `Escape` | Go back / close dialog |
| `S` | Toggle speech on/off |
| `R` | Read current article aloud |
| `X` | Stop reading |
| `N` | Next article |
| `P` | Previous article |
| `D` | Go to Digest tab |
| `/` | Focus search field |
| `?` | Show keyboard shortcuts help |
| `Delete` | Remove selected feed |

## Speech Engine

The Web Speech API is unreliable across browsers. This reader includes a hardened speech engine that handles the known issues:

- **Chunked utterances** — text is split at sentence boundaries into ~180-character chunks to prevent Chrome's silent cutoff bug
- **Pause/resume watchdog** — a background timer nudges Chrome every 5 seconds to prevent the speech engine from freezing
- **Voice readiness waiting** — retries voice loading up to 10 times on startup, since voices load asynchronously
- **Queue system** — speech requests are queued and processed sequentially; new requests cleanly cancel old ones
- **Timeout safety** — each chunk has a maximum duration; if something gets stuck, it moves on

## Feed Compatibility

The reader supports standard RSS 2.0, RSS 1.0, and Atom feeds. It has been tested with:

- **Ghost** blogs (`/rss/`)
- **WordPress** sites (`/feed/`)
- **Blogger** / Blogspot
- **Substack** newsletters
- **BBC**, **NPR**, **The Guardian**, and other major news outlets
- **Podcast feeds** (RSS with enclosures)
- **Google News** topic RSS feeds

### Ghost Blogs

Ghost sites serve their RSS at `https://yourblog.com/rss/`. Tag-specific feeds are at `/tag/tag-name/rss/` and author feeds at `/author/name/rss/`.

## Themes

| Theme | Best for |
|-------|----------|
| **Dark** (default) | Comfortable reading, reduced eye strain |
| **Light** | Bright environments, users who prefer light backgrounds |
| **High Contrast** | Maximum readability — pure black background, white text, yellow accents. Meets WCAG AAA contrast requirements |

## Limitations

- **CORS restrictions** — some feeds can't be loaded because the feed server doesn't allow cross-origin requests and the CORS proxy can't reach them. The multi-strategy approach handles most cases but not all.
- **rss2json rate limits** — the free tier of the rss2json API has usage limits. The reader falls back to the CORS proxy when this happens.
- **Browser speech quality varies** — the available voices and speech quality depend entirely on your operating system and browser. macOS/iOS generally has the best voices; Windows and Linux are more limited.
- **No sync** — subscriptions are stored in localStorage only. They don't sync between devices or browsers.
- **Feed search directory is curated** — keyword search matches against a built-in list of ~35 feeds plus Google News. It doesn't search the entire web for feeds (use the URL discovery feature for that).

## Browser Support

| Browser | Status |
|---------|--------|
| Chrome / Edge | ✅ Full support (speech engine includes Chrome-specific workarounds) |
| Firefox | ✅ Full support |
| Safari | ✅ Full support (best voice quality on macOS) |
| Mobile Safari | ✅ Works with VoiceOver |
| Chrome Android | ✅ Works with TalkBack |

## Contributing

Contributions are welcome, especially around:

- **More curated feeds** for the search directory
- **Better feed discovery** strategies
- **Localisation** — the interface is English-only currently
- **OPML import/export** — for migrating from other readers
- **Improved paywall detection** heuristics
- **Testing with specific screen readers** (JAWS, NVDA, VoiceOver, TalkBack, Orca)

## License

MIT — do whatever you like with it.

## Credits

- [Atkinson Hyperlegible](https://brailleinstitute.org/freefont) font by the Braille Institute
- [Feedsearch API](https://feedsearch.dev/) for feed discovery
- [allorigins](https://allorigins.win/) for CORS proxying
- [rss2json](https://rss2json.com/) for RSS-to-JSON conversion
- Built during a conversation on [Claude](https://claude.ai) about accessible RSS readers

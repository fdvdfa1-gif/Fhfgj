# 日本 Nihon Diary

A free, mobile-first Japanese learning app that runs entirely in your browser. Learn kana, kanji, vocabulary and grammar from absolute beginner up to **JLPT N2**, with spaced repetition, native audio, daily quests and streaks.

No account. No ads. No backend. Your progress stays on your device.

> **Try it:** `https://<your-username>.github.io/<repo-name>/`
> *(replace with your GitHub Pages link)*

---

## Features

**Content**
- Hiragana and katakana with a memory mnemonic for every character
- About **5,300 vocabulary words** across JLPT N5 to N2, with example sentences
- About **1,000 kanji** with readings, meanings and stroke counts
- **120+ grammar points** with original example sentences
- Learning path in five stages: *Kana & first steps → N5 → N4 → N3 → N2*

**Learning**
- FSRS-style spaced repetition: items come back right before you would forget them
- Short lessons followed by a quiz, with configurable session sizes
- **Blitz mode:** a 60-second timed round on items you already know
- **Album:** every learned item lights up, and turns gold once it is in long-term memory (21+ day interval)
- Native-speaker audio for words, with automatic fallbacks (see [Audio](#audio))

**Motivation**
- XP, levels and rank titles (*Beginner → Apprentice → Traveler → Scholar → Adept*)
- Daily streaks, streak milestones and buyable streak freezes
- Daily quests, a daily XP goal and a reward chest
- 20+ badges and a 14-day activity chart

---

## Install

Nihon Diary is a Progressive Web App (PWA), so there is nothing to download from an app store.

**Android (Chrome)**
1. Open the app link above.
2. Tap **⋮ → Install app** (or **Add to Home screen**).

**iPhone / iPad (Safari)**
1. Open the app link above.
2. Tap **Share → Add to Home Screen**.

**Desktop**
Just open the link in any modern browser. In Chrome or Edge you can also click the install icon in the address bar.

---

## Audio

The app plays Japanese audio using three sources, in this order:

1. **Bundled clips:** native-speaker recordings and generated voice packs shipped with the app (`v*.bin`, `t*.bin`)
2. **Your device's Japanese voice**, if it has one installed
3. **Online voice** as a last resort. This can be switched off in settings

Voice packs are only cached once they have been played or downloaded. To hear audio with no connection, go to **Me → Settings → Save voices for offline → Download** while you are online.

---

## Offline use

After your first visit, the app opens and runs without internet. A service worker (`sw.js`) handles this:

- **App files** (`index.html`, manifest, icons) are cached on install. They load instantly from the cache and refresh quietly in the background, so an update appears the next time you open the app after it has been fetched.
- **Voice packs** (`.bin`) never change, so they are served from the cache first and fetched only once.
- The **online voice** fallback is never cached and needs a connection.

Offline mode needs the app to be served over HTTPS (GitHub Pages is fine) or `localhost`. Service workers do not run on `file://` pages.

---

## Your data

- Progress is stored in your browser's `localStorage` (key: `nd:state:v2`).
- Phones can clear browser storage when space runs low, so use **Me → Settings → Backup or restore** to copy a backup code and keep it somewhere safe.
- To move to another device, paste your backup code into **Restore** on the new device.
- **Erase all progress** is available in the same settings screen.

### Privacy

Nothing is sent to any server by the app itself, and there is no analytics or tracking. The one exception is the optional **online voice** fallback: if it is enabled and no clip or device voice is available, the text to be spoken is sent to Google Translate's text-to-speech endpoint. Turn **Online voice** off in settings to prevent this.

---

## Run locally

There is no build step and there are no dependencies.

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
python -m http.server 8000
```

Then open <http://localhost:8000>.

Serve it over `http://` or `https://` rather than double-clicking `index.html`. The service worker and the audio packs are loaded with `fetch`, which browsers restrict on `file://` pages.

---

## Deploy to GitHub Pages

1. Push all the files above to your repository.
2. Go to **Settings → Pages**, set the source to your main branch and the root folder, and save.
3. After a minute or two the app is live at `https://<your-username>.github.io/<repo-name>/`.

### Publishing an update

Whenever you change `index.html` (or any cached file), open `sw.js` and bump the version at the top:

```js
const CACHE = 'nd-cache-v7'; // was v6
```

Without this, phones keep serving the old cached copy. Note that bumping the version also clears cached voice packs, so users will need to tap **Save voices for offline** again if they want them stored.

---

## Project structure

```
├── index.html            # The whole app: UI, logic, and all learning content
├── manifest.webmanifest  # PWA manifest (name, colors, icons)
├── sw.js                 # Service worker for offline use
├── icon-192.png          # App icons
├── icon-512.png
├── v1.bin … v6.bin       # Native-speaker word audio packs
└── t1.bin … t6.bin       # Generated voice packs for other words, kanji and sentences
```

The vocabulary, kanji and grammar lists live in the `DATA` object near the top of the script in `index.html`. Everything else is plain HTML, CSS and vanilla JavaScript.

---

## Contributing

Bug reports, typo fixes and content corrections are welcome. Open an issue or a pull request.

When reporting a problem, please include your device, browser and a short description of what happened.

---

## Credits and licenses

Nihon Diary stands on the shoulders of open data. Thank you to everyone below.

| What | Source | License |
|---|---|---|
| Native word recordings | [Tofugu / WaniKani](https://www.wanikani.com) | CC BY-SA 4.0 |
| Generated voice (other words, kanji, sentences) | Open JTalk voice *tohoku-f01*, Tohoku University | CC BY 4.0 |
| Vocabulary | [open-anki-jlpt-decks](https://github.com/jamsinclair/open-anki-jlpt-decks), built on Jonathan Waller's JLPT lists ([tanos.co.uk](https://www.tanos.co.uk/jlpt/)) | MIT |
| Dictionary data | [JMdict](https://www.edrdg.org/jmdict/j_jmdict.html), EDRDG | CC BY-SA 4.0 |
| Kanji | [kanji-data](https://github.com/davidluzgouveia/kanji-data), based on KANJIDIC (EDRDG) | MIT / CC BY-SA 4.0 |
| Vocabulary example sentences | Tanaka Corpus (now on [Tatoeba](https://tatoeba.org)), via [odashi/small_parallel_enja](https://github.com/odashi/small_parallel_enja) | Public domain / CC BY |
| Grammar points and example sentences | Original to this project | |

**Notes**
- The JLPT publishes no official grammar list, so grammar levels are approximate.
- The spacing algorithm is an FSRS-style model, not an official FSRS implementation.
- Nihon Diary is an independent project and is not affiliated with or endorsed by the JLPT, WaniKani or Tofugu.

<!-- Add your own LICENSE for the app code here, e.g. MIT. -->

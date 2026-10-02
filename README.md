# Nihon Diary

Personal Japanese study app (kana, JLPT N5 to N2 vocabulary, kanji and grammar).
Static site: no build step, no server, no accounts. Progress is stored in the browser.

## Files
- `index.html` the whole app
- `manifest.webmanifest`, `icon-192.png`, `icon-512.png` make it installable
- `sw.js` offline support (bump `CACHE` inside it after changing `index.html`)
- `v1.bin` ... `v6.bin` voice packs (about 8.7 MB total)

## Voices
1. Bundled native-speaker clips for about 2,600 words (used first).
2. The phone's own Japanese voice, if it has one.
3. Online voice fallback (can be switched off in Me > Settings).

## Credits
Word recordings: Tofugu / WaniKani, licensed CC BY-SA 4.0
(https://github.com/tofugu/japanese-vocabulary-pronunciation-audio).
Re-encoded to mono 32 kbps and bundled into packs; no other changes.
Vocabulary: open-anki-jlpt-decks (MIT), built on JLPT lists by Jonathan Waller
and the JMdict dictionary. Kanji data: KANJIDIC.

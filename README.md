# Nihon Diary

Personal Japanese study app (kana, JLPT N5 to N2 vocabulary, kanji and grammar).
Static site: no build step, no server, no accounts. Progress is stored in the browser.

## Files
- `index.html` the whole app
- `manifest.webmanifest`, `icon-192.png`, `icon-512.png` make it installable
- `sw.js` offline support (bump `CACHE` inside it after changing `index.html`)
- `v1.bin` ... `v6.bin` native-speaker word clips, `t1.bin` ... `t6.bin` synthesized clips

## Voices
Every word, kana, kanji and sentence has audio.
1. Native-speaker clips for about 2,600 words (used first).
2. Synthesized clips for everything else.
3. The phone's own Japanese voice or an online voice, only as a last resort.

## Credits and licenses
See LICENSES.txt.

# Hifz Repeater — حِفْظ

A single-file web tool for Quran memorisation, built on the method used for fourteen centuries: hear the recitation from a teacher (**Talaqqi**), repeat each ayah until it settles (**Takrar**), then veil the page and recite from memory (**Hifz**).

Everything — landing page and tool — lives in one HTML file with no build step, no dependencies to install, and no backend. Open it in any browser on any device.

## What it does

You pick a surah and an ayah range (or the whole surah), choose a reciter and optionally an English translation, and load the passage. The exact Uthmani mushaf text renders on a parchment-styled page. From there:

- **Listen on a loop.** The audio engine plays per-ayah recordings in two modes: *read through* (each ayah once, in order — the classic sabaq listening pattern) or *repeat each ayah* 3, 5, 7, or 10 times before advancing. An optional passage loop restarts the whole range when it ends. The ayah currently being recited is highlighted in gold.
- **Veil the page.** One tap blurs the ink while the page stays in front of you. While veiled, tapping any single ayah peeks at just that one — the way a teacher lets a student glance at one word, never the whole page. Tap again to re-veil it.
- **Read the meaning.** With a translation selected, the English appears beneath each ayah and is veiled along with the Arabic, so it can't quietly do your recall for you.

## Reciters

Audio comes from two sources, handled transparently by the tool.

**Classical / Teaching** (Quran.com per-ayah API)
- Mahmoud Khalil al-Husary
- Husary — Mu'allim (the slow teaching-pace recording made for tajweed students)
- AbdulBaset AbdulSamad (Murattal)
- Mohamed Siddiq al-Minshawi

**Contemporary**
- Mishari Rashid al-Afasy *(Quran.com)*
- Saud ash-Shuraym *(Quran.com)*
- Abdur-Rahman as-Sudais *(Quran.com)*
- Maher al-Muaiqly *(EveryAyah CDN)*
- Saad al-Ghamdi *(EveryAyah CDN)*

> Idris Abkar and Abdul Rashid Sufi are not included because no free source offers their recitations as verse-by-verse audio files — only full-surah recordings, which the per-ayah repeat engine cannot use. If a per-ayah source appears, adding a reciter is a one-line change (see below).

## Translations

- Saheeh International
- M.A.S. Abdel Haleem
- Al-Hilali & Khan
- T. Usmani

Footnote markers are stripped automatically.

## How to use it

1. Open `hifz.html` in a browser (double-click locally, or host it — see below).
2. Scroll past the landing page or tap **Open the tool**.
3. Choose a surah, set the ayah range — or tick **Whole surah**.
4. Pick a reciter and (optionally) a translation, then **Load passage**.
5. Press **Play**. Set the mode (read through / repeat ×N) and the **Loop the passage** toggle in the player bar.
6. When the sound is familiar, press **Hide** and recite. Tap an ayah to peek if you get stuck.

A suggested session: load the passage → *read through + loop* a few cycles while following the text → switch to *repeat 5×* and recite along → **Hide** and recite from memory, peeking only where needed.

## Technical notes

- **Text:** Uthmani script from `api.quran.com/api/v4/quran/verses/uthmani` (one request per chapter).
- **Audio:** per-ayah MP3s. Quran.com reciters resolve via the bulk endpoint `recitations/{id}/by_chapter/{n}?per_page=300` — a single request even for Al-Baqarah's 286 ayat (full surah with translation loads in ~1.3 s). EveryAyah reciters need no lookup at all; URLs follow the pattern `everyayah.com/data/{folder}/{SSS}{AAA}.mp3`.
- **Translations:** `quran/translations/{id}?chapter_number={n}`, indexed by ayah number.
- **Adding a reciter:** add one `<option>` to the reciter select. Value `q:{recitation_id}` for Quran.com, or `e:{folder_name}` for an EveryAyah folder.
- **Frontend:** vanilla JS, GSAP + ScrollTrigger (cdnjs) for the landing animations. The landing motion fully respects `prefers-reduced-motion` and the page works with JavaScript animation disabled. Fonts: Amiri Quran (Arabic), Fraunces and Figtree (Latin), via Google Fonts.
- **Broken audio handling:** if a single MP3 fails to load mid-session, the player skips to the next ayah instead of stalling.

## Hosting

It's one file. Any static host works:

- **GitHub Pages:** push `hifz.html` to a repo, enable Pages, done.
- **Netlify / Vercel / Cloudflare Pages:** drag and drop.
- **Locally:** just open the file. (An internet connection is still required — text and audio are fetched live.)

Tip: rename it `index.html` if you want it served at the root of a domain.

## Known limitations

- **Online only.** Nothing is cached; every load fetches live. An offline mode (Service Worker caching the passage you're working on) is the most natural next feature.
- **First play needs a tap.** Mobile browsers block autoplay; the first Play press must be a user gesture. The tool surfaces a clear message if this happens.
- **No progress tracking.** The tool deliberately holds no state between sessions — your memorisation log stays with you and your teacher.

## Credits

- Quranic text and recitations served live by [Quran.com](https://quran.com) (QuranFoundation API) and [EveryAyah.com](https://everyayah.com).
- Built as a study aid — your teacher remains your teacher.



# Hifz Repeater

**A single-file web tool for Quran memorisation — built on the method used for fourteen centuries.**

Hear it from a reciter · Repeat it until it settles · Veil the page and recite

<br>

![Single file](https://img.shields.io/badge/single_file-no_build_step-c8a14b?style=flat-square&labelColor=0c1e16)
![Vanilla JS](https://img.shields.io/badge/vanilla_JS-zero_dependencies-c8a14b?style=flat-square&labelColor=0c1e16)
![GSAP](https://img.shields.io/badge/motion-GSAP_+_ScrollTrigger-c8a14b?style=flat-square&labelColor=0c1e16)
![API](https://img.shields.io/badge/text_&_audio-Quran.com_API-c8a14b?style=flat-square&labelColor=0c1e16)
![Mobile](https://img.shields.io/badge/mobile-first-c8a14b?style=flat-square&labelColor=0c1e16)

<br>

<img src="assets/hero.png" alt="Landing page — Al-Qamar 54:17 unveiling over a hand-drawn rub el hizb" width="92%">

</div>

<br>

## ✦ The idea in one image

The page stays in front of you. The ink does not.

<div align="center">
<img src="assets/page-veiled.png" alt="Al-Fatihah veiled — only the first ayah peeked into focus" width="86%">
</div>

One tap blurs every ayah so you can recite from memory. Stuck on a single verse? **Tap it to peek** — only that one sharpens, the way a teacher lets a student glance at one word, never the whole page. Tap again and the veil returns.

<br>

## ✦ The method

Nothing new. That is the point.

```mermaid
flowchart LR
    A["تَلَقِّي<br><b>Talaqqi</b><br>receive it from a reciter"] --> B["تَكْرَار<br><b>Takrar</b><br>repeat each ayah until it holds"]
    B --> C["حِفْظ<br><b>Hifz</b><br>veil the page and recite"]
    C -.->|the passage loops| A
    style A fill:#12291e,stroke:#c8a14b,color:#f3ead3
    style B fill:#12291e,stroke:#c8a14b,color:#f3ead3
    style C fill:#12291e,stroke:#c8a14b,color:#f3ead3
```

| | Mode | What it does |
|---|---|---|
| 🎧 | **Read through** | Plays the passage ayah by ayah, start to finish — the classic *sabaq* listening pass |
| 🔁 | **Repeat ×3 / ×5 / ×7 / ×10** | Drills one ayah on a loop before advancing to the next |
| ♾ | **Loop the passage** | Restarts the whole range when it ends — combine with either mode |
| 👆 | **Veil & peek** | Blur everything; reveal one ayah at a time, on your terms |

<br>

## ✦ The page itself

Exact **Uthmani mushaf script**, served live from the Quran.com API, set in a Quranic typeface on a parchment page — with the ayah currently being recited highlighted in gold.

<div align="center">
<table>
<tr>
<td align="center" width="50%">
<img src="assets/page-arabic.png" alt="Flowing mushaf layout, Arabic only"><br>
<sub><b>Arabic only</b> — flowing mushaf layout</sub>
</td>
<td align="center" width="50%">
<img src="assets/page-translation.png" alt="Verse-by-verse layout with English translation beneath each ayah"><br>
<sub><b>With translation</b> — veiled along with the Arabic</sub>
</td>
</tr>
</table>
</div>

<br>

## ✦ Built for the phone in your hand

Memorisation happens before Fajr, on commutes, between things — so the whole experience is mobile-first: stacked controls, thumb-sized targets, a sticky player that follows you down the page.

<div align="center">
<table>
<tr>
<td align="center"><img src="assets/mobile-hero.png" alt="Mobile landing" width="260"></td>
<td align="center"><img src="assets/mobile-tool.png" alt="Mobile tool with passage loaded" width="260"></td>
</tr>
</table>
</div>

<br>

## ✦ Nine reciters, four translations

| Classical / Teaching | Source | Contemporary | Source |
|---|---|---|---|
| Mahmoud Khalil al-Husary | Quran.com | Mishari Rashid al-Afasy | Quran.com |
| Husary — **Mu'allim** *(teaching pace)* | Quran.com | Saud ash-Shuraym | Quran.com |
| AbdulBaset AbdulSamad (Murattal) | Quran.com | Abdur-Rahman as-Sudais | Quran.com |
| Mohamed Siddiq al-Minshawi | Quran.com | Maher al-Muaiqly | EveryAyah |
| | | Saad al-Ghamdi | EveryAyah |

**Translations:** Saheeh International · M.A.S. Abdel Haleem · Al-Hilali & Khan · T. Usmani — shown beneath each ayah and veiled with it, so the English can't quietly do your recall for you.


<br>

## ✦ Quick start

```
1. Open hifz.html in any browser          (double-click, or host it anywhere)
2. Tap "Open the tool"
3. Pick a surah · set the ayah range · or tick ☑ Whole surah
4. Choose a reciter and (optionally) a translation → Load passage
5. Press ▶ Play — set the mode and loop in the player bar
6. When the sound is familiar: Hide → recite → peek only where stuck
```

**A suggested session:** *read through + loop* a few cycles while following the text → switch to *repeat ×5* and recite along → **Hide** and recite from memory.

<br>

## ✦ How it works

```mermaid
flowchart TB
    subgraph file["hifz.html — one file, no build"]
        L["Landing<br><i>GSAP unveiling, rub el hizb line-work</i>"]
        T["Tool<br><i>vanilla JS, single &lt;audio&gt; element</i>"]
    end
    T -->|"1 request / chapter"| TXT["Quran.com<br>Uthmani text"]
    T -->|"1 request / chapter"| TR["Quran.com<br>translations"]
    T -->|"1 bulk request / chapter"| AQ["Quran.com<br>per-ayah audio"]
    T -->|"constructed URLs, zero lookups"| AE["EveryAyah CDN<br>per-ayah audio"]
    style file fill:#0c1e16,stroke:#c8a14b,color:#f3ead3
    style TXT fill:#12291e,stroke:#87a093,color:#e9f0ea
    style TR fill:#12291e,stroke:#87a093,color:#e9f0ea
    style AQ fill:#12291e,stroke:#87a093,color:#e9f0ea
    style AE fill:#12291e,stroke:#87a093,color:#e9f0ea
```

- **Bulk audio resolution.** Quran.com reciters resolve through `recitations/{id}/by_chapter/{n}?per_page=300` — one request even for Al-Baqarah. Measured result: **all 286 ayat, with translation, loaded in 1.3 s**.
- **EveryAyah needs no lookup at all** — URLs follow `everyayah.com/data/{folder}/{SSS}{AAA}.mp3`.
- **Resilient playback.** A broken MP3 mid-session skips to the next ayah instead of stalling.
- **Adding a reciter is one line** — a new `<option>` in the reciter select:

```html
<option value="q:6">…</option>                      <!-- q:{recitation_id}  → Quran.com -->
<option value="e:Ghamadi_40kbps">…</option>          <!-- e:{folder_name}    → EveryAyah -->
```

- **Motion that knows when to stop.** GSAP + ScrollTrigger drive the landing's blur-to-sharp "unveiling" language; `prefers-reduced-motion` disables all of it and the page remains fully usable.
- **Fonts:** Amiri Quran (Arabic) · Fraunces + Figtree (Latin), via Google Fonts.

<br>

## ✦ Hosting

It is one file. Any static host works.

| Host | How |
|---|---|
| **GitHub Pages** | Push, enable Pages, done |
| **Netlify / Vercel / Cloudflare** | Drag and drop |
| **Locally** | Just open the file *(internet still required — text and audio are fetched live)* |

Rename to `index.html` to serve it at the root of a domain.

<br>

## ✦ Known limitations & roadmap

- **Online only.** Nothing is cached. A Service Worker that caches *the passage you're working on* for offline pre-Fajr sessions is the natural next feature.
- **First play needs a tap** — mobile browsers block autoplay; the tool surfaces a clear message when it happens.
- **No progress tracking — by design.** The tool holds no state between sessions. Your memorisation log stays with you and your teacher.

<br>

---

<div align="center">

Quranic text and recitations served live by **[Quran.com](https://quran.com)** and **[EveryAyah.com](https://everyayah.com)**

*Built as a study aid — your teacher remains your teacher.*

<sub>﴿ فَلَقَدْ يَسَّرْنَا الْقُرْآنَ لِلذِّكْرِ فَهَلْ مِن مُّدَّكِرٍ ﴾</sub>

</div>

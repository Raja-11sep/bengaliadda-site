# bengaliadda.in source

**Hidden while being built:** `HIDDEN = True` in `_src/build.py` asks search engines not to list any page (robots.txt + a noindex tag). At launch set it to `False`, add the new Instagram/Facebook (`INSTAGRAM_URL`, `INSTAGRAM_HANDLE`, `FACEBOOK_URL`) and the new e-mail (`EMAIL`), run `build.py`, upload.

The website is plain HTML/CSS/JS built by a small Python script. This `_src` folder is **not published**:
GitHub Pages skips folders whose name starts with `_`.

## Rebuild

```
pip install qrcode pillow
python3 _src/build.py
```

This rewrites `index.html`, `download.html` and the four legal pages in the site folder.

| File | What it holds |
|---|---|
| `_src/build.py` | Page layouts, all home/download text (English + Bengali), header/footer, settings |
| `_src/art.py` | The SVG illustrations: the home picture's kites and stitched arch frame, the strings of mela lights (`festoon`), alpana border |
| `img/story-1.webp` … `story-6.webp` | The six pictures of the home page story ("A story of friendship"), also used on the Join us cards: 1600 x 900 photos (Nov 2026). To change one, save the new picture over it at 1600 x 900 (WebP), then run `build.py`. `_src/tools/make_story.py` made the older drawings; running it would paint over the photos |
| `story.js` | The story section. Wide screens: one sticky picture frame that cross-fades as each chapter scrolls past. Phones: the chapters are a row of cards to swipe through, with dots that follow. Without it each chapter shows its own picture card |
| `motion.js` | Home page motion: How it works (a thread sews from step to step, each number lights up, its phone wakes), Adda Tables (the cards are dealt, then the front card acts out asking for a seat), Questions (Bengali Adda "types" before each reply), and phones tilting toward the mouse. Off for visitors who ask for reduced motion |
| `music.js`, `audio/story-theme.mp3` | The site's music, on every page: our own recording of the Purano Sei Diner Kotha tune, made by `_src/tools/make_theme.py` (public-domain tune, so no licence needed). On by default: every page tries to start it, which browsers allow once the visitor has tapped anywhere on the site; otherwise their first tap starts it, and the floating button says "Tap for music" for a few seconds (once per visit). It carries on across pages, stops at once when the page is hidden (another app or tab, screen locked) and comes back after, has lock-screen controls, and "Pause music" is remembered. No fades on iPhones (pages can't change the volume there) |
| `match.js` | "Matched by what you share": the two circles drift together, shared answers fly into the overlap, the match % counts up; "Try someone else" matches you with the next person (`VENN_PEOPLE` in `build.py`) |
| `_src/tools/make_hero.py` | Paints the home page picture (friends on a Ganga ghat at sunset) into `img/hero-ghat.webp`. Run it, then `build.py`. Other looks: `dusk`, `morning` |
| `_src/pages/*.html` | Legal page bodies (privacy, terms, delete account, child safety) |
| `_src/tools/make_og.py` | Draws `og.png`, the picture shown when a bengaliadda.in link is shared (WhatsApp, Facebook, X): 1200 x 630, same look as the hero. Run it, then `build.py`; pages link it with `?v=`, so apps fetch the new picture. WhatsApp may still show its saved preview for a while: share `bengaliadda.in/?v=2` to see the new one at once |
| `_src/tools/make_app_screens.py` | Draws the four How it works screens (`img/app-welcome`, `app-looking-for`, `app-quiz`, `app-picks`.webp) in the app's new "Mela at dusk" look, which the app gets before the Play Store release. The picks photo is `_src/tools/picks-photo.webp`: already cropped, blurred and mirrored so no one can tell who it is. To use another photo: `python3 _src/tools/make_app_screens.py photo.jpg` (adjust `CROP` and `FACE` in the script); never commit the original. Run it, then `build.py` |
| `_src/tools/prep_screens.py` | Turns app screenshots into `img/app-*.webp` (cleans the status bar, blurs photos) | Once the app has the dusk look, real screenshots replace the drawn ones |
| `style.css`, `site.js`, `story.js`, `motion.js`, `music.js`, `match.js`, `download.js` | Styles and the small scripts (edited directly) |
| `fonts/` | Anek Bangla (headings) and Hind Siliguri (text), served from the site itself. `_src/tools/make_fonts.py` remakes them |

Settings at the top of `build.py`:

- `PLAY_URL`: set at the public launch. Every Download button then goes to Google Play, and `/download` redirects there.
- `APK_FILE`: where the website APK lives (`app/mon-mela.apk`).
- `UPDATED_EN` / `UPDATED_BN`: the "Last updated" date on the legal pages.

Links to `style.css` and the scripts carry `?v=<hash>`, so browsers fetch the new file as soon as it changes.

## Look

"A mela at dusk": deep-teal evening sections (hero, download page, closing panel, footer) with strings of
lights that switch on once when the page opens, and warm sections in between: paper, haldi yellow
(Adda Tables), terracotta clay like Bishnupur's temples (How it works), and mela night (Inside the app). Marigold is kept for
the "get the app" buttons. Colours, fonts and every section are described at the top of `style.css`.

## New app screenshots

Take them on an emulator with a debug build (release builds block screenshots). Use test accounts only.
Put them in a folder as `welcome.jpg`, `looking-for.jpg`, `quiz.jpg` and `picks.jpg`, then:

```
python3 _src/tools/prep_screens.py <that folder>
python3 _src/build.py
```

Raw screenshots are not stored here.

# brand-motion-design

A Claude Code skill that turns any brand into a showreel-grade motion film, in code: a product launch, a feature spotlight, a promo or offer, a brand teaser, social proof, an event, a before/after or a product showcase, as an Instagram Reel, a TikTok or a launch video. Give it a **brand book**, a **codebase**, a **website URL**, or nothing but a few answers (every question has a "you choose for me" option), plus any logo, photos, screenshots or recordings you have, and it makes a fast, dynamic cut: lit Three.js scenes with glossy materials, bloom and particles, a camera cut every two beats, giant slammed type, a colour flip on every chapter, a viewfinder HUD, cut to a generated hip-hop or punchy beat. It renders with [HyperFrames](https://github.com/heygen-com/hyperframes) (HTML to video, Apache 2.0) and keeps the brand's own colours, fonts, logo, voice and claims.

Fast is the default: it never asks "calm or catchy?". A calm explainer is made only if you ask for one.

Based on [product-film](https://github.com/Rieranthony/product-film-skill) by Anthony Riera (MIT), ported from Remotion to HyperFrames and rebuilt around the showreel cut.

## What's new in this edition

- **For any brand, even without a brand book.** No brand files? It asks a few questions with AskUserQuestion (colours, type, tone, audience), each with "You choose for me", and shows its picks as style frames.
- **It remembers.** The brand, your standing choices (format, music, tone, language) and your notes on each film live in `videos/BRAND.md`; the next film reuses them and only asks what is new.
- **Nine video types.** Launch, feature spotlight, promo / offer, brand teaser, social proof, event, before/after, product showcase, and an explainer on request, each with its own chapters and ending (`reference/video-types.md`).
- **Your assets.** Logo (SVG or PNG), product photos and cut-outs as lit 3D cards, screenshots, screen recordings, footage, your song or a voiceover (`reference/assets.md`). Prices, dates and reviews are used word for word, never invented.
- **Brand, codebase or URL in, film out.** A brand folder or a repo is read as law; a bare URL goes through `hyperframes capture` (screenshots, colour and type tokens, page text, fonts, SVGs), and a blocked capture stops instead of guessing.
- **Always a showreel.** A 12-bar shape at 140 BPM: cold open, the problem as a picture, the drop, the fix, the payoff, the logo lockup. A new picture every 2 beats, under twenty words on screen.
- **Rich 3D, not CAD blocks.** `kit/three.js` gives an environment-lit stage with bloom (only the accent glows), glossy, glass and satin materials, colour ramps inside the palette, fog, particles, curves that draw themselves, cards and stickers in exact brand colours, and camera shots that cut on the beat with drift. The recipe that separates a flat cut from a rich one is written down in `reference/showreel.md`.
- **Brand moment rules.** Pace, light, depth and transitions go bold; palette, logo, fonts, voice, claims and correctness never bend.
- **HyperFrames instead of Remotion.** Plain HTML, CSS and JS; no React build, no company license. Editable in HyperFrames Studio.
- **One clock, pure frames.** `PF.film` drives a `draw(t)` from HyperFrames' seekable timeline, so every frame (3D included) is a function of time.
- **Music without a license problem.** `synth.py` generates a royalty-free beat on an exact grid: hip-hop / trap with 808 glides by default, punchy electronic, or a soft bed; impacts, risers and a breath before the drop. Sound effects land on their frames (`place-audio.mjs`).
- **One beat sheet for everything.** `cues.js` is read by the film and by every script: the readable beat sheet, review stills by bar and beat, audio placement, render names.
- **Social formats.** 9:16 by default, safe zones in debug stills, loudness targets for Reels, TikTok and Shorts.
- **Stronger verification.** HyperFrames `check` (text crossing text, contrast, overflow) in the review loop; `verify.py` decodes the final files and checks duration, BT.709 tags, colours, loudness and true peak.
- **Math, Arabic, charts.** KaTeX on demand, right-to-left text, function plots and 3D fields that settle onto a function.
- **Offline renders.** GSAP, Three.js (and KaTeX) are vendored into the project; nothing loads from a CDN at render time.
- **Traps found while validating** on a real brand (four iterations of a social cut) are written into `SKILL.md`.

## Install

In Claude Code:

```
/plugin marketplace add ouerf-man/brand-motion-design-skill
/plugin install brand-motion-design@brand-motion-design-skill
```

Or copy the skill folder by hand:

```bash
git clone https://github.com/ouerf-man/brand-motion-design-skill
mkdir -p ~/.claude/skills
cp -R brand-motion-design-skill/plugins/brand-motion-design/skills/brand-motion-design ~/.claude/skills/
```

To share it with a team, commit that folder to your repo at `.claude/skills/brand-motion-design/`.

Optional, recommended: the official HyperFrames skills, which this one builds on (`npx hyperframes skills update`).

## Use

In your product's repo, ask Claude Code for the film:

> Make a 20 second Instagram Reel for this product.

> Make a 30 second launch video, with this song.

> Here is our website: https://example.com. Make a 20 second Reel.

> Use the brand folder in `brand/` and make a launch promo, like this reference video.

> I run a bakery, here's my logo and three photos. Make a 15 second Reel for our weekend offer: 2 croissants for 3 €.

The skill takes it from there:

1. **Discovery.** Your saved profile if there is one, then your brand folder, repo or captured website: palette, fonts, logo, the accent, the brand's graphic pack, the voice and the claims rules.
2. **Interview (AskUserQuestion).** Brand questions only if nothing answers them; then the video type, where it plays and how long, the one message, the music, the facts it needs and the assets you have. Every question has "You choose for me". Never the pace.
3. **Brand kit and story.** `videos/BRAND.md` (what bends for video, what never does), a film prompt and a beat sheet (`cues.js`): 5 or 6 chapters, each with a 3D showpiece. It checks in with 3 style frames before building everything.
4. **Music.** A generated trap or punchy beat on an exact grid (or your song, measured and cut on bars), with each sound effect landing on its frame.
5. **Build.** One HyperFrames composition with a lit Three.js stage, DOM words and stickers, HUD and grain, every frame a function of time.
6. **Review.** Stills at every handoff (with measured boxes and safe zones in debug), the HyperFrames check, a draft render and a contact sheet. It fixes, then shows you.
7. **Final render.** A 240 fps master blended into 60 fps motion blur. You get an H.264 file with music, a muted loop or WebM if you want them, and a poster, all decoded and checked.
8. **Remember.** The film and your reactions go into the brand profile, so the next one starts where this one ended.

## What's inside

```
plugins/brand-motion-design/skills/brand-motion-design/
├── SKILL.md              the workflow, quality floor and traps
├── reference/            showreel (the default cut and 3D recipe), video-types, assets, discovery, interview, story, ingredients, engine, music, review, render, social
├── templates/
│   ├── BRAND.md          the brand profile: brand rules, owner choices, assets, films (reused next time)
│   ├── film-prompt.md    fill-in film brief
│   ├── index.html        starter composition
│   ├── cues.js           starter beat sheet
│   └── kit/              film (clock, grid, easing), motion (springs, moves, camera), words, draw, cursor, fx (showreel toolkit), three (lit 3D, bloom, shots, particles), debug
└── scripts/
    ├── setup.mjs         create the HyperFrames project, copy the kit, vendor GSAP/KaTeX/Three.js
    ├── synth.py          royalty-free music bed on an exact grid, and sound effects
    ├── beats.py          beat grid from a song (numpy)
    ├── audio-edit.py     cut a song on bars
    ├── place-audio.mjs   write the <audio> tags from the beat sheet
    ├── beat-sheet.mjs    the readable beat sheet, with a dead-bar check
    ├── stills.mjs        review stills by bar and beat, debug overlay
    ├── render.mjs        master, motion blur, deliverables (versioned)
    ├── verify.py         decode the files and check them
    └── cues-lib.mjs      shared: read cues.js in Node
```

## Requirements

- [Claude Code](https://claude.com/claude-code) (or another agent that runs skills and a shell).
- Node.js 22 or newer, and FFmpeg (HyperFrames needs both; `npx hyperframes doctor` checks).
- [uv](https://docs.astral.sh/uv/) for the Python scripts (numpy is pulled on demand).
- HyperFrames is installed per project by `npx hyperframes init` (Apache 2.0).
- Music you have the rights to use, or the generated bed.

## License

MIT, for the skill's own text and code. See [LICENSE](LICENSE). The original product-film skill is © Anthony Riera, MIT.

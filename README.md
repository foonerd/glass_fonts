# Glass fonts

The text faces [Glass](https://github.com/foonerd/glass) draws with: one family, PeppyFont, assembled from Google's Noto fonts so that a theme's title, artist and album rows read in every script that music metadata comes in. The family keeps its name, PeppyFont, because themes and player configurations refer to the files by it.

This repository was `peppy_fonts`. The old name still works: GitHub redirects links, clones and raw file URLs to it.

## What is here

- `fonts/PeppyFont-Light.ttf`, the light weight, for artist, album and smaller rows
- `fonts/PeppyFont-Regular.ttf`, the regular weight, for titles and general text
- `fonts/PeppyFont-Bold.ttf`, the bold weight, for emphasis
- `fonts/PeppyFont-Italic.ttf`, the italic

The italic uses the genuine Noto Sans Italic for Latin, Cyrillic and Greek. CJK and the per-script faces (Arabic, Hebrew, Devanagari, Bengali, Tamil, Thai, Georgian, Armenian) have no italic in Noto, and those scripts do not use one, so they fall back to their upright forms: full coverage, with real italics where they exist.

The seven-segment clock face, DSEG7, is not built here; Glass ships it in its own tree.

## How Glass uses them

When the Glass plugin is packaged, Light, Regular and Bold are fetched from this repository at a pinned commit and checked against their digests; Italic travels in the Glass repository itself. Together with DSEG7 they are Glass's built-in faces: a theme's `font.light`, `font.regular`, `font.bold` and `font.italic` styles are set in them unless the player says otherwise, and a character the chosen face lacks is taken from PeppyFont-Regular, so a theme set in a Latin-only face still shows a Japanese title.

On the player, the Appearance tab of the Glass Manager sets each style to the built-in face, to a font uploaded there, or to one of the player's own. Remotes bring the fonts from the player, so they draw the same.

## Script coverage

Music metadata in every major language:

- Latin (English, French, German, Spanish, Portuguese and the rest)
- Cyrillic (Russian, Ukrainian and the rest)
- Greek
- CJK: Chinese, Japanese, Korean (the IICore common subset)
- Arabic
- Hebrew
- Devanagari (Hindi, Marathi, Nepali)
- Bengali
- Tamil
- Thai
- Georgian
- Armenian

## Build

The fonts are built by the repository's GitHub Action with Google's fonttools (`pyftmerge`), which commits the four files under `fonts/` when they change. The Noto sources are downloaded from the Noto project at build time; no source font is kept here.

By hand:

```text
pip install fonttools cu2qu brotli
python scripts/build.py
```

The output lands in `fonts/`. `scripts/config.json` says which Noto faces go into each weight.

## Source

Every source face is from the Google Noto project: <https://github.com/notofonts>

## Licence

The output fonts are under the SIL Open Font License, Version 1.1, as the Noto sources require; see `LICENSE`. The build scripts are under GPL v3.

## Where they are used

- [Glass](https://github.com/foonerd/glass): the plugin package, the display and its remotes.
- PeppyMeter Screensaver and PeppyMeter Remote used them before Glass and keep fetching them under the old name.

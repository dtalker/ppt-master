# Media Embedding — Video & Audio (Step 7.4)

> `svg_to_pptx.py` builds **static** slides. It has **no** path for movies or audio.
> To get playable media (demo recordings, an opening song, interaction clips), use
> `scripts/embed_media.py` **after** the normal export (Step 7.3). Do **not**
> hand-roll `python-pptx add_movie` per project.

## Primary mode — named slots (no page numbers, no coordinates)

The user gives you a **file** and **which page** (in their words). You never make
them compute coordinates or count slides. The mechanism:

1. **Executor tags the placeholder rect** where the media sits, in the SVG:
   ```xml
   <rect data-media-slot="song" x="96" y="236" width="312" height="312" rx="20" fill="#13294A"/>
   ```
   A navy "screen" rect with a play button reads well and doubles as the fallback
   look in the static PDF. The rect's **slide** (its position in
   `sorted(svg_output/*.svg)`) and its **x/y/width/height** become the embed target.
   Keep it a clean ratio (16:9 → `width:540 height:304`; or square for a player).

2. **Attach a file to each slot** — one line each:
   ```bash
   python3 scripts/embed_media.py <project> --put song=assets/song.mp3 --put demo=assets/demo.mp4
   ```
   `embed_media.py <project>` with no `--put` prints the slots it found. Output is
   `exports/<name>_media.pptx`.

That's the whole contract: tag a rect → name it → drop a file on the name. Page
and coordinates are read from the SVG automatically.

> **Agent workflow:** when the user says "put this video on the 软件日抛 page", you
> map that description to the slot you tagged (e.g. `demo`) and run one `--put`.
> If the page wasn't tagged yet, add the `data-media-slot` attribute to that page's
> placeholder rect first (no re-export of media needed — just re-run 7.4).

## Hard-won gotchas (the script handles these)

1. **Audio embedded as audio frequently won't play in Keynote.** Any audio file is
   auto-wrapped into a still-poster `.mp4` (H.264 + AAC, ffmpeg) and embedded as a
   **video** — plays in Keynote *and* PowerPoint.
2. **There is no `add_audio` in python-pptx.** `add_movie` is the only embed API.
3. **Slide order == `sorted(svg_output/*.svg)`** — a filename's numeric prefix is
   not the slide number once you insert e.g. `01a_song.svg`. Slots sidestep this:
   the rect's real position is used.
4. **px→EMU** uses `slide_width / canvas_width` (canvas width from the spec_lock
   `viewBox`, default 1280) so the rect geometry lands exactly.

## Declaring slots in a manifest (instead of `--put`)

`media.json`:
```json
[
  {"slot": "song", "file": "assets/song.mp3"},
  {"slot": "demo", "file": "assets/demo.mp4", "poster": "assets/poster.jpg"}
]
```
`spec_lock.md` `## media`:
```
## media
- @song | assets/song.mp3
- @demo | assets/demo.mp4 | assets/poster.jpg
```

## Explicit page+coords mode (decks without slot tags)

Still supported when no `data-media-slot` exists:
```json
{"page": "P02", "file": "assets/song.mp3", "x":96, "y":236, "w":312, "h":312, "poster": "assets/player.png"}
```
- `page` = `P<NN>` (1-based slide position) or an svg basename.
- `x,y,w,h` in canvas pixels.

## Field reference

| Field | Meaning |
|---|---|
| `slot` | name of a `data-media-slot` rect → resolves page + geometry automatically. |
| `page` | (explicit mode) `P<NN>` or svg basename. |
| `x,y,w,h` | (explicit mode) canvas pixels. |
| `file` | video (`.mp4/.mov/.m4v/.webm`) or audio (`.mp3/.wav/.m4a/.aac/.flac/.ogg`). |
| `poster` | optional; video → auto-extract frame; audio → auto-generate play button. |

## Requirements & failure modes

- **ffmpeg** on PATH for audio-wrap + poster extraction. Without it, audio is
  skipped (warning); videos embed only with a supplied poster.
- Unknown slot / page → **skipped with a message** (deck still exports). The script
  is idempotent: reads the newest `exports/*.pptx` without `_media`, writes fresh.
- `--pptx <in>` / `--out <out>` to control files explicitly.

## When NOT to use this

- Per-slide TTS narration is a different feature — see `notes_to_audio.py` /
  the `generate-audio` workflow (bakes narration via the exporter, not as a
  clickable media object).

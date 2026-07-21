# Site media

`game.toml` declares two `[media]` assets the deploy rail uploads next to the manifest and the
site prefers over any baked-in fallback:

- `thumbnail = "media/thumb.gif"` — the hover animation (480×300): the match's final hand
  playing out — blinds, a raise, the flop/turn betting, an all-in, the called showdown
  (queens-full over kings-up) and the winner banner.
- `cover = "media/cover.png"` — the static card picture (960×600): the felt at that decisive
  called showdown, both hole hands up and the pot in the middle.

Both are rendered from this game's own `view/` felt-table SPA — no external art. To regenerate
(art follows the view): load `view/index.html` in headless Chromium, stop the live poll, call
`renderPoker(state, null)` per hand-state frame, screenshot at 960×600, then crop the felt oval
(792×495 @ 84,55) and downscale to 480×300 for the GIF frames (~1.1s a frame, hold the showdown
and banner). The states must audit as real poker (blinds/streets/chip math) — never mock the
layout with impossible hands.

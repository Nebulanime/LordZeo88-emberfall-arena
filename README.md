# 🔥 EMBERFALL ARENA — Roguelite Arena Survival

An original browser game built for the **make.fun Best Game bounty** ($1,000).
**One single file:** `game/index.html` (43,663 bytes) holds the whole game —
HTML + CSS + JavaScript inline, canvas **800×500**, **100% offline**.
No build step, no CDN, no external assets, no network requests, no accounts,
no ads, no login / paywall / tracking / crypto / wallet inside the game.

## Play it

**Option A — double-click:** open `game/index.html` directly in any desktop
browser (Chrome / Edge / Firefox).

**Option B — local server:**
```bash
node serve.ts            # serves game/ at http://localhost:8080
# or: cd game && python3 -m http.server 8000
```

## How to play

You are the last ember in a burning arena. Enemies pour in from the edges in
waves. Kill them, collect the cyan **shards** they drop, level up, and pick
upgrades. Every 5th wave the **EMBER WARDEN** boss appears — break it.

- Survive as many waves as you can. Score = kills × combo multiplier + bonuses.
- Kills within 3 seconds build your **combo** (up to ×2 score).
- Wave clear gives a bonus + small heal. Dying ends the run — your best score
  is saved in `localStorage`.

## Controls

| Input | Action |
|---|---|
| WASD / Arrow keys | Move |
| Mouse | Aim |
| Hold left click / Space | Shoot (or leave auto-fire on) |
| F | Toggle auto-fire (ON by default — auto-aims at nearest enemy) |
| P / Esc | Pause / resume |
| M | Mute / unmute |
| 1 / 2 / 3 or click | Pick a level-up upgrade |
| R | Restart after game over |
| Enter | Start from the menu |

## Features

- **Roguelite loop:** XP shards, level-ups, pick 1 of 3 upgrades from a pool
  of 12 (damage, fire rate, split shot, pierce, crit, magnet, regen, armor,
  max HP, move speed, bullet speed, heal).
- **5 enemy types:** Cinder (chaser), Spark (fast runner), Hexer (ranged
  shooter), Bulwark (tank), Splitter (splits into 2 runners on death).
- **Boss every 5 waves:** the Ember Warden — big HP bar, radial bullet
  patterns, charge attacks.
- **Feel:** particles, screen shake, floating damage numbers, crits,
  hit-flash, drifting ember background, wave banners.
- **Sound:** WebAudio oscillator SFX only (shoot / hit / pickup / level-up /
  boss / hurt). Mute with M. No audio files.
- **Complete flow:** start menu with tutorial → playing → pause → level-up
  → game over with stats → restart. High score + best wave saved locally.
- **HUD:** HP bar, XP bar, score, wave, level, time, combo multiplier,
  boss HP bar.
- **Deterministic screenshot scenes** (kit convention): open with
  `?shot=start&seed=1`, `?shot=play&seed=1` or `?shot=end&seed=1` — the
  game plays its real rules forward with a seeded autopilot and freezes
  the frame, setting `window.__shotReady`. See `shots.json` and
  `SCREENSHOTS.md`.

## Tech

- `game/index.html` — the whole game, one file (43,663 bytes, canvas 800×500)
- `main.ts` — starter entrypoint (unchanged): copies `game/` + `screenshots/`
  to `/output` and writes `dossier.json` via `vendor/makefun-game.ts`
- `vendor/makefun-game.ts` — kit copy, **unchanged** (sha256 `dc671875…6129`)
- `serve.ts` — starter static server for local play-testing
- `shots.json` — the 3 screenshot scenes and their `?shot=` queries
- No dependencies. No network calls. Art is drawn in Canvas code;
  no image, font, or audio files are loaded.

## Build the dossier (after screenshots exist)

```bash
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
# writes out/game/, out/screenshots/, out/dossier.json
```

## Why it fits the bounty

- **Completeness:** menu, play, pause, level-up, boss, game over, restart,
  high score — nothing is a stub; all shown in the 3 screenshots.
- **Fun / depth:** 12 upgrades × 5 enemy types × boss waves × combo scoring
  make every run different.
- **Feel / polish:** particles, shake, damage numbers, banners, SFX, HUD.
- **Look / originality:** original ember-arena theme, all art generated
  in code, no copied assets, no AI-generated / stock / ripped art.

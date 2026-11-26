# PwnPantry

Field notes from the workbench — documenting fuzzing experiments, homebrew dev, console modding, and jailbreak progress across every device on the bench: Switch 2, 3DS, and whatever is next. Wins, crashes, near-bricks, and everything in between.

Run by [RetroVentures-Hayden](https://github.com/RetroVentures-Hayden) — also the home of [SnaccMart](https://github.com/RetroVentures-Hayden/SnaccMart), a homebrew app store for Nintendo Switch 2.

## What's in the pantry

| Device | Status | Notes |
| --- | --- | --- |
| Nintendo Switch 2 | Firmware 23.5.0 — watching and building | Homebrew dev with libounce / ounce-devkit. Fuzzing Switch 1 apps that run on it through backwards compatibility. |
| Nintendo 3DS XL (2013, original model) | Modded — Luma3DS / boot9strap | Stable. Watching for any new brick risk from Nintendo. |
| Nintendo Wii (launch model) | Modded — Homebrew Channel | Complete in box. The GameCube-compatible model. Nintendo left this one alone in 2010, so it just works. |
| Home server (2022 HP Victus laptop, ZimaOS) | Running | The build box: Docker, the ounce-devkit toolchain, and game streaming over Tailscale. |

## The log

Progress entries live in [`log/`](log/) as dated Markdown files, one per session or finding:

`log/YYYY-MM-DD-device-short-title.md`

Each entry uses this format:

```markdown
# <Title>

**Date:** YYYY-MM-DD
**Device:** <device + firmware/version>
**Type:** Fuzzing / Modding / Dev / Exploit research
**Result:** Finding / Clean / Progress / Blocked

## What I did

## What happened

## What's next
```

## How to view the logs

Every entry is a plain Markdown file in the [`log/`](https://github.com/RetroVentures-Hayden/PwnPantry/tree/main/log) folder — no special tools needed:

1. Open the [`log/`](https://github.com/RetroVentures-Hayden/PwnPantry/tree/main/log) folder.
2. Files are named by date (`YYYY-MM-DD-device-short-title.md`), so they sort in order — the newest entry is the last one in the list.
3. Click any file to read it right here on GitHub. Each entry opens with the date, device, type, and result, then what I did, what happened, and what's next.

Cloning the repo instead? Same deal — the entries are in the `log/` folder and open in any text or Markdown editor.

## House rules

- Everything documented here is my own hardware and my own work.
- Findings get written up honestly — a crash is a crash, not an "exploit," until it's proven otherwise.
- No keys, firmware dumps, or game files will ever be posted here. Notes and write-ups only.

## Projects

- [SnaccMart](https://github.com/RetroVentures-Hayden/SnaccMart) — a cozy homebrew app store for Nintendo Switch 2, built with libounce.

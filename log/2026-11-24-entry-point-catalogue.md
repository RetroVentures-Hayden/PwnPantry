# Entry-Point Catalogue: What Else Could Open a Door on Switch 2?

**Date:** 2026-11-24
**Device:** Nintendo Switch 2, firmware 23.5.0
**Type:** Exploit research
**Result:** Progress

## What I did

Catalogued the Switch 1 titles and surfaces that could plausibly serve as homebrew entry points on Switch 2, beyond the three already known (SmileBASIC 4, the Civilization VII cartridge bug, and Seedsow Lullaby). Honest framing up front: on firmware 23.5.0 everything here is stage-one and in-game only — the stage-two escape is patched, so none of this is a jailbreak by itself.

## The proven ones

- **Balatro (Switch 1 cartridge)** — a save-data trick gets userland code execution on Switch 1 *and* Switch 2. Balatro is a LÖVE (Love2D) game, and LÖVE loads save data ahead of the game's own files, so a crafted save shadows the game's entry point and boots a Lua console instead. Verified on real hardware by its author. Catch: the save has to be planted from an already-hacked Switch 1. ([repo](https://github.com/Luminger/balatro-switch-rce))
- **The Artemis-engine family** — Seedsow Lullaby's save trick turns out to be an engine-wide behaviour: a save file can redirect the game's script engine into loading attacker Lua. Working launcher saves exist for four JP demos, and two of them — **Hamidashi Creative** and **Nora, Princess and Stray Cat HD** — were still downloadable from the JP eShop at last check. Same catch: saves are planted from a hacked Switch 1. ([repo](https://github.com/alula/switch-artemis-launcher))
- **Drift Legends 2 (free)** — a researcher demonstrated a WebKit entry on Switch 2 reached through this free-to-play game. The bug lives in the system's WebKit, not the game — the game is just a free host that opens web pages. Demonstrated on 23.0.1; whether it survives on 23.5.0 is unknown, and no code is public. ([write-up](https://karotech.io/blog/2026/11/01/switch-2-webkit-proof-of-concept-drift-legends-2/))

## The unexplored surfaces

- **RPG Maker WITH + its free Player** — the first console RPG Maker with online sharing of whole games. The free Player downloads and executes other creators' game data: the biggest untrusted-content parser in this category, and nobody in the scene appears to have poked it yet. (A real RPG Maker save-file CVE exists, but it's for the desktop runtime — it doesn't transfer to the console engine.)
- **RPG Maker MV Player (free)** — same idea, older engine; the console version strips custom JavaScript, which removes the richest surface.
- **Game Builder Garage** — confirmed running on Switch 2, but the node system is sandboxed by design. Low hopes, noted for completeness.
- **KORG Gadget** — parses other users' song data and text comments in online multiplayer. No known bugs; a watch item at best.

## The lesson

Entry-point titles get pulled or patched — one of the Artemis demos is already gone from the eShop. The free candidates cost nothing to install now and preserve the option later, so that's the play: grab the free ones while they exist.

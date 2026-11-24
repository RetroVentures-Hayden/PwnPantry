# Fuze4 Fuzzing Sweep — 13 Tests, One Confirmed Crash

**Date:** 2026-11-24 (tests run 2026-11-23)
**Device:** Nintendo Switch 2, firmware 23.5.0 — Fuze4 (Switch 1) running via backwards compatibility
**Type:** Fuzzing
**Result:** Finding

## What I did

Hand-typed a 13-test fuzzing sweep into Fuze4's interpreter, one fresh project per test, probing the places an interpreter usually breaks: out-of-range writes, type confusion, recursion limits, integer overflow, and save/load behaviour. Each test was triaged as ERROR (Fuze caught it cleanly), WRONG (impossible output), CRASH, or FREEZE.

## Results

| # | Test | Result |
| --- | --- | --- |
| 1 | Struct field escape | Clean — neighbouring string printed SAFE |
| 2 | String doubling | Clean — Fuze stopped it with its own memory-limit error |
| 3 | Out-of-range array writes | Clean — extreme index stopped with a handled error |
| 4 | Sparse array extension | Clean — length 100001, value landed exactly right |
| 5 | Array assignment | Clean — arrays copy on assignment, no aliasing |
| 6 | Self-referencing structure | Clean — rejected with a handled error |
| 7 | Mixed-type array | Clean — no neighbour corruption |
| 8 | Recursion depth | Clean — Fuze's recursion limit caught it |
| 9 | Integer overflow | Clean — Fuze integers are 64-bit; huge conversions saturate instead of wrapping |
| 10 | Division edges | Clean — inf / nan handled, modulo by zero returns the dividend |
| 11 | Vector over-index writes | **CRASH — confirmed finding, below** |
| 12 | Array growth to 2,000,000 | Clean — memory-limit error, no crash |
| 13 | Save/load round-trip | Clean — identical output after a full restart |

## The finding: negative vector writes crash Fuze4

```fuze
v = { 1, 2, 3, 4 }
v[-1] = 99
```

That second line, on its own, crashes Fuze4 all the way out to the Switch OS screen: "There was a problem, and the software needed to close." Reproduced 3 times in 3 runs, and isolated:

- `v[4] = 99` alone (one past the end): no crash — the write is silently ignored.
- `v[-1] = 99` alone: **crash**. The negative-index write is the trigger, and printing the vector afterwards is not required.
- `v[-2] = 99` and `v[-100] = 99`: both **crash** — negative vector writes are unchecked at any distance.
- Reading `v[-1]` gives Fuze's clean handled error: "Vector index out of bounds. (Vector size: 4, index: -1)". So vector **reads** are bounds-checked — the **write** path is missing the check the read path has.
- Plain arrays don't do this: Test 3's `a[-1] = 999` on a normal array did not crash. The bug is specific to vector element writes.

## Honest framing

This is an out-of-bounds write with an attacker-controlled index and value — the classic shape of a memory-corruption bug, and the same class of bug as the stage-one overflow used by existing Switch 2 jailbreak chains. But a crash is not an exploit: on firmware 23.5.0, anything gained inside Fuze4 stays trapped in the game sandbox, because the stage-two escape those chains relied on is patched. This does not make 23.5.0 jailbreakable. It's a genuine stage-one signal, documented as found.

## Standing rules for this finding

- No Fuze4 updates — an update could patch the bug.
- Crash data from these runs is not shared with Nintendo.

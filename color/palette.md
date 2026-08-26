# Flash Card — colour specification

## The palette

| Role | Hex | RGB | Approx. CMYK | Notes |
|---|---|---|---|---|
| **Card base** | `#080a0d` | 8, 10, 13 | see below | Near-black, **not** pure black. Has warmth in the shadow. |
| **Accent** | `#f97316` | 249, 115, 22 | 0 / 65 / 95 / 0 | Bitcoin orange. The only accent. |
| Chip face (light) | `#f5c96b` | 245, 201, 107 | 3 / 20 / 65 / 0 | Illustrative only — the real module is supplied by the manufacturer. |
| Chip face (dark) | `#c9963f` | 201, 150, 63 | 20 / 40 / 85 / 5 | as above |
| Signature panel | `#f6f4ee` → `#e9e6dd` | — | 2 / 2 / 6 / 0 | Warm off-white. Panel is usually a supplied material, not printed. |
| Body text | `#8e949d` | 142, 148, 157 | — | Legal copy on the back. |
| Secondary text | `#6f757e` | 111, 117, 126 | — | Protocol line. |
| Footer wordmark | `#c9ced6` | 201, 206, 214 | — | Back only; the front wordmark is pure white. |

### Reserved — do not use on the card

| | Hex | |
|---|---|---|
| **Flash green** | `#41ad49` | Sacred to the app UI. It is deliberately absent from the card so the card reads as *the Bitcoin rail*, not as a piece of app chrome. Do not reintroduce it. |

## ⚠ The black is probably not ink

This is the single most important thing on this page.

`#080a0d` describes how the card should *look*. On a matte black card it is
almost certainly **the substrate, not printed ink** — you specify black-core PVC
and print the orange and white on top. Printing a black build onto white PVC
gives a different, worse result: it looks flat, it shows every roller mark, and
any scuff exposes white core.

Decide this with the manufacturer before separations:

- **Black-core PVC (recommended).** The body is black through its thickness. A
  scratch shows black, not white. `#080a0d` becomes a material choice, and the
  only inks are white and orange.
- **Printed black on white core.** If it must be printed, use a **rich black** —
  a single-plate 100K on a card this size will look weak and mottled. Start from
  `C60 M50 Y40 K100` and pull a press proof. Expect the result to read cooler
  than `#080a0d`; compensate by lifting M slightly rather than adding Y.

## ⚠ The CMYK values above are a starting point, not a specification

They are unmanaged conversions. Do not send them to plate. The correct values
depend on the press, the substrate and the ICC profile in use, and PVC behaves
differently from paper stock — ink sits on the surface rather than soaking in,
so saturated colours tend to run darker and glossier than a paper proof
suggests.

**`#f97316` is the colour to protect.** It is the only accent and it carries the
brand association, so it should survive from screen to card unchanged. Two
options:

1. **Spot colour (recommended for a production run).** Nearest Pantone matches
   are around **PMS 1585 C** and **PMS 165 C**. Neither is exact. Confirm
   against a physical Pantone book *on the actual substrate under the actual
   laminate* — a matte laminate will knock the orange back noticeably, and a
   colour approved on a gloss chip will disappoint on a matte card.
2. **CMYK build.** Cheaper, but orange is one of the worst colours to hold in
   four-colour process; it drifts toward red or brown across a run. If the run
   is large enough for a spot plate, use one.

Whichever route: **ask for a physical press proof on the real stock with the
real laminate before committing.** A screen and a paper proof will both lie to
you about this specific card.

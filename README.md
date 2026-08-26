# Flash Card — production asset pack

Print-ready and editable artefacts for the Flash bearer NFC card, derived from
the approved design draft `source/ecashNFC-v1.jpg`.

**Status: draft v1. Not released to plate.**

### Where this fits

These are the physical artefacts for the
[Cashu-First Flash Cards](https://github.com/lnflash/cashu-javacard) project — a
card that holds Bitcoin-denominated ecash on its own chip and spends it by tap.
Several design choices here are downstream of that and are not free to change:

| Choice | Why | Reference |
|---|---|---|
| No name, no card number | It is a bearer instrument, not a debit card | [D2](https://github.com/lnflash/cashu-javacard/blob/main/docs/DECISIONS.md#d2) |
| "Lost or stolen cards cannot be recovered" | Literally true — there is no seed and no backup | [D5](https://github.com/lnflash/cashu-javacard/blob/main/docs/DECISIONS.md#d5) |
| JavaCard 3.0.5 on the back panel | A hard floor; 3.0.4 chips cannot run the applet | [D6](https://github.com/lnflash/cashu-javacard/blob/main/docs/DECISIONS.md#d6) |

For the product reasoning, see
[VISION](https://github.com/lnflash/cashu-javacard/blob/main/docs/VISION.md).
 See
[`SPECIFICATIONS.md` §7–8](SPECIFICATIONS.md) for the pre-flight checklist and
the items still open.

---

## Start here

| If you are… | Read |
|---|---|
| A **print shop** quoting or producing | [`SPECIFICATIONS.md`](SPECIFICATIONS.md) then [`color/palette.md`](color/palette.md) |
| A **design studio** modifying the design | This file, then open the `.svg` masters |
| Deciding **colour** | [`color/palette.md`](color/palette.md) — the black is probably not ink |

## What's in the box

```
flash-card-assets/
├── SPECIFICATIONS.md      ← the production spec: body, finish, chip, copy, pre-flight
├── dielines/
│   └── card-dieline-ID1   ← trim / bleed / safe / corner radius / chip keep-out
├── artwork/
│   ├── concept-a-bearer-front          ← HERO concept, front
│   ├── concept-a-bearer-back           ← back (SHARED — Concept B uses this too)
│   ├── concept-a-bearer-front-SPOTUV   ← UV gloss separation, NOT artwork
│   └── concept-b-circuit-front         ← alternative concept, front
├── logos/
│   ├── flash-wordmark
│   ├── nfc-contactless-symbol
│   └── lightning-bolt
├── color/palette.md       ← hex, CMYK starting points, Pantone candidates, caveats
├── preview/               ← 600 dpi PNGs for approval only, never for plate
└── source/                ← the original design draft this was built from
```

Every vector artefact ships as both **`.svg`** (editable master) and **`.pdf`**
(vector, print-facing). The SVGs open natively in Illustrator, Affinity
Designer, Inkscape and Figma.

## Working with these files

**Units are millimetres.** Every card file uses `1 SVG user unit = 1 mm` with an
artboard of `91.6 × 59.98 mm` (85.6 × 53.98 trim + 3 mm bleed). Don't rescale
the artboard — place against the dieline instead.

**Type is live, on purpose.** It is set in **Inter** (SIL OFL, free for
commercial use) so you can re-set it. **Outline all type — and the strokes on
the contactless mark and circuit traces — before releasing to plate.**

**Colours are RGB.** Convert in your own colour-managed workflow. Read
[`color/palette.md`](color/palette.md) first: on a matte black card the black is
most likely the *substrate*, not ink, and `#f97316` probably wants to be a spot
colour rather than a CMYK build.

**Layers.** The dieline keeps every guide on its own labelled layer so guides
can be switched off or deleted for output. Nothing on those layers prints.

## Three things that will bite you if skipped

**1. The chip keep-out is nominal.** It is drawn to match the approved concept,
not to a specific module supplier. The real footprint and position come from the
card manufacturer per ISO/IEC 7816-2. Get their template and replace ours before
separations.

**2. Concept B centres the chip, and that may not be manufacturable.** On most
dual-interface stock the module position is fixed at top-left by tooling. Either
the centred chip is a printed graphic only — which changes the design — or a
custom module position is commissioned, with cost and MOQ consequences. Resolve
before pricing Concept B. Concept A is unaffected.

**3. The matte is a finish, not a texture.** The source mockup simulates matte
with screen noise. That is deliberately not reproduced in these files. Printing
simulated texture fights the laminate and muddies the black.

## The spot gloss is the idea, not a flourish

A matte black card with a gloss FLASH wordmark: the mark should be invisible
until the card catches the light. `artwork/concept-a-bearer-front-SPOTUV` is the
**varnish plate**, not artwork — solid black is glossed, white is not, and it
registers 1:1 with the front artwork. Supply it as a separate plate or a spot
channel set to overprint. Never merge it into the CMYK.

## What is deliberately absent

**No cardholder name, no card number, no magnetic stripe, no embossing, no
personalisation of any kind.** This is a bearer instrument — it belongs to
whoever holds it, and "BEARER CARD" in small caps is the statement rather than
an omission. Please don't help by adding a name field.

**No Flash green (`#41ad49`).** It is reserved for the app UI and is absent so
the card reads as the Bitcoin rail rather than app chrome.

**No card-scheme marks.** This is not a Visa/Mastercard product. The contactless
symbol supplied is a generic mark; the official EMV Contactless Indicator is
trademarked and would need licensing from EMVCo.

## Provenance

These files were reconstructed as clean vector from the design draft in
`source/`, which was a flat raster. They are a faithful interpretation, not a
mechanical trace — measurements are set to ISO/IEC 7810 rather than scaled off
the image, and the simulated matte texture was dropped for the reasons above.
Where the source was ambiguous, the choice is documented in
[`SPECIFICATIONS.md`](SPECIFICATIONS.md).

Design intent, rationale and the concept comparison all live in the source
image — worth reading before making changes, since several apparent
simplifications are deliberate.

## Licence

[MIT](LICENSE) — © 2026 Flash (getflash.io).

MIT is a software licence and these are design artefacts; it is used here for
consistency with the rest of the Flash repositories, and it grants everything a
print shop or studio needs (use, modify, redistribute) provided the notice is
kept. It does **not** grant rights to the Flash name or wordmark — reuse the
files, not the brand.

## On this being public

Publishing card artwork is not a security concern for this product. The card's
value is bound to a secp256k1 key generated inside the chip and never exported;
a visually identical card with no valid chip cannot produce the NUT-11 signature
a mint requires, so it holds nothing and spends nothing. The artwork is
branding, not a credential.

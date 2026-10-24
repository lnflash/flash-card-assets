# Flash Card: production specification

Bearer NFC payment card · Cashu ecash · **draft v1, not released to plate**

---

## 1. Card body

| | |
|---|---|
| Standard | ISO/IEC 7810 **ID-1** |
| Trim size | **85.60 × 53.98 mm** |
| Corner radius | **3.18 mm** |
| Thickness | **0.76 mm** (ISO nominal) |
| Bleed | **3 mm** all round → artboard **91.60 × 59.98 mm** |
| Safe area | **3 mm** inside trim → **79.60 × 47.98 mm** |
| Orientation | Landscape, both faces |

All supplied artwork is built to the artboard above. Trim, safe area, corner
radius and keep-outs are on `dielines/card-dieline-ID1.svg`.

## 2. Substrate and finish

| | |
|---|---|
| Material | PVC, **black core recommended**; see `color/palette.md` |
| Finish | **Matte laminate**, both faces |
| Special | **UV spot gloss on the FLASH wordmark, front only** |
| Mag stripe | **None** |
| Embossing | **None** |
| Personalisation | **None**: no name, no number, no encoding |

**The matte is a laminate finish.** The reference mockup simulates it with a
noise texture; that is a screen effect and is deliberately absent from the
production files. Do not print simulated texture, which fights the laminate and
muddies the black.

**The spot gloss carries the design.** The card is matte black with a gloss wordmark, so the
FLASH mark is invisible until the card catches the light. Separation is
supplied as `artwork/concept-a-bearer-front-SPOTUV.svg`, a separate plate that
stays out of the CMYK. If registration is marginal at this size, **spread** the
varnish ~0.1 mm rather than choking it; a hairline of gloss on black cannot be
seen, a hairline of matte inside a glossed letter can.

## 3. Chip and RF

| | |
|---|---|
| Platform | **JavaCard 3.0.5** (minimum; see note) |
| Interface | **Dual**: contactless ISO/IEC 14443-4 + contact ISO/IEC 7816 |
| Module position | **Top-left, front** (Concept A) |
| Applet | Cashu bearer applet, loaded post-production via GlobalPlatform |

**JavaCard 3.0.5 is a hard floor.** The applet calls
`KeyAgreement.ALG_EC_SVDP_DH_PLAIN_XY`, which does not exist in the 3.0.4 API. A
3.0.4 card, including several otherwise-suitable JCOP3 and Feitian parts,
**cannot run this applet at all**. Confirm the platform version with the
manufacturer in writing before any tooling is cut.

**The chip keep-out on the dieline is nominal.** The contact plate footprint and
its exact position are set by the module supplier per ISO/IEC 7816-2 and vary
between suppliers. Replace the keep-out with the manufacturer's own template
before separations. Nothing prints inside it, and the cavity is milled after
lamination.

**Antenna.** A dual-interface card carries an induction antenna wound just
inside the card edge, between core layers. It is invisible and imposes no print
restriction, **but heavy metallic or foil coverage over the ring can detune it**.
There is no foil in the current design; flag it if any is added.

### ⚠ Concept B centres the chip: confirm feasibility before quoting

Concept B places the module at the card's centre. On most dual-interface stock
the module position is fixed at top-left by the milling tooling. Either the
centred element is a **printed graphic only** (with the real module still at
top-left, which changes the design), or a custom module position is commissioned,
with tooling cost and minimum-order implications. **Resolve this before
Concept B is priced.** Concept A has no such issue.

## 4. Typography

| | |
|---|---|
| Family | **Inter**: [rsms.me/inter](https://rsms.me/inter) |
| Licence | SIL Open Font License 1.1, free for commercial use, embeddable |
| Wordmark | Inter **Black (900)**, letter-spacing ≈ 0.02em |
| Card copy | Inter Regular / Medium / SemiBold |

Type is supplied as **live text** so the studio can re-set it. **Convert all
type to outlines before release to plate.** Minimum reproduction size on the
back is **1.5 mm cap height**. The legal copy is already close to that floor,
so do not scale it down further.

## 5. Copy

The back copy is **legally and editorially load-bearing** and is not filler:

> This card is a bearer instrument. Whoever holds this card controls the funds
> stored on the chip. Keep it safe. Treat it like cash. Lost or stolen cards
> cannot be recovered.

> Powered by Cashu ecash protocol · NFC ISO 14443-4 · JavaCard 3.0.5

> getflash.io · flash@flashapp.me

Do not reflow to fewer lines, shrink, or soften this without sign-off. It states
the product promise plainly, and the "cannot be recovered" clause is the part
users most need to see. Legal review is still outstanding; see §8.

There is **no cardholder name and no card number**, by design. "BEARER CARD" in
small caps states that.

## 6. File formats supplied

| Format | Use |
|---|---|
| **SVG** | Master, fully editable vector. Opens in Illustrator, Figma, Inkscape, Affinity. |
| **PDF** | Vector, print-facing. Generated from the SVG masters. |
| **PNG @600 dpi** | Reference/approval only, **never** send to plate. |

Everything is vector; there is no resolution ceiling. If a raster is ever
substituted it must be **≥ 600 dpi at final size** for a card this small. 300
dpi is a paper convention and is visibly soft on a 85.6 mm canvas held at
reading distance.

Supplied colours are **RGB**. Conversion to CMYK or to a spot plate must be done
in the studio's own colour-managed workflow; see `color/palette.md`, which also
explains why `#f97316` should probably be a spot colour.

## 7. Pre-flight checklist

- [ ] Manufacturer's chip template replaces the nominal keep-out
- [ ] JavaCard **3.0.5+** confirmed in writing
- [ ] Black-core vs printed-black decided
- [ ] `#f97316` route decided (spot vs CMYK build)
- [ ] All type converted to outlines
- [ ] Strokes outlined (contactless mark, circuit traces)
- [ ] Spot UV supplied as a separate plate, set to overprint
- [ ] Concept B chip position resolved (if Concept B proceeds)
- [ ] **Physical press proof on real stock, under the real laminate**, approved
- [ ] Legal sign-off on back copy

## 8. Open items

1. **Legal review of the bearer copy.** The disclaimer asserts unrecoverable
   loss. That is technically accurate for this product, but whether it is
   sufficient as consumer-facing disclosure is a question for counsel, and it
   may vary by jurisdiction of issue.
2. **Regulatory marks.** No card-scheme marks apply (this is not a Visa/MC
   product). If the official **EMV Contactless Indicator** is wanted, that mark
   is trademarked and must be licensed from EMVCo. The symbol supplied in
   `logos/` is a generic equivalent, appropriate for a non-scheme card.
3. **Quantity and tooling.** Spot UV, a spot colour plate, and any custom module
   position each carry setup cost that only amortises over volume. Pricing
   should be sought at the intended run size.
4. **Card lifecycle.** Applet loading, key generation and funding all happen
   after the cards are manufactured. The production run should not include
   personalisation of any kind.

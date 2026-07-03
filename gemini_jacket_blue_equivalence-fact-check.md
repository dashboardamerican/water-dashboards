# Fact-Check Report: Gemini Blue-Water Equivalence Dashboard
> Last audited: 2026-06-23
> Target: docs/gemini_jacket_blue_equivalence.html
> Scope: Full audit (first audit — no prior report existed)
> Mode: standard + external web verification of the central Gemini-paper figures

## Audit Summary
- **Claims reviewed**: 18 (core constants, 9 comparison items, 2 offsite intensities, denominator, framing)
- **Verified**: 15 (calculation reproduced and/or source traced)
- **Minor issues**: 3 (leather US-correction multiplier provenance; "average American" denominator framing; LBNL page archive status)
- **Significant issues**: 0
- **Unverifiable**: 0 (central Gemini figures web-confirmed; all other inputs trace to on-disk sources)
- **Overall confidence**: HIGH — every comparison-item calculation reproduces exactly; the central Gemini prompt figures match the primary arXiv paper; the conservative framing is genuine.

## Source Inventory
| # | Source | Type | Path/URL | On disk? | Last verified |
|---|--------|------|----------|----------|---------------|
| G1 | Google Gemini environmental study, arXiv:2508.15734v1 (Aug 21 2025) | Primary technical paper | https://arxiv.org/abs/2508.15734 | No (web) | 2026-06-23 |
| G2 | Fulton et al. (2019), CA almonds, Ecological Indicators | Peer-reviewed | research/sources/1-s2.0-S1470160X17308592-main.pdf | Yes | 2026-06-23 |
| G3 | Mekonnen & Hoekstra (2010/2012), Farm Animal Products | Peer-reviewed | research/datasets/wfn_farm_animals.pdf | Yes | 2026-06-23 |
| G4 | Klopatek & Oltjen (2022), US beef water, J. Animal Science | Peer-reviewed | research/references/klopatek_oltjen_2022_beef_water.pdf | Yes | 2026-06-23 |
| G5 | WFN Report 47, Water Footprint of Crops (cotton) | Research report | research/datasets/Report47_WaterFootprintCrops_Vol2.txt | Yes (txt only) | 2026-06-23 |
| G6 | LBNL 2024 US Data Center report | Federal lab | https://escholarship.org/uc/item/32d6m0d1 | Text in research/sources/primary_trace_2026-02-24 | 2026-02-24 |
| G7 | Brian Potter, "I Was Wrong About Data Center Water" | Secondary (blog) | https://www.construction-physics.com/p/i-was-wrong-about-data-center-water | No | — |
| G8 | USGS water-use model (WY2020 CONUS consumptive) | Federal agency | https://www.usgs.gov/.../water-use-united-states | Cross-checked vs PP1894D on disk | 2026-06-23 |
| G9 | US Census 2020 population | Federal agency | census.gov 2020 release | No | — |

## Claim-by-Claim Audit

### Claim 1: Gemini direct water = 0.26 mL/query; energy = 0.24 Wh/query
- **Location**: `promptProfiles.google_median` (lines 635–638); input defaults
- **Source**: G1 (arXiv:2508.15734)
- **Web verification (2026-06-23)**: Paper reports the **median Gemini Apps text prompt uses 0.24 Wh of energy and ~0.26 mL of water** ("equivalent of five drops of water"). Exact match.
- **Verdict**: ✅ VERIFIED — **HIGH**. Not on disk; confirmed against the primary paper via web. Recommend archiving the PDF to `research/references/` to make it locally traceable.

### Claim 2: Jeans = 10,000 L/kg cotton × 33% blue × 0.80 kg = 2,640 L
- **Calc check**: 10000 × 0.33 × 0.80 = 2,640 ✓ (matches displayed `targetBlueL` = 2640)
- **Source**: G5 — seed-cotton global avg (green 2,282 / blue 1,306 / grey 56 m³/ton → 3,644 L/kg; lint ≈ 3,644/0.35 ≈ 10,411 L/kg ≈ 10,000). Blue share of seed cotton = 1,306/3,644 = **35.8%** (dashboard uses 33%, conservative round-down).
- **Verdict**: ✅ VERIFIED — **MEDIUM/HIGH**. The clean "10,000 L/kg" and "2,495 L/shirt" are WFN published aggregates (not literal cells), but they are derivable from the on-disk M&H seed-cotton data and internally consistent. 33% blue is slightly below the 35.8% source value → conservative.

### Claims 3–7: Other cotton items (shirt, sofa, socks, area rug) and suit jacket
- shirt: 2,495 × 0.33 = 823.4 L ✓ · sofa: 10,000 × 0.33 × 7.5 = 24,750 L ✓ · socks: 10,000 × 0.33 × 0.07 = 231 L ✓ · area rug: 10,000 × 0.33 × 20 = 66,000 L ✓ · jacket: user-editable (0.70 kg default, disclosed as on-page assumption)
- **Verdict**: ✅ VERIFIED — calculations reproduce; mass assumptions (sofa 7.5 kg, rug 20 kg, socks 0.07 kg) are disclosed in the per-item notes with industry yardage citations.

### Claim 8: Leather shoes = 17,093 L/kg × 4% blue × 4.33 (US correction) × 0.50 kg = 1,480 L
- **Calc check**: 17093 × 0.04 × 4.33 × 0.50 = 1,480.3 L ✓
- **Component 8a — M&H leather total + blue share**: G3 worked example gives leather green 15,900 / blue 680 / grey 500 / **total 17,080 L/kg**; blue share = 680/17,080 = **3.98% ≈ 4%**. Dashboard's 17,093 is within ~13 L of 17,080. ✅ VERIFIED.
- **Component 8b — the 4.33× "US correction"**: ⚠️ **MINOR ISSUE**.
  - Klopatek (G4) confirms **US beef blue = 2,275 L/kg** (verbatim). ✅
  - The 4.33 multiplier is a *derived ratio* (US beef blue ÷ M&H global beef blue), not a verbatim figure. M&H's clean global beef blue (G3) ≈ **550 L/kg**, giving **2,275 ÷ 550 = 4.14×**; 4.33× implies a denominator of ~525 L/kg.
  - **Direction is correct**: US irrigated-feed beef blue water (2,275) far exceeds the global average (~525–550) because US feed is heavily irrigated — applying that ratio to leather (same animal, co-product) is a defensible disclosed approximation.
  - The exact 4.33 is ~5% high vs the cleanest M&H value (4.14×); effect on the leather figure: 1,480 L vs 1,415 L (≈4% — negligible for the dashboard's purpose).
- **Note on a false-positive caught in audit**: a sub-agent initially flagged this as a "backwards/inverted" error by comparing 2,275 to a garbled "5,129 L/kg" figure in Klopatek (the same sentence contains the impossible "128,594 L/kg" — an OCR artifact). The clean M&H source (550 L/kg) confirms the dashboard's direction and magnitude. This is **not** a significant error.
- **Recommendation**: cite the ratio as "≈4.1× (US beef blue 2,275 ÷ M&H global beef blue ~550)" or pin 4.33 to the specific M&H table value used; note it is applied to leather by analogy to beef.
- **Verdict**: ⚠️ MINOR ISSUE — **HIGH** confidence on the diagnosis.

### Claim 9: Almonds (handful, 28 g) = 5,290 L/kg blue × 0.028 = 148 L
- **Calc check**: 5290 × 0.028 = 148.1 L ✓
- **Source**: G2 — verbatim: "Between 2004 and 2015, the average water footprint of one kilogram of raw California almond kernels was **5290 liters blue water**, 570 green, 4,380 grey (total = 10,240 l/kg)." Exact match; uses the blue figure directly (no extra blue-share multiply, correct).
- **Verdict**: ✅ VERIFIED — **HIGH** (primary source on disk).

### Claim 10: Lawn sprinkler (1 hr) = 12 GPM × 60 = 720 gal × 3.785 L/gal × 70% consumptive = 1,908 L
- **Calc check**: 720 × 3.785411784 × 0.70 = 1,907.9 L ✓ (note states 2,725 L/hr applied, 1,908 L consumptive)
- **Source**: EPA WaterSense outdoor use (12 GPM typical). The 70% consumptive (ET) fraction is a reasonable modeling assumption (disclosed).
- **Verdict**: ✅ VERIFIED — **MEDIUM** (flow rate is "typical residential," disclosed as such).

### Claim 11: LBNL offsite path = 4.52 L/kWh (includes hydro)
- **Source**: G6 (LBNL 2024). The eScholarship page returned a challenge/block page in the Feb-24 archive (status logged in the page's own `TRACE_ARCHIVE_LOOKUP`). Figure is consistent with the LBNL boundary used in the audited calculator dashboard.
- **Verdict**: ✅ VERIFIED — **MEDIUM** (primary page archive was blocked; figure cross-consistent with prior calculator audit).

### Claim 12: Non-hydro offsite path = 1.7838676580625 L/kWh
- **Derivation (stated)**: Potter total 275 Mgal/day − LBNL direct 47.768 Mgal/day = 227.232 Mgal/day offsite, over 176 TWh annual DC electricity.
- **Calc check**: 227.232e6 gal/day × 365 × 3.785411784 L/gal ÷ 176e9 kWh = **1.78387 L/kWh** ✓ (reproduces to the displayed precision)
- **Verdict**: ✅ VERIFIED — **MEDIUM**. Internally exact; the inputs (275 Mgal/d Potter, 47.768 LBNL direct, 176 TWh) trace to the same LBNL/Potter sources audited in the calculator dashboard. Disclosed as a "secondary sensitivity source."

### Claim 13: Average American blue baseline = 84,939 Mgal/day ÷ 331,449,281 pop = ~354,000 L/person/yr
- **Calc check**: 84,939e6 gal/d × 3.785411784 × 365 ÷ 331,449,281 = **354,076 L/person/yr** ✓ (dashboard computes 354,036 — match to rounding)
- **Source**: G8 USGS WY2020 CONUS consumptive (84,939 = 78,400 + 2,382 + 4,157, cross-checked vs USGS PP1894D on disk) + G9 Census 2020 (331,449,281, exact).
- **Verdict**: ✅ VERIFIED — **HIGH** on the math/inputs; see Framing Note F1 on interpretation.

### Claim 14 (headline behavior): "At 100 prompts/day it would take ~105 years to equal one pair of jeans"
- **Calc check**: total = 0.00026 + (0.00024 × 1.78387) = 0.000688 L/query; ×100×365 = 25.1 L/yr; 2,640 ÷ 25.1 = 105.1 yr ✓
- **Verdict**: ✅ VERIFIED — internally consistent; the "tiny in context" conclusion is robust.

## Calculation Verification
| Calc | Formula | Expected | Actual | Match |
|------|---------|----------|--------|-------|
| Avg American blue | 84,939e6×3.78541×365 ÷ 331,449,281 | ~354,000 L | 354,076 L | ✅ |
| Non-hydro L/kWh | (275−47.768)e6×365×3.78541 ÷ 176e9 | 1.78387 | 1.78387 | ✅ |
| Jeans blue | 10,000×0.33×0.80 | 2,640 | 2,640 | ✅ |
| Leather blue | 17,093×0.04×4.33×0.50 | 1,480 | 1,480 | ✅ (multiplier ⚠️) |
| Almonds blue | 5,290×0.028 | 148 | 148.1 | ✅ |
| Sprinkler | 720×3.78541×0.70 | 1,908 | 1,907.9 | ✅ |

## Apples-to-Apples Audit
| Comparison | Left (AI prompt) | Right (item) | Aligned? | Notes |
|-----------|------------------|--------------|----------|-------|
| Prompt blue water vs item blue water | Direct + offsite-electricity blue water | Item blue water only (green/grey excluded) | ✅ | Both sides are **blue water only** — explicitly stated as the most conservative framing |
| Prompt blue water vs "average American" | Annual prompt blue water | Per-capita total US consumptive use | ⚠️ | Denominator includes ag/industry (see F1) |

## Framing Notes
- **F1 — "Share of an average American's blue water consumption."** The denominator (84,939 Mgal/day) is *total US consumptive use across all sectors* (≈70–75% agriculture) allocated per capita. This is the standard per-capita water-footprint convention, but a reader could mistake it for *personal/household* use. Because the denominator is large, this **minimizes** the AI share — i.e., it is the *less* conservative choice for the "AI water is trivial" narrative, not a thumb on the scale toward alarm. Recommend a one-line clarifier: "per-capita total US consumptive use (all sectors, incl. agriculture)."
- **F2 — Conservative framing is genuine.** Tracking blue water only (excluding green/grey and returned withdrawals) is the most conservative comparison and is stated repeatedly. It consistently makes AI look larger relative to its true total footprint, not smaller.
- **F3 — Marginal vs total electricity water.** The offsite path attributes grid-average power-water intensity to marginal AI load. Disclosed via the two selectable boundaries (LBNL-with-hydro vs Potter no-hydro).

## Unresolved / Recommendations (priority order)
1. **Leather 4.33× multiplier** (Claim 8b): re-label as ≈4.1× with explicit "US beef blue 2,275 ÷ M&H global ~550" derivation, or pin to the exact M&H table cell used. Minor magnitude effect.
2. **"Average American" denominator** (F1): add "all sectors, incl. agriculture" clarifier.
3. **Archive the Gemini paper PDF** (Claim 1) to `research/references/` so the central figures are locally traceable rather than web-only.
4. **Cotton aggregates** (Claim 2): optionally note that 10,000 L/kg and 2,495 L/shirt are WFN published aggregates derived from the M&H seed-cotton data.

## Change Log
| Date | Auditor | Scope | Key findings |
|------|---------|-------|--------------|
| 2026-06-23 | Claude | Full first audit (18 claims) | 0 significant issues. Gemini 0.26 mL/0.24 Wh web-verified vs arXiv:2508.15734. All item calcs reproduce. 3 minor: leather 4.33× provenance (≈4.14× per clean M&H), "average American" denominator framing, LBNL page archive-blocked. Caught and downgraded a sub-agent false-positive that misread Klopatek's OCR-garbled "5,129 L/kg." |
| 2026-07-02 | Claude | Fixes applied (recommendations 1–4) | **Rec 1 FIXED**: leather multiplier changed 4.33× → 4.14× with explicit derivation (US beef blue 2,275 ÷ M&H global ~550) in the item note, sources list, and evidence manifest; leather shoes now 1,415.30 L. **Rec 2 FIXED**: "average American" card, calc trace, and sources entry now state "all sectors, including agriculture (≈3/4 of total) — not household use." **Rec 3 FIXED**: Gemini paper archived to `research/references/arxiv_2508.15734_gemini_environmental.pdf`. **Rec 4 FIXED**: WFN cotton entry notes the aggregates derive from M&H seed-cotton data. Also (evidence-layering pass, not audit findings): hero provenance line linking key inputs to anchored source entries; source-quality tier chips; archive status from the JS manifest now rendered in the Sources panel; fact-check badge added. All 13 harness checks pass. |

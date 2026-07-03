# Fact-Check Report: US Data Center Water Calculator
> Last audited: 2026-07-03
> Target: docs/us_data_center_water_calc_explicit.html
> Scope: Full audit (incremental - builds on 2026-02-25 audit + ethanol/pools sub-audits) plus 2026-06-03 PPA capacity addendum, 2026-06-08 zero-water procurement boundary correction, 2026-06-30 PPA/source refresh, 2026-07-01 PPA traceability hardening, and 2026-07-03 PPA solar/wind split diagnostic
> Mode: standard + selective external cross-validation

## Audit Summary
- **2026-07-03 PPA solar/wind split diagnostic**: no change to the **84.899 GW** PPA default. Added a resource-mix diagnostic: **67.287 GW solar + 17.611 GW wind**, or about **79.3% solar / 20.7% wind**. Amazon and Meta are exact source-derived splits; Google and Microsoft are chart-derived estimates from the BCSE/BNEF 2026 Factbook buyer chart because neither company publishes a complete public US/NA project-level wind/solar table.
- **2026-07-01 PPA traceability hardening**: no numeric change to the PPA default. Added an on-page PPA traceability ledger with direct source links, extraction method, zero-water exclusion rule, confidence label, and known limitation for Google, Amazon, Meta, Microsoft, and the default total. Mirrored the same audit structure into the export trace, assumption rows, and downloadable PPA CSV.
- **2026-06-30 PPA/source refresh and deep pass**: contracted full-build zero-water capacity now uses **84.899 GW** as the strict lower-bound default: Google **16.700 GW** North America zero-water floor + Amazon **22.491 GW** live CSV named US wind/solar + Meta **19.558 GW** live map numeric US wind/solar + Microsoft **26.150 GW** zero-water-adjusted US renewable map. Microsoft starts from the official **26.252 GW** map and subtracts **0.102 GW** of identified Hawk's Nest hydropower. A separate non-default Google aggregate-adjusted cross-check implies **~95.0-97.3 GW** for the Big 4, but it is not the model default because Google's public aggregate is not resource-specific.
- **Claims reviewed**: 39 core claims + 1 PPA split diagnostic
- **Verified**: 33 core claims + 1 PPA split diagnostic
- **Minor issues**: 3
- **Significant issues**: 1 (golf figure)
- **Unverifiable**: 2 (LBNL 2028 projections; Sampson et al. paywalled)
- **Overall confidence**: HIGH — core model math is bulletproof; the golf issue doesn't affect the headline conclusion (and is conservative)

## 2026-06-23 Delta Re-Audit (current working tree, file mtime June 19)

The working-tree file was modified after the June 8 report. This delta confirms the June 8 recommendations were implemented; no new issues introduced.

| June 8 item | June 23 status (current file) | Evidence |
|---|---|---|
| ❌ Golf 292 Bgal attributed to GCSAA (should be ~531 applied / ~425 consumed) | ✅ **FIXED** | Now **425 Bgal/yr** with label "GCSAA Phase IV: 1.63M AF applied (HortTechnology 35(5), 2025) × 80% ET consumptive" (lines 2142, 2654). 1.63M AF × 325,851 × 0.80 = 424.9 ≈ 425 ✓. Now apples-to-apples (consumptive) with the chart. "292" no longer appears anywhere in the file. |
| ⚠️ Google replenishment "~64% of consumption" missing "freshwater" | ✅ **FIXED** | Lines 1546 & 2757 now read "~64% of **freshwater** consumption." |
| ⚠️ "Last verified Feb 24" stale | ✅ **FIXED** | Header now reads "Last full audit: March 29, 2026; zero-water procurement trace updated: June 8, 2026" (lines 1151–1152). |
| ⚠️ Orchards (7.9 Bgal/day) missing from source mapping | ❌ **STILL OPEN** | `agricultureBgalDay` still has `{id:"orchards", label:"Orchards (almonds, etc.)", bgalDay:7.9}` (line 2196), but the `ag_benchmark_*` source-mapping rows (lines 2658–2662) cover alfalfa, other hay/grass, cotton, alfalfa-china, all-irrigation — **no orchards row**. 7.9 Bgal/day = 8.85M AF/yr is plausible (~11% of US irrigation) but undocumented. Add `ag_benchmark_orchards_af_year` (~8,849,125 AF/yr) with source attribution. |

**Overall (June 23):** core math and headline "rounding error" conclusion remain robust; one documentation gap (orchards) carries over.

## Prior Audit Issues — Resolution Status

### RESOLVED (5 of 7 prior issues fixed)

| Prior Issue | Status | Evidence |
|---|---|---|
| ❌ Evidence snippet quoted USGS abstract (2010-2020 avg) instead of WY2020 body text | ✅ FIXED | Line 1196 now quotes WY2020 values (4,157/78,400/2,382 Mgal/d) with explicit note that abstract differs |
| ❌ Golf source URL dead (wrong volume/issue) | ✅ FIXED | URL updated to `journals.ashs.org/view/journals/horttech/35/5/article-p848.xml` (confirmed accessible) |
| ❌ Swimming pools 110 Bgal overstated | ✅ FIXED | Revised to 56 Bgal (7.5M pools × 7,500 gal/yr); prior deep audit confirmed as conservative lower bound |
| ⚠️ Ethanol ">90%" conflated (national increase vs regional sourcing) | ✅ FIXED | Line 738 now reads "regions that source >90% of their irrigation from the Ogallala Aquifer" — matches paper's framing |
| ⚠️ Ethanol "67% of irrigated acreage" should be "irrigation water applications" | ✅ FIXED | Line 1080 now says "irrigation water applications" |

### STILL OPEN (2 prior issues)

| Prior Issue | Status | Details |
|---|---|---|
| ❌ Golf 292 Bgal figure understated vs GCSAA primary | ❌ STILL OPEN | See Claim 17 below. Figure and source attribution remain misaligned. |
| ❓ Sampson et al. (2021) paywalled | ❓ STILL UNVERIFIABLE | Full paper not acquired. The 4% Kansas irrigation claim remains unverifiable from available project sources. |

## Source Inventory
| # | Source | Type | Path/URL | Last Verified |
|---|--------|------|----------|---------------|
| S1 | LBNL 2024 Data Center Report | Federal lab | https://escholarship.org/uc/item/32d6m0d1 | 2026-02-25 |
| S2 | USGS Professional Paper 1894-D | Federal agency | https://pubs.usgs.gov/publication/pp1894D | 2026-02-25 |
| S3 | IEA Energy and AI | International agency | https://www.iea.org/reports/energy-and-ai/executive-summary | 2026-02-25 |
| S4 | CBRE NA Data Center Trends H1 2025 | Industry report | https://www.cbre.com/insights/reports/17887575722 | 2026-02-25 |
| S5 | GCSAA Golf Environmental Profile Phase IV | Peer-reviewed publication | https://journals.ashs.org/view/journals/horttech/35/5/article-p848.xml | 2026-03-29 |
| S5b | GCSAA Phase IV Water Report (PDF) | Industry survey | https://www.gcsaa.org/docs/default-source/what-we-do/gcep-phase-4-water-report.pdf | 2026-03-29 |
| S5c | GCSAA Press Release | Industry press | https://www.gcsaa.org/who-we-are/media/news-release/2025-news-releases/2025/12/30/golf-courses-reduce-water-usage-by-31-percent-according-to-national-survey | 2026-03-29 |
| S6 | Brian Potter, "How Does the US Use Water?" | Secondary (blog) | https://www.construction-physics.com/p/how-does-the-us-use-water | 2026-02-25 |
| S7 | NCASI Technical Bulletin 960 | Industry research org | https://www.ncasi.org/wp-content/uploads/2019/02/tb960.pdf | 2026-02-25 |
| S8 | AF&PA 2025 Sustainability Report | Industry association | https://www.afandpa.org/sites/default/files/2025-07/2025AF%26PASustainabilityReport_FinalWeb.pdf | 2026-02-25 |
| S9 | AF&PA Production/Capacity Release | Industry association | https://www.afandpa.org/news/2025/afpa-details-us-paper-production-and-capacity-trends | 2026-02-25 |
| S10 | EPA WaterSense Pool Efficiency | Federal agency | https://www.epa.gov/watersense/swimming-pools-and-spas | 2026-02-25 |
| S11 | Lamsal & Marston 2025 | Peer-reviewed journal | https://doi.org/10.1029/2024WR038334 | 2026-02-25 |
| S12 | Google 2025 Environmental Report | Corporate report (EY verified) | https://sustainability.google/reports/google-2025-environmental-report/ | 2026-06-03 |
| S12b | Clearway-Google US PPAs | Developer press release / investor disclosure | https://www.clearwayenergygroup.com/press-releases/clearway-signs-portfolio-of-power-purchase-agreements-with-google-totaling-nearly-1-2-gw-across-three-states/ | 2026-06-30 |
| S12c | TotalEnergies-Google Texas solar PPAs | Developer press release | https://totalenergies.com/news/press-releases/united-states-totalenergies-provide-1-gw-solar-capacity-power-googles-data | 2026-06-30 |
| S12d | Enlight/Clenera-Google Oklahoma solar PPA | Developer press release via Nasdaq/GlobeNewswire | https://www.nasdaq.com/press-release/enlight-signs-200-mw-ac-solar-power-purchase-agreement-google-support-data-center | 2026-06-03 |
| S12e | BCSE/BloombergNEF 2026 Sustainable Energy in America Factbook | BNEF market dataset / public factbook | https://bcse.org/wp-content/uploads/2026/02/2026-Sustainable-Energy-in-America-Factbook.pdf | 2026-07-03 |
| S12f | Google 2026 Environmental Report | Corporate report (limited assurance) | https://sustainability.google/reports/google-2026-environmental-report/ | 2026-06-30 |
| S12g | Google operations / CFE procurement page | Corporate source page | https://sustainability.google/operations/ | 2026-06-30 |
| S12h | Brookfield-Google hydro framework | Developer press release | https://bam.brookfield.com/press-releases/brookfield-and-google-sign-hydro-framework-agreement-deliver-3000-mw-homegrown | 2026-06-30 |
| S12i | Google-Kairos nuclear agreement | Corporate blog | https://blog.google/outreach-initiatives/sustainability/google-kairos-power-nuclear-energy-agreement/ | 2026-06-30 |
| S12j | Google/Fervo geothermal procurement | Corporate / utility announcement | https://blog.google/feed/nevada-clean-energy/ | 2026-07-01 |
| S12k | Google-CFS fusion agreement | Developer announcement | https://cfs.energy/news-and-media/google-and-commonwealth-fusion-systems-sign-strategic-partnership/ | 2026-07-01 |
| S12l | Google-Duane Arnold nuclear agreement | Corporate announcement | https://blog.google/feed/infrastructureduane-arnold-nuclear-plant-iowa/ | 2026-07-01 |
| S13 | Meta 2025 Sustainability Report | Corporate report | https://sustainability.atmeta.com/2025-sustainability-report/ | 2026-06-03 |
| S14 | Microsoft Cloud Blog (Dec 2024) | Corporate blog | https://www.microsoft.com/en-us/microsoft-cloud/blog/2024/12/09/sustainable-by-design-next-generation-datacenters-consume-zero-water-for-cooling/ | 2026-02-25 |
| S15 | AWS Sustainability | Corporate page | https://sustainability.aboutamazon.com/products-services/aws-cloud | 2026-02-25 |
| S16 | Amazon Sustainability Report 2024 | Corporate report | https://sustainability.aboutamazon.com/2024-report | 2026-02-25 |
| S16b | Amazon current carbon-free energy project CSV | Corporate project inventory | https://sustainability.aboutamazon.com/content/dam/sustainability-marketing-site/05-carbon-free-energy/amazon-carbon-free-energy-projects.csv | 2026-07-03 |
| S17 | Meta Sustainability Report 2024 | Corporate report | https://sustainability.fb.com/wp-content/uploads/2024/08/Meta-2024-Sustainability-Report.pdf | 2026-02-25 |
| S17b | Meta Energy page and sustainability impact map | Corporate project inventory | https://sustainability.atmeta.com/energy/ | 2026-07-03 |
| S18 | Microsoft Feb 2026 blog | Corporate blog | https://blogs.microsoft.com/blog/2026/02/18/a-milestone-achievement-in-our-journey-to-carbon-negative/ | 2026-06-30 |
| S18b | Microsoft renewable map image | Corporate map | https://blogs.microsoft.com/wp-content/uploads/2026/02/renewable-energy-map-miller-light.png | 2026-06-30 |
| S18c | Microsoft renewable project examples | Corporate feature | https://news.microsoft.com/source/features/sustainability/6-projects-that-helped-microsoft-meet-its-renewable-energy-goal/ | 2026-06-30 |
| S18d | LIHI Hawk's Nest Hydroelectric Project page | Hydropower certification data | https://lowimpacthydro.org/hawks-nest-project-wv/ | 2026-07-01 |
| S19 | USDA FAS GATS | Federal agency | https://apps.fas.usda.gov/gats/ | 2026-02-25 |
| S20 | Prior fact-check (swimming pools) | Internal | notes/us_data_center_water_calc_explicit-fact-check-pools.md | 2026-02-24 |
| S21 | Census SWUM documentation | Federal agency / academic | Randy Becker CES-WP-15-16 | 2026-02-25 |
| S22 | NIST unit conversion tables | Federal agency | https://www.nist.gov/pml/owm/metric-si/unit-conversion | 2026-02-25 |
| E1 | Teter et al. (2018) | Peer-reviewed (open access) | references/teter_2018_rfs_water_impacts.pdf | 2026-02-26 |
| E2 | Lark et al. (2022) | Peer-reviewed (open access) | references/lark_2022_rfs_environmental_outcomes.pdf | 2026-02-26 |
| E5 | Sampson et al. (2021) | Peer-reviewed (paywalled) | Not on disk | 2026-02-26 |

## PPA / Zero-Water Procurement Addendum (2026-06-30)

### Result
- **Strict lower-bound contracted full-build zero-water capacity**: **84.899 GW**.
- **Non-default aggregate-adjusted cross-check**: **~95.0-97.3 GW** if Google's North America clean-energy aggregate is adjusted for identifiable non-zero-water CFE and 2026 solar/wind announcements.
- The strict 84.899 GW value remains the defensible single-number default for the contracted-capacity scenario. The 95.0-97.3 GW range is useful context, but not a default model input.
- Boundary: US-focused wind/solar/solar+storage procurement, including identifiable on-site solar, excluding nuclear/hydro/geothermal/fusion because those are not zero-water resources.

### Calculation Trace
| Component | Calculation | Included GW | Confidence | Notes |
|---|---:|---:|---|---|
| Google North America zero-water floor | Conservative floor pending US/NA wind-solar split | 16.700 | Medium as lower bound | 2026 report gives nearly 35 GW global and >29 GW North America clean-energy agreements through 2025, but this includes nuclear, hydro, geothermal, storage, EAC agreements, and other CFE. Do not use full 29+ GW as zero-water in the default. |
| Google aggregate-adjusted cross-check | 29+ NA aggregate + 1.17 Clearway + 1.00 TotalEnergies - 2.085 to 4.415 known non-zero-water CFE | 26.8-29.1 | Medium-low | Not used in default because the aggregate is rounded and not resource-specific. Range subtracts signed/known hydro/nuclear/geothermal/fusion at the high end and the full hydro framework at the low end. |
| Google 2025 BNEF/BCSE chart split | 4.181 GW US offsite PPAs; digitized stacked bar: solar 106 px + wind 29 px over 212 px | ~2.66 zero-water | Medium | Corroborating chart-derived evidence only, not additive to Google's cumulative 29+ GW North America aggregate. Same chart implies ~1.52 GW hydro/nuclear in Google's 2025 US offsite PPAs. |
| Amazon current US named wind/solar | 18,112.41 MW solar + 4,378.42 MW wind | 22.491 | High | Live Amazon CSV. Excludes 3,120 MW US nuclear and 21.33 MW unlabeled / Whole Foods records from strict default. |
| Meta current US numeric wind/solar map | 129 numeric US wind/solar records | 19.558 | Medium-high | Live Meta energy-page marker array. Five US records have blank capacity and are excluded. |
| Microsoft US contracted renewables | 26.252 official map - 0.102 Hawk's Nest hydro | 26.150 | High for renewable map / medium-high for zero-water | Official Dec. 31, 2025 Microsoft map. Microsoft project examples identify Hawk's Nest hydropower; LIHI lists it at 102 MW. The >90% PPA disclosure is an energy-share statement, not a capacity de-rate. Residual uncertainty is any additional undisclosed US hydropower or other non-zero-water renewable resource. |
| **Total** | 16.700 + 22.491 + 19.558 + 26.150 | **84.899** | Medium-high | Google is the only material proxy. |
| **Aggregate-adjusted total** | Google 26.8-29.1 + Amazon 22.491 + Meta 19.558 + Microsoft 26.150 | **95.0-97.3** | Medium | Sensitivity only; excluded from model default. |

### What Is Still Missing
- Google does not publish a US-only or North-America wind/solar-only project table for 2025. The current 29+ GW North America figure is clean-energy, not zero-water-only, and Google's methodology says the GW total can include PPAs, storage agreements, and EAC agreements.
- Amazon's current CSV contains 21.33 MW of unlabeled / Whole Foods rows. They are likely on-site solar but are excluded from the strict named wind/solar default.
- Meta's current map has five US wind/solar records with blank capacity.
- Microsoft does not publish a complete US project-level renewable PPA table by resource; the ISO/RTO map is the best public source. The known Hawk's Nest hydro project is now subtracted. The remaining risk is not the >90% PPA share, which is an energy metric, but possible additional undisclosed non-zero-water renewable resources inside the regional map.
- Google and Microsoft still lack exact cumulative default solar/wind splits. The new split diagnostic uses the BCSE/BNEF 2026 Factbook's annual 2025 US offsite buyer chart as a proxy ratio and should not be treated as a project-level inventory.
- Delivered-energy estimates remain separate from contracted capacity. A signed GW count should not be used as if all projects are online and generating in the footprint year.

### Traceability Hardening Pass (2026-07-01)
No number changed. The change was to make the audit trail explicit in every surface a reviewer is likely to use: the on-page PPA ledger, Source Mapping, Evidence Snippets, the exported trace, and `ppa_big4_us_dataset.csv`.

| Component | Public trace surface | Reproducible extraction | Confidence | Main failure mode |
|---|---|---|---|---|
| Google | 2026 report, operations page, BCSE/BNEF Factbook, Clearway, TotalEnergies, Brookfield hydro, Duane Arnold nuclear, Kairos nuclear, Fervo geothermal, CFS fusion | Default keeps 16.700 GW floor; sensitivity starts with 29+ GW NA clean-energy, adds 2026 solar/wind, subtracts known non-zero-water CFE; BNEF/BCSE page 44 chart supports ~2.66 GW 2025 US offsite solar/wind vs ~1.52 GW hydro/nuclear | Medium as lower bound | No public US/NA wind-solar project table; higher aggregate-adjusted range remains a sensitivity only |
| Amazon | Company project page and live CSV | Filter Country = United States; include named wind/solar; sum System Size MW = 22.491 GW | High for contracted capacity | Live CSV/COD fields can change; COD-derived delivered vintages stay separate from contracted capacity |
| Meta | Energy map and 2025 data index | Parse live map records; filter US wind/solar; include 129 numeric records = 19.558 GW | Medium-high | Five blank-capacity US wind/solar map records excluded until Meta publishes capacities |
| Microsoft | Feb 2026 procurement blog, official US map image, project examples, LIHI Hawk's Nest certificate | Sum US ISO/RTO contracted map values = 26.252 GW; subtract 0.102 GW identified Hawk's Nest hydro = 26.150 GW | High for map / medium-high for zero-water | Regional map is not a full project-level resource table; additional undisclosed hydro would need removal if found |
| Default total | Ledger + Source Mapping + Evidence Snippets + CSV + export trace | 16.700 + 22.491 + 19.558 + 26.150 = 84.899 GW; sensitivity = 95.0-97.3 GW | Medium-high | Signed GW is not delivered MWh; delivered-energy scenarios remain the year-matched displacement basis |

### Solar/Wind Split Pass (2026-07-03)
No default-capacity number changed. This pass adds a diagnostic resource split for the **84.899 GW** contracted full-build default.

| Component | Solar GW | Wind GW | Method | Confidence |
|---|---:|---:|---|---|
| Amazon | 18.112 | 4.378 | Exact live CSV split: Country = United States; named/site solar and wind rows; excludes 3.120 GW nuclear and 0.021 GW unlabeled rows. | High |
| Meta | 16.747 | 2.811 | Exact live map split: CONUS numeric records by type; excludes four blank solar records and one blank wind record. | Medium-high |
| Google | 13.113 | 3.587 | Estimated split: BCSE/BNEF page 44 Google 2025 US offsite chart has 4.181 GW total; digitized solar 106 px and wind 29 px over 212 px total, giving 2.091 GW solar and 0.572 GW wind. Apply that zero-water ratio to the 16.700 GW floor. | Low-medium |
| Microsoft | 19.315 | 6.835 | Estimated split: BCSE/BNEF page 44 Microsoft 2025 US offsite chart has 1.244 GW total; digitized solar/wind areas 2,470 / 874 over 3,344, giving 0.919 GW solar and 0.325 GW wind. Apply that ratio to the 26.150 GW zero-water adjusted map total. | Low-medium |
| **Default diagnostic total** | **67.287** | **17.611** | Mixed exact/inferred estimate = about **79.3% solar / 20.7% wind**. Use for capacity-factor sanity checks only, not as an independent source of PPA capacity. | Medium diagnostic |

## PPA / Zero-Water Procurement Addendum (2026-06-08; superseded by 2026-06-30)

### Result
- **Default tracked zero-water clean-energy procurement capacity** now uses **80.589 GW**, up from the prior **80.359 GW** strict off-site-only framing.
- **Google** updated from the **6.485 GW** legacy strict US floor to **17.300 GW** as a central North America proxy. Google's current public reporting gives **>22 GW** of clean-energy agreements globally and **>17.3 GW** in North America. BNEF/BCSE separately reports Google signed **4,181 MW** of US offsite corporate clean-energy PPAs in 2025 alone, confirming that the old floor materially undercounts current Google procurement.
- **Amazon** corrected from **19.874 GW** strict off-site floor to **20.104 GW** zero-water procurement total. The current Amazon CSV lists **20,103.99 MW** of US wind/solar/solar+storage projects, including **230.06 MW** of US on-site solar. Because this dashboard models water displacement from zero-operational-water procurement, the on-site solar remains included. The narrower off-site-only floor remains **19,873.93 MW** for sensitivity context only.
- **Meta** updated from **9.800 GW** to **19.558 GW**. The current Meta energy-page map includes 134 US wind/solar records; 129 have numeric capacity values totaling **19,558 MW**. Blank-capacity records are excluded.
- **Microsoft** remains **26.252 GW x 90% = 23.627 GW**. The Feb. 18, 2026 Microsoft blog/map supports the US contracted sum, and the blog states that >90% of the contracted portfolio is under PPAs or similar long-term contracts. This remains a proxy because Microsoft does not publish an explicit US resource-level renewable PPA-only split.

### Calculation Trace
| Component | Calculation | Included GW | Status |
|---|---:|---:|---|
| Google North America clean-energy agreements proxy | Google-reported >17.3 GW North America | 17.300 | Updated central proxy |
| Google strict US disclosed floor | 6.485 + 1.170 + 1.000 + 0.200 | 8.855 | Floor sensitivity only |
| Google BNEF 2025 US offsite cPPA context | BNEF/BCSE top buyer chart: 4,181 MW in 2025 | 4.181 | Annual 2025 context only |
| Amazon US zero-water wind/solar/solar+storage project total | 20,103.99 MW / 1,000 | 20.104 | Updated water-boundary default |
| Meta current US numeric wind/solar records | 19,558 MW / 1,000 | 19.558 | Updated |
| Microsoft US contracted proxy | 26.252 GW x 0.90 | 23.627 | Unchanged |
| Default tracked zero-water procurement baseline | 17.300 + 20.104 + 19.558 + 23.6268 | 80.589 | Updated |

### Caveats
- These are **clean-energy procurement/project-list capacity inputs**, not delivered MWh. The calculator separately converts GW to TWh using the user-editable capacity factor.
- Google is now a **North America proxy**, not a strict US-only value. This is less conservative but better reflects where Google data centers and clean-energy procurement are concentrated. The BNEF 2025 US number is annual and offsite-only, so it validates scale but should not be added to the North America cumulative total.
- Microsoft remains a proxy because the current US map is not published as a resource-level PPA-only table.
- The values are current to public source pages/reports checked on **2026-06-08**.

## Claim-by-Claim Audit

*Claims 1–16, 18–34 were verified in the 2026-02-25 audit. Claims E1–E16 were verified in the 2026-02-26 ethanol sub-audit. Only changed, new, or still-open claims are detailed below. For full details on previously verified claims, see the Change Log section.*

### Claim 17 (UPDATED): "Golf courses (US) consume 292 Bgal/year"
- **Location**: `industryAnnualBgal` array, line 1359
- **Type**: Statistic
- **Source claimed**: S5 (GCSAA Golf Environmental Profile Phase IV; HortTechnology 35(5), 2025)
- **What GCSAA Phase IV actually reports**: **1.63 million AF applied in 2024** (confirmed via GCSAA press release S5c, GCSAA PDF S5b, Golf Wire coverage, Golf Course Industry coverage)
- **Conversion**: 1.63M AF × 325,851 gal/AF = **~531 Bgal/year applied**
- **At 80% consumptive**: ~425 Bgal/year consumed
- **Where 292 likely comes from**: Brian Potter's informal blog estimate (S6): "about a billion gallons of water a day" × 365 × ~80% ≈ 292. This is ~55% of the GCSAA figure.
- **Verdict**: ❌ SIGNIFICANT ISSUE
- **Confidence**: HIGH (GCSAA primary source confirmed via multiple independent outlets)
- **Issue**: The dashboard attributes 292 to "GCSAA Golf Environmental Profile Phase IV" but the actual GCSAA data shows ~531 Bgal applied / ~425 Bgal consumed. The source label is misleading — the figure traces to Potter, not GCSAA.
- **Impact on narrative**: The undercount is **conservative** (makes data centers look larger relative to golf). Correcting to 531 or 425 would make golf even larger vs data centers. The "rounding error" conclusion gets stronger.
- **Recommendation**:
  - **Option A (preferred)**: Update to 531 Bgal/yr applied (GCSAA primary) or 425 Bgal/yr consumed (×80%)
  - **Option B**: Keep 292 as ultra-conservative lower bound, but change source label from "GCSAA Phase IV" to "Potter synthesis (conservative); GCSAA Phase IV reports ~531 applied"
  - The assumption trace row already labels it "legacy synthesis benchmark" — that internal honesty should surface in the public-facing source label

### Claim 19 (UPDATED): "Residential swimming pools (US) consume 56 Bgal/year"
- **Location**: `industryAnnualBgal` array, line 1373
- **Type**: Calculation
- **Calculation check**: 7.5M pools × 7,500 gal/yr = 56.25 ≈ 56 Bgal/yr ✓
- **Source label**: "7.5M pools (CAPE Analytics satellite) × 7,500 gal/yr size- & climate-weighted evap (EPA WaterSense)"
- **Prior audit**: Deep audit (S20) confirmed 56 Bgal as conservative lower bound of 56–110 range
- **Verdict**: ✅ VERIFIED (conservative, properly sourced and labeled)
- **Confidence**: HIGH
- **Notes**: Significant improvement from the prior 110 Bgal figure. Source label now transparent about methodology.

### Claim 36 (NEW): "Orchards (almonds, etc.) irrigation: 7.9 Bgal/day"
- **Location**: `agricultureBgalDay` array, line 1389
- **Type**: Statistic
- **Conversion check**: 7.9 Bgal/day × 365 × 1e9 / 325,851.429 = 8,849,125 AF/year ✓
- **Source**: NOT in source mapping table. The ag note (line 760) cites "Lamsal & Marston (2025)" for crop values, but orchards/almonds are not listed in the explicit AF/year values in the source mapping (line 953). The figure likely derives from Construction Physics (Potter) synthesis, not directly from Lamsal & Marston.
- **Verdict**: ⚠️ MINOR ISSUE
- **Issue**: Orchards is the only ag chart row without a corresponding entry in the source mapping table and without an explicit AF/year figure listed. All other ag rows (alfalfa, other hay, cotton, alfalfa-China, all irrigation) have explicit AF/year values in the source mapping.
- **Recommendation**: Add an orchards AF/year entry to the source mapping table (~8,849,125 AF/year) with proper source attribution (Lamsal & Marston 2025 if traceable, or note the derivation).
- **Confidence**: MEDIUM — the value is plausible for US orchard irrigation but needs source documentation

### Claim 37 (NEW): "Last verified on February 24, 2026"
- **Location**: Header subtitle, line 648
- **Type**: Metadata
- **Verdict**: ⚠️ MINOR ISSUE
- **Issue**: The dashboard claims "last verified on February 24, 2026" but today is March 29, 2026 — over one month since last verification. No source data has materially changed in this window, but the date should be updated when any corrections are applied.
- **Recommendation**: Update to current date when next changes are made.

### Claim 38 (NEW): Google replenishment "~64% of consumption"
- **Location**: Buildout assumptions note, line 858
- **Type**: Corporate statistic
- **Source**: S12 (Google 2025 Environmental Report)
- **Source says**: "from 18% in 2023 to 64%" — this is percentage of **freshwater consumption** (~7.0–7.2B gal), not total consumption (~8.1B gal)
- **Verdict**: ⚠️ MINOR ISSUE
- **Issue**: The text says "~64% of consumption" without specifying "freshwater." Against total consumption it would be ~55%.
- **Recommendation**: Change to "~64% of freshwater consumption" for precision. This is Google's own framing.
- **Confidence**: HIGH

### Claim 4 (UNCHANGED): LBNL 2028 projection range
- **Verdict**: ❓ UNVERIFIABLE — still access-restricted
- **Confidence**: MEDIUM

### Claim E14 (UNCHANGED): Sampson et al. ~4% Kansas irrigation
- **Verdict**: ❓ UNVERIFIABLE — still paywalled
- **Confidence**: LOW

## Apples-to-Apples Audit
| Comparison | Left Side Scope | Right Side Scope | Aligned? | Notes |
|---|---|---|---|---|
| Data centers vs golf | DC on-site + grid water, consumptive | Golf irrigation applied (GCSAA) or applied × 80% consumptive | ⚠️ | If using 531 Bgal applied: not strictly apples-to-apples (applied ≠ consumed). If using 425 Bgal consumed: aligned. |
| Data centers vs pulp/paper | DC on-site + grid water, consumptive | NCASI withdrawals × 7% low-end consumptive | ✅ | Conservative; both measure consumptive water |
| Data centers vs swimming pools | DC on-site + grid water, consumptive | Pool evaporation (100% consumptive by nature) | ✅ | Same physical mechanism |
| Data centers vs RFS ethanol | DC total (all consumption) | Marginal irrigation (policy counterfactual) | ⚠️ | Asymmetry is clearly disclosed in chart note. Total ethanol water (1.0–1.4T gal) is 5–7× larger. Conservative. |
| Data centers vs agriculture | DC total, consumptive | Lamsal & Marston blue water consumption | ✅ | Both measure consumptive (evaporated/incorporated) |
| Industry chart vs USGS denominator | Industry annual Bgal converted to kAF | USGS 2020 modeled consumptive use | ✅ | Same units, same scope |

## Calculation Verification
All calculations from prior audits re-confirmed. Key new verification:

| Calc | Input | Formula | Expected | Actual | Match? |
|------|-------|---------|----------|--------|--------|
| Orchards AF/yr | 7.9 Bgal/day | × 1e9 / 325,851.429 × 365 | 8,849,125 | 8,849,124.9 | ✅ |
| Golf (GCSAA) | 1.63M AF × 325,851 gal/AF | to Bgal | ~531 | 531.1 | ✅ |
| Golf (consumed) | 531 × 0.80 | | ~425 | 424.9 | ✅ |
| All prior calcs | See 2026-02-25 report | | | | ✅ |

## Cross-Source Discrepancies
| Figure | Source A | Source B | Delta | Explanation |
|--------|---------|---------|-------|-------------|
| Golf Bgal/yr | Dashboard: 292 | GCSAA Phase IV: ~531 applied / ~425 consumed | -44% to -31% | Dashboard uses Potter synthesis; GCSAA shows 1.63M AF applied. Dashboard is conservative. |
| Meta replenishment | Dashboard: 1.5B gal | Meta precise: 1.59B gal | 6% | Conservative rounding (unchanged from prior audit) |

## Unresolved Questions
- [ ] **Golf figure**: Should update to GCSAA Phase IV primary data (531 applied or 425 consumed). Current 292 is from informal secondary source but attributed to GCSAA.
- [x] **Orchards source** (closed 2026-07-02): Source mapping entry added (`ag_benchmark_orchards_af_year` = 8,849,125 AF/yr), attributed as a Construction Physics synthesis benchmark; explicitly noted as not itemized in the Lamsal & Marston extract. A primary-source trace (e.g., Lamsal & Marston full data) would still upgrade it.
- [ ] **Sampson et al. (2021)**: Full text still needed for 4% Kansas irrigation claim verification.
- [ ] **LBNL 2028 projections**: Report access still restricted.
- [ ] **Buildout linearity assumption**: New builds may have better WUE (Microsoft zero-water, AWS 0.15 L/kWh), potentially making the 2025 linear-scaled estimate slightly high. Not currently quantifiable.

## Framing Notes
- The dashboard's narrative conclusion ("rounding error" relative to peer sectors) remains **robust across all scenarios and corrections**. Even correcting golf upward to 531 Bgal *strengthens* the conclusion.
- The disclosure gap note (no federal industrial water reporting since 1983) is verified and genuinely distinctive.
- Conservative errors consistently favor data centers looking *larger*, not smaller — this is the right direction for credibility.
- The RFS ethanol comparison is the most editorially bold element. Using marginal (192 Bgal) rather than total (1,000–1,400 Bgal) is well-documented and transparent.
- The "last verified" date (Feb 24) is mildly stale but no underlying source data has changed in the intervening month.

## Recommendations (Priority Order)

1. **Fix golf source attribution** (Claim 17): Either update figure to GCSAA Phase IV primary data (~531 applied or ~425 consumed) OR change source label to clearly indicate 292 is from Potter synthesis, not GCSAA. The current state — 292 attributed to GCSAA Phase IV — is factually incorrect.

2. **Add orchards to source mapping** (Claim 36): Add a row with ~8,849,125 AF/year and proper source citation. This is the only ag chart row without a source mapping entry.

3. **Clarify Google replenishment denominator** (Claim 38): Change "~64% of consumption" to "~64% of freshwater consumption."

4. **Update "last verified" date** when corrections are applied.

## Change Log
| Date | Auditor | Scope | Key Findings |
|------|---------|-------|-------------|
| 2026-02-24 | Claude | Swimming pools claim (110 Bgal) | Per-pool evap overstated; revised to 56 Bgal conservative |
| 2026-02-25 | Claude | Full audit (35 claims) | Evidence snippet quotes wrong USGS numbers; golf 292 understated and source URL dead; core math verified |
| 2026-02-26 | Claude | RFS ethanol section (16 claims) | 2 minor issues (">90%" conflation, "acreage" wording); 0 significant; Sampson paywalled |
| 2026-03-29 | Claude | Incremental full audit (39 claims) | 5 of 7 prior issues FIXED. Golf 292 still open (GCSAA confirms 531 applied). New findings: orchards missing from source mapping; "last verified" date stale; Google replenishment needs "freshwater" qualifier. Overall confidence remains HIGH. |
| 2026-06-03 | Codex | PPA capacity trace | Updated default tracked signed PPA baseline from 59.955 GW to 80.359 GW. Amazon off-site floor corrected to 19.874 GW; Meta current US numeric wind/solar records updated to 19.558 GW; Google moved to 17.300 GW North America clean-energy agreements proxy after BNEF/BCSE cross-check; Microsoft proxy unchanged. |
| 2026-06-08 | Codex | Zero-water procurement boundary | Updated active baseline from 80.359 GW to 80.589 GW by retaining Amazon's 230.06 MW of US on-site solar. Rationale: the dashboard models water displacement from zero-operational-water procurement, not a strict off-site PPA-only market boundary. |
| 2026-06-23 | Claude | Delta re-audit (current working tree) | 3 of 4 prior open/minor issues now FIXED in the file: golf corrected to 425 Bgal/yr (GCSAA primary, consumptive) resolving the standing ❌; Google replenishment now "~64% of freshwater consumption"; "last verified" date refreshed. **Orchards source-mapping gap STILL OPEN** (7.9 Bgal/day ag row has no `ag_benchmark` entry). No new issues introduced June 8→19. Confidence remains HIGH. |
| 2026-06-30 | Codex | PPA/source refresh and deep pass | Updated contracted full-build zero-water capacity to 84.899 GW strict lower-bound default. New components: Google 16.700 GW NA zero-water floor, Amazon 22.491 GW live CSV named US wind/solar, Meta 19.558 GW live map numeric US wind/solar, Microsoft 26.150 GW zero-water-adjusted US map after subtracting 102 MW Hawk's Nest hydro. Added BNEF/BCSE chart-derived Google 2025 US offsite split (~2.66 GW solar/wind; ~1.52 GW hydro/nuclear) and non-default Google aggregate-adjusted cross-check implying 95.0-97.3 GW Big-4 total, but kept it outside the model default because Google does not publish a regional resource-specific table. |
| 2026-07-01 | Codex | PPA traceability hardening | No numeric change. Added on-page PPA traceability ledger, direct links for Google non-zero-water exclusions (Duane Arnold, Fervo, CFS), Microsoft Hawk's Nest project/capacity links in the Evidence Snippets row, export-trace confidence/failure-mode lines, assumption rows for PPA traceability surfaces and residual risks, and CSV cross rows documenting audit surfaces and default residual risks. |
| 2026-07-02 | Claude | Orchards gap closed + evidence-layering pass | **Orchards STILL-OPEN item FIXED**: `ag_benchmark_orchards_af_year` added to the assumption-trace source mapping (7.9 Bgal/day = 8,849,125 AF/yr), labeled honestly as a Construction Physics synthesis benchmark (USDA/USGS-derived) not itemized in the Lamsal & Marston extract; HTML Source Mapping ag-baselines row and source links updated to match. Non-substantive evidence-layering changes: fact-check badge in header; provenance lines under headline/scale cards linking to anchored Source Mapping rows (`source-lbnl-direct`, `source-buildout-scale`, `source-usgs-denominator`, etc.); visible source lines under industry/RFS/agriculture charts; two longest Advanced Settings hints trimmed to one line + anchor (full detail unchanged in Source Mapping). No model values changed; script syntax and all 27 internal anchors verified. |
| 2026-07-03 | Codex | PPA solar/wind split diagnostic | No change to the 84.899 GW PPA default. Added split estimate of 67.287 GW solar + 17.611 GW wind (79.3% / 20.7%). Amazon and Meta are exact source-derived splits; Google and Microsoft are conservative BCSE/BNEF chart-derived estimates because exact cumulative resource tables remain unpublished. Mirrored trace into on-page ledger, Source Mapping, Evidence Snippets, CSV, export trace, and this memo. |

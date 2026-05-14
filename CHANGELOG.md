# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.12.0] - 2026-05-14

### Added
- Bilingual placeholder examples (Japanese / English) in the search box
- Tagline under the header explaining the multi-source, API-extensible architecture
- Bilingual IHME CSV upload instructions

### Changed
- Bumped version label to "v0.12 · API-extensible ✨"

## [0.11.0] - 2026-05-14

### Added
- **IHME GBD CSV upload** feature: load user-supplied CSVs from the IHME GBD Results Tool
- Auto-detection of cause × measure × metric combinations as separate indicators
- Location-name to ISO3 mapping for 40+ countries
- PapaParse dependency for CSV parsing
- Orange-styled upload UI in the sidebar

### Changed
- `ALL_META` refactored to a Proxy object that merges WDI + OWID + dynamically-loaded IHME indicators
- Chart and pill rendering now distinguishes three sources (WDI / OWID / IHME)

## [0.10.0] - 2026-05-14

### Removed
- All IHME/GBD-licensed OWID indicators (Parkinson's, depression, anxiety, schizophrenia,
  bipolar disorder, drug use disorders, alcohol use disorders, cardiovascular death rate,
  air pollution death rate, road traffic death rate). These cannot be redistributed under
  IHME's license; OWID returns 403 for their CSV endpoints.
- Related natural-language keywords (depression, anxiety, parkinson, drug use, etc.)

### Changed
- OWID section limited to 7 WHO/UNAIDS/JHU-sourced indicators that allow redistribution
- Warning banner now explains the IHME license restriction and points to vizhub.healthdata.org
  for direct user access
- Source labels: "OWID/GBD" → "OWID"

## [0.9.0] - 2026-05-14

### Added
- 15 new OWID indicators across 5 disease categories: mental health (depression, anxiety,
  schizophrenia, bipolar), substance use (drug use disorder, alcohol use disorder, alcohol
  intake), metabolic (obesity, diabetes, cardiovascular death), infectious (HIV, TB, COVID),
  environment & social (smoking, air pollution, road deaths)
- Category-based sub-headers in the OWID indicator list (🧠 mental, 💊 substance, etc.)
- Bilingual keyword parsing for new indicators

### Note
This version was later found to be broken: IHME-sourced OWID slugs return 403 Forbidden.
Resolved in v0.10 by removing IHME indicators entirely.

## [0.8.0] - 2026-05-14

### Removed
- e-Stat (Japanese government statistics) integration removed entirely:
  - "e-Stat 🇯🇵" toggle
  - appId input field and session persistence
  - 5 e-Stat indicators (drug arrests, suicides, births, population, Parkinson's patients)
  - JSONP fallback fetch logic
  - `fetchEstat` parser (~200 lines)
- Related natural-language keywords (drug arrests, etc.)

### Changed
- Bumped version label to "v0.8 · clean ✨"
- Placeholder examples updated to remove Japan-specific references

## [0.7.0] - 2026-05-14

### Changed
- **Complete visual restyle to anime aesthetic**:
  - Sky-blue gradient background with sun glow and cloud layers
  - Subtle grid pattern overlay (90s/00s anime background cliche)
  - M PLUS Rounded 1c (body) + Klee One (headings) typography
  - Pink (#ff5c8a) primary + yellow (#ffd23f) accent palette
  - Fully rounded buttons (border-radius: 999px) with depth shadows
  - Title "Explorer" gets a yellow highlight underline marker
  - Star symbols (✦) before sidebar h3 headings
  - 16px rounded corners on all panels with 2px borders

### Removed
- Fraunces serif font (editorial style)
- JetBrains Mono font (was used for code-like labels)
- italic emphasis styling throughout

## [0.6.0] - 2026-05-14

### Fixed
- **e-Stat parser bug**: previously, only `cat01` dimension was checked for "total" rows,
  causing age-group breakdown rows to leak into totals (sawtooth chart for Parkinson
  patient counts). Now applies strict total-matching (`^総数|^合計|^全|^Total`) across
  ALL category dimensions, treating a row as grand total only when every non-breakdown
  dim matches its total code. Year-level deduplication added.

### Added
- OWID indicators show "⚠ local" badge (preview frame fetch blocked)
- Local-only warning banner above results when an OWID indicator is selected

## [0.5.0] - 2026-05-14

### Added
- Parkinson's disease indicators via OWID/GBD (prevalence, incidence, mortality, DALY)
- e-Stat appId paste support (cross-tab clipboard handling)

### Fixed
- OWID slug corrections (Parkinson incidence: added `-ihme` suffix; death rate: `-ghe` suffix)

## [0.4.0] - 2026-05-14

### Added
- e-Stat (Japanese government statistics) integration with JSONP fallback
- 5 e-Stat indicators: drug arrests, suicides, births, population, Parkinson patients

## [0.3.0] - 2026-05-14

### Added
- Direction icons (↑good / ↓bad / ◐neutral) for all indicators
- OECD SDMX integration
- Year alignment modes (each country's latest vs common latest)
- Metadata tooltips on indicator items

## [0.2.0] - 2026-05-14

### Added
- Multi-indicator support
- Small-multiples chart layout

## [0.1.0] - 2026-05-14

### Added
- Initial MVP with WDI / WHO / OECD / PubMed
- Editorial Fraunces design
- World map with bubble overlay
- CSV export

[0.12.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.12.0
[0.11.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.11.0
[0.10.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.10.0
[0.9.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.9.0
[0.8.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.8.0
[0.7.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.7.0
[0.6.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.6.0
[0.5.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.5.0
[0.4.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.4.0
[0.3.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.3.0
[0.2.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.2.0
[0.1.0]: https://github.com/hiroki-tamba-research/research-data-explorer/releases/tag/v0.1.0

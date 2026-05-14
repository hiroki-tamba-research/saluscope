# Saluscope

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20175133.svg)](https://doi.org/10.5281/zenodo.20175133)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Multi-source health & development data explorer via open APIs.
> Extensible to any indicator (WDI / OWID / IHME / your own).

A single-file, zero-build HTML application for exploring international health and development indicators across the World Bank (WDI), WHO/UNAIDS/JHU (via Our World in Data), and the IHME Global Burden of Disease study. Natural-language search, interactive world map, time-series charts, CSV export.

**Live demo:** open `index.html` in any modern browser. No installation, no build step.

## Features

- 🌐 **Multi-source API integration**: World Bank WDI (12 indicators), OWID/WHO/UNAIDS/JHU (7 indicators), PubMed literature search
- 📂 **IHME CSV upload**: bring your own GBD Results CSV; auto-detects cause × measure × metric combinations and registers them as searchable indicators
- 🔍 **Natural-language queries**: bilingual (Japanese/English) keyword parsing — `北欧の自殺率` or `suicide rates in Nordic countries` both work
- 🗺 **Interactive world map**: D3 + topojson bubble overlay, year alignment toggle (each country's latest vs common latest year)
- 📊 **Small-multiples charts**: time series per country, direction-aware color coding (↑good / ↓bad / ◐neutral)
- 📑 **CSV export**: all retrieved data in one click
- 🎨 **Anime-styled UI**: M PLUS Rounded 1c + Klee One typography, pastel palette
- ⚡ **Zero dependencies at build time**: D3, topojson, PapaParse loaded from CDN at runtime

## Quick start

1. Download `index.html`
2. Open in any modern browser (Chrome, Firefox, Safari, Edge)
3. Type a query (e.g. "japan diabetes obesity") or click indicators in the sidebar
4. Click **Search**

OWID indicators require running the file locally (`file://`) — Claude.ai's iframe sandbox blocks cross-origin fetches.

## Adding IHME GBD data

For disease burden indicators not in OWID's redistributable set (Parkinson's, depression, drug use disorders, etc.):

1. Create a free account at [https://vizhub.healthdata.org/gbd-results/](https://vizhub.healthdata.org/gbd-results/)
2. Select your cause × measure × metric × locations × years
3. Download as CSV
4. Click **📂 Select CSV / CSVを選択** in the Explorer sidebar

The CSV must contain these columns (default in GBD Results exports):
`measure_name, location_name, sex_name, age_name, cause_name, metric_name, year, val`

The tool auto-filters to `sex_name == 'Both'` and `age_name == 'All ages'` or `'Age-standardized'` for aggregate views.

## Data sources & licensing

| Source | Indicators | License | In-app behavior |
|---|---|---|---|
| World Bank WDI | Life expectancy, mortality, fertility, GDP, etc. | CC BY 4.0 | Direct API fetch |
| OWID (WHO/UNAIDS/JHU upstream) | Obesity, diabetes, smoking, HIV, TB, COVID, alcohol | CC BY 4.0 | Direct CSV fetch |
| IHME GBD | Disease burden (any) | Custom (no redistribution) | User-supplied CSV |
| PubMed E-utilities | Literature search | Public domain | Direct API fetch |

This tool does **not** redistribute IHME data. Users must obtain GBD Results CSVs themselves under IHME's terms.

## Citation

If you use this tool in your research, please cite:

```bibtex
@software{tamba_saluscope,
  author       = {Tamba, Hiroki},
  title        = {Saluscope: Multi-source health and development data via open APIs},
  year         = 2026,
  publisher    = {Zenodo},
  version      = {v0.12.0},
  doi          = {10.5281/zenodo.20175133},
  url          = {https://github.com/hiroki-tamba-research/saluscope}
}
```

See [CITATION.cff](CITATION.cff) for the structured citation file (auto-recognized by GitHub).

## Architecture

Single HTML file. CSS, JavaScript, and templates inline. External dependencies loaded from CDN:

- [D3.js](https://d3js.org/) v7.8.5 — visualization
- [topojson](https://github.com/topojson/topojson) v3.0.2 — world map geometry
- [PapaParse](https://www.papaparse.com/) v5.4.1 — IHME CSV parsing

No package manager, no bundler, no transpiler. Open the HTML; it works.

## Roadmap

- [ ] Additional API integrations: UNODC drug statistics, OECD Health Statistics, FRED
- [ ] DOI-cited data snapshots (export bundle: data + provenance + Zenodo-deposited)
- [ ] Multi-indicator correlation views
- [ ] User-defined indicator plugins via small JS adapter modules

## Contributing

Issues and PRs welcome. The codebase is deliberately small (~1500 lines of JS) and unbundled to make modification easy. Adding a new API source typically means:

1. Add a metadata block (like `INDICATOR_META` or `OWID_META`)
2. Add a fetch function (like `fetchWDI` or `fetchOWID`)
3. Add the source's name to the toggle row
4. Add a dispatch case in `runSearch`

About 50 lines of code total per new source.

## License

MIT — see [LICENSE](LICENSE).

## Author

Hiroki Tamba ([@TambaClan](https://x.com/TambaClan)) — Narrative & Governance / independent research on classification cascades, cognitive governance, and AI-era epistemic infrastructure.

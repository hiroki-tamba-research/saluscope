# 30-Minute DOI Setup Guide

This guide walks you through publishing **Research Data Explorer** as a citable software artifact with a permanent DOI via Zenodo + GitHub.

**Estimated total time: 30 minutes.**

## What you'll have at the end

- A GitHub repository at `https://github.com/hiroki-tamba-research/research-data-explorer`
- A Zenodo deposit with a permanent DOI like `https://doi.org/10.5281/zenodo.XXXXXXX`
- A "Cite this software" button on your GitHub repo
- Auto-updating: future Releases automatically mint new versioned DOIs

---

## Step 1 — Create the GitHub repository (5 min)

1. Go to **https://github.com/new**
2. Repository name: `research-data-explorer` (or your choice; if you change it, update the URLs in `README.md`, `CITATION.cff`, `.zenodo.json`)
3. Description: `Multi-source health & development data explorer via open APIs. Extensible to any indicator.`
4. Set to **Public**
5. **Do NOT** initialize with README, .gitignore, or license — we'll push our prepared files
6. Click **Create repository**

You'll see a page with setup instructions. Keep it open; we'll need the repo URL.

---

## Step 2 — Push the prepared files (5 min)

The Claude session has prepared the following files in `/home/claude/repo/`:
- `index.html` (v0.12 of the tool)
- `README.md`
- `CITATION.cff`
- `.zenodo.json`
- `LICENSE` (MIT)
- `CHANGELOG.md`
- `HOWTO_DOI.md` (this file)

Download all of these to a folder on your machine. Then in that folder:

```bash
# Before running git commands, replace USERNAME placeholders in the files
# (README.md, CITATION.cff have `USERNAME` strings to swap to your GitHub handle)

git init
git add .
git commit -m "Initial commit: v0.12 — API-extensible health data explorer"
git branch -M main
git remote add origin https://github.com/hiroki-tamba-research/research-data-explorer.git
git push -u origin main
```

After push, refresh the GitHub page. You should see the files and a rendered README.

GitHub will also detect `CITATION.cff` automatically and show a **"Cite this repository"** button on the right sidebar within a few minutes.

---

## Step 3 — Connect Zenodo to GitHub (5 min)

1. Go to **https://zenodo.org/account/settings/github/**
2. Sign in with GitHub (Zenodo supports GitHub SSO)
3. Authorize Zenodo to access your repositories (read-only is fine)
4. On the Zenodo GitHub settings page, find `research-data-explorer` in the list
5. Flip the toggle **ON** for that repository

Zenodo is now watching your repo. The next Release you create will be archived automatically.

---

## Step 4 — Create a GitHub Release to mint the DOI (5 min)

1. On your repo page, click **Releases** in the right sidebar
2. Click **Create a new release** (or **Draft a new release**)
3. **Tag version**: `v0.12.0` (must start with `v` for semver; Zenodo accepts any tag but `vX.Y.Z` is conventional)
4. **Target**: `main`
5. **Release title**: `v0.12.0 — API-extensible health data explorer`
6. **Description** (paste this in):

```markdown
Initial public DOI-citable release of Research Data Explorer.

## Features
- Multi-source health & development data: World Bank WDI, OWID (WHO/UNAIDS/JHU), PubMed
- IHME GBD CSV upload: auto-detects cause × measure × metric combinations
- Bilingual (Japanese/English) natural-language search
- D3-based interactive world map with bubble overlay
- Small-multiples time-series charts, CSV export
- Anime-styled UI with M PLUS Rounded 1c + Klee One typography
- Zero build step, single-file HTML, no installation

## Citation

Tamba, H. (2026). Research Data Explorer (v0.12.0) [Software]. Zenodo. https://doi.org/[FILL-IN-AFTER-RELEASE]

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for the full history.
```

7. Click **Publish release**

Zenodo will detect the release within 1–5 minutes and create a DOI. Refresh **https://zenodo.org/account/settings/github/** and click your repository; you'll see the deposit listed with its DOI.

---

## Step 5 — Update files with the real DOI (5 min)

Once you have the DOI (e.g., `10.5281/zenodo.1234567`):

1. Edit `README.md`:
   - Replace `PENDING` in the DOI badge URL with your DOI
   - Replace `PENDING` in the BibTeX block with your DOI

2. Edit `CITATION.cff`:
   - Replace `PENDING` in the `value:` line under `identifiers:` with your DOI

3. Commit and push:

```bash
git add README.md CITATION.cff
git commit -m "Add real DOI from Zenodo"
git push
```

The GitHub "Cite this repository" button will now show the DOI in the citation block.

---

## Step 6 — Verify everything works (5 min)

1. Open your repo's main page. Confirm:
   - [ ] README renders correctly with the DOI badge clickable and resolving
   - [ ] "Cite this repository" sidebar button works and shows citation in 4 formats (APA, BibTeX, etc.)
   - [ ] Releases tab shows v0.12.0 with the description

2. Open your Zenodo deposit URL (e.g., `https://zenodo.org/records/1234567`):
   - [ ] All files from the GitHub release are archived
   - [ ] DOI resolves via `https://doi.org/10.5281/zenodo.1234567`
   - [ ] Metadata (author, keywords, description) matches `.zenodo.json`

3. Test the DOI link in a browser private window — it should redirect to your Zenodo record.

---

## Step 7 — Announce (optional but valuable for "先取り" timestamp)

This is the most important step for **establishing public timestamp evidence**:

1. **X/Twitter post** (your `@TambaClan` account):

```
新しい研究ツールを公開しました。
Research Data Explorer v0.12

世界の保健・開発データを複数のオープンAPIから一括検索・可視化。
WDI / OWID / IHME / PubMed 統合。
日英バイリンガル自然言語検索対応。

DOI: https://doi.org/10.5281/zenodo.XXXXXXX
GitHub: https://github.com/hiroki-tamba-research/research-data-explorer

#OpenScience #GlobalHealth
```

2. **Bluesky / Threads**: same content, different platforms (more timestamp anchors = stronger priority claim)

3. **Optional: ResearchGate, Mastodon (FOSDEM/academic instance)** for additional academic visibility

Each post adds an independent timestamp from a different platform's logs. Combined with the Zenodo DOI (which has a cryptographic registration timestamp via DataCite), this creates an unforgeable priority record.

---

## What to do later (v0.13+ roadmap)

When you add API sources (OECD Health, WHO direct, Eurostat, arXiv, etc.):

1. Bump version in `index.html`, `CITATION.cff` (`version:`), and `CHANGELOG.md`
2. Commit and push
3. Create a new GitHub Release with tag `v0.13.0`
4. **Zenodo automatically mints a new DOI for that version**
5. Zenodo also maintains a "concept DOI" that always points to the latest version — useful for general citation

The concept DOI never changes; only versioned DOIs change per release. Both are valid for citation.

---

## Troubleshooting

**Zenodo didn't pick up my release after 10 minutes**
- Verify the toggle is still ON at https://zenodo.org/account/settings/github/
- Check that the Release is **Published** (not Draft)
- Re-trigger by deleting and recreating the Release, or by sending a manual webhook from Zenodo's UI

**"Cite this repository" button doesn't appear on GitHub**
- Verify `CITATION.cff` syntax: `cff-version: 1.2.0` must be present at top
- It can take up to 1 hour for GitHub to index new CITATION.cff files
- Try cff-validator: https://citation-file-format.github.io/cff-validator/

**DOI badge in README shows "PENDING"**
- You forgot Step 5 — update README with the real DOI after Zenodo mints it

**Want to update authorship / add co-authors**
- Edit `CITATION.cff` and `.zenodo.json`, commit, push, then create a new Release to apply

---

## Questions to consider after DOI is live

1. **Add to your ORCID record** (https://orcid.org → Works → Add → Search & link → Zenodo). This links the software to your researcher profile across all platforms.

2. **Submit to JOSS (Journal of Open Source Software)?** JOSS gives a peer-reviewed publication for software. Requires ~200-word paper.md. Not urgent; can do later if the tool grows.

3. **Pre-print companion paper?** A short methods note on arXiv/SSRN/OSF Preprints describing the tool's architecture would add an academic anchor. Optional.

---

That's it. Total time: 30 minutes for the whole flow, with the DOI live and citable from the moment Step 4 completes.

If you hit any snags during execution, copy the error message back into Claude and I'll help diagnose.

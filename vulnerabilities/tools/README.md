# Tools

The scripts behind this Philippines-only run of global-law's vulnerability detectors. They run inside a copy of
[global-law/vulnerabilities/scripts](https://github.com/lexifina/global-law/tree/main/vulnerabilities/scripts) (Python 3.11+,
`pip install duckdb pyarrow`), with a bare clone of this repository at `sources/corpus/philippines-law.git`, a blobless bare
clone of global-law at `sources/global-law.git`, and a `pins.json` that names only philippines-law, its commit, its
language (`en`) and its code (`PH`). `build_vulns.py`, `flags_chart.py`, `late_ext_select.py`, `late_ext_rebut.py` and
`config.json` sit three folders up, next to the copy of global-law (`gl/vulnerabilities/scripts/`).

| Script | What it does |
| --- | --- |
| `run.sh` | Indexes the history and texts, adds this repository's history rows, and runs the detectors (`bash run.sh <shards>`; run here with 6) |
| `add_root.py` | Builds the history rows from this repository's own commits (global-law replays it only up to an earlier commit), so the history detectors read every change; changed for this repository (below) |
| `run_triage.sh` | The model review: the 40 strongest flags per category, the 40 strongest lapsed time limits in law texts, and the empty periods |
| `late_ext_select.py` | Chooses the empty periods for global-law's review of that category (none here) |
| `late_ext_rebut.py` | Adds the second, arguing-against pass to the empty-period review, as `triage.py` does for the other categories |
| `build_vulns.py` | Builds `data/flags.csv`, `data/reviewed.csv` and `data/by_category.csv` from the findings and the model review |
| `flags_chart.py` | Draws the chart at the top of the README, in English, light and dark |
| `config.json` | The repository, its language (English), the category names, the files and folders that are not law, and the chart's labels |
| `patch_detectors.py` | Fixes blind spots found in runs on several country repositories in the copy of global-law's scripts (`python -X utf8 patch_detectors.py <scripts dir>`; a fix already in place is skipped) |
| `patch_en.py`, `patch_en_et.py`, `patch_en_nr.py`, `patch_en_nz.py` | The same for English text (found by the Bhutan, Ethiopia, Nauru and New Zealand runs): "vacated" only as a marker, a provision that repeals another section or a whole earlier law not as a placeholder, a reprint's history notes not as references, days written "1st" or "31st" as dates, amendment directions and ranges not as references, "$10 million" as ten million |
| `patch_detectors_vi.py`, `patch_es.py`, `patch_ca.py`, `patch_de.py`, `patch_co.py`, `patch_sv.py`, `patch_pt.py`, `patch_ru.py`, `patch_r18.py`, `patch_xk.py`, `patch_mo.py`, `patch_lu.py`, `patch_li.py`, `patch_mx.py`, `patch_mn.py`, `patch_mt.py`, `patch_np.py`, `patch_dv.py`, `patch_az.py`, `patch_ar.py`, `patch_nb.py`, `patch_mk.py`, `patch_pa.py` | The same for other languages and jurisdictions (found by other runs); they change nothing in this repository's English text, but `apply_patches.py` and `redo.py` run them on every repository |
| `patch_en_ph.py` | Written for this run (below): an amending Act's section that deletes a section of the Act it amends, and a heading that names a kind of repeal |
| `apply_patches.py` | Runs the patches above once each, in a fixed order (`patch_en_ph.py` last), and records them in the scripts folder (`.kit_patches.json`) |
| `map_moved.py` | For a repository that moved its act folders (`data/paths.json`), rewrites the paths in the history table to each act's folder since the move; this repository moved every act on 10 November 2026 (from `labor-code/` to `pd/1974/442/`), and it rewrote 487,686 paths of 18,393 folders |
| `redo.py` | Runs the patches, then again only the scans and detectors the fixes change, the model review of lapsed time limits, references to deleted provisions and empty periods, and the build (`python -X utf8 redo.py <run folder> [--keep-reviews] [--full]`; `--keep-reviews` keeps every review already made and reviews only new strong flags; `--full` runs every step again through `run.sh`, sends every category to the model and keeps every review already made; `EMBED_FONTS` names the script that embeds the chart's fonts); not needed here, as the steps were re-run by hand after the fix |

The model review needs `LLM_BASE_URL`, `LLM_API_KEY`, `LLM_MODEL` and `LLM_AUTH` set for an OpenAI-compatible Responses API.
It was run as `bash run_triage.sh '^(data|tools|vulnerabilities)/'` (every flag is in a law's own folder; the root files,
`data/` and `tools/` have none). Every lapsed time limit is in a law text, so the 40 strongest were reviewed twice, once
per step of `run_triage.sh`; the second review is the one kept.

Changes made for this repository:

- `add_root.py`: the 1987 Constitution's commit carries `Kind: referendum` (it is dated by its ratification, 2 February
  1987); `referendum` was added to the kinds that count as law, so the history table holds 18,393 commits: 15,260
  `Kind: law` (Republic Acts, Acts, Batas Pambansa, Commonwealth Acts), 3,132 `Kind: decree` (Executive Orders and
  Presidential Decrees) and the Constitution. The two `Kind: documentation` commits (the move of every act to its
  `<kind>/<year>/<number>/` folder, and the change to `tools/on.py` that reads those folders) are left out, and the 22 commits that change only the README,
  `data/` or `tools/` carry no `In-force` date and are not in the table.
- `patch_en_ph.py` (the copy of global-law's scripts), `detectors/placeholder_ref.py` `is_placeholder()`, which
  `detectors/dead_fine.py` also uses:
  - an amending Act's own section that deletes a section of the Act it amends ("SEC. 10. Section 15 of Republic Act No.
    9160 is hereby deleted.", Republic Act No. 9194; "SEC. 24. Sections 10, 11 and 12 of the same Act are hereby
    deleted.", Republic Act No. 10846) was taken for a placeholder of a deleted section, so 13 references in the same
    amending Acts, to sections of the Act they amend or of a third Act with the same numbers ("Section 10 of the same
    Act is hereby amended to read as follows: "SEC. 10. Freezing of Monetary Instrument or Property. ..."), were read as
    references to a repealed placeholder; a text that says a section "is hereby deleted" or "are hereby deleted" is now,
    like one that says it "is hereby repealed" (`patch_en.py`), the deleting provision, not a placeholder (`PH_DELETED`);
  - "Section 22. Revival of Law Impliedly Repealed. - When a law which impliedly repeals a prior law is itself repealed,
    ..." (Executive Order No. 292, the Administrative Code of 1987) was taken for a placeholder because "Repealed" opens
    its text, so "Section 22 (1), article VII of the Constitution", in a file of the same Code, was read as a reference
    to it and as a dead fine; a marker word after an adverb ("impliedly repealed") and followed by more than 60
    characters of text now names a kind of repeal, not the provision's own (`PH_ADVERB`).

Together, references to repealed placeholders went from 14 to 0 and dead fines from 1 to 0. Each change carries the
marker named above and is skipped where the marker is already there; a second run changes nothing.

`config.json` counts as not law `data/`, `tools/`, `vulnerabilities/`, the root files (`README.md`, `REPRODUCE.md`,
`LICENSE`, `jurisdiction.json`) and, through `not_law_files`, each act's `README.md`.

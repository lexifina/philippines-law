# How this repository was made (Philippines)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
|  | <https://www.officialgazette.gov.ph> | 2026-10-28 | Public domain ("All content is in the public domain unless otherwise stated"; RA 8293 s. 176) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | Internet Archive terms of use |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | The Constitution of the Republic of the Philippines (1987) | 1 | 1987-02-02 to 1987-02-02 |
| `data-privacy-act` | Data Privacy Act of 2012 (Republic Act No. 10173) | 1 | 2012-09-08 to 2012-09-08 |

The build made 2 commits:

| Commits | Kind |
| ---: | --- |
| 2 | first version of an act |
| 0 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-30.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 2 laws in the record.
- 4 tags.

## Dates

Each commit is dated at noon (Asia/Manila) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Executive Order No. 200 (1987), s. 1, amending Civil Code art. 2: "Laws shall take effect after fifteen days following the completion of their publication either in the Official Gazette or in a newspaper of general circulation in the Philippines, unless it is otherwise provided." https://www.officialgazette.gov.ph/1987/06/18/executive-order-no-200-s-1987/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `a45dc039b4a7ad3f4fbab74e8e180d7f8f3cfbf74e55459d61fa2d21f2e54cba` (240868 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3e59cb6f05eccb94a9ec14431a7f6781221e83ef`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

Not yet run for this build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- The Official Gazette is the source of every text.
- The 1987 Constitution has never been amended, so it has one version, in force 2 February 1987, the day of the plebiscite (Art. XVIII, s. 27; De Leon v. Esguerra, G.R. No. 78059, 31 August 1987).
- Constitution: the Gazette page prints Article headings and subheadings as centered lines. Article headings become each file's first line; Article IX's part letters (A to D) are kept in the keys and labels because its sections restart in each part; the other 16 subheadings (for example "Principles", "State Policies") are left out of the files.
- Constitution: the closing "Ratified: February 2, 1987" line, the table of contents and the page's "Source: CDAsia" line are not provision text and are left out.
- Data Privacy Act: Republic Act No. 10173 was approved on 15 August 2012; s. 45 makes it take effect "fifteen (15) days after its publication in at least two (2) national newspapers of general circulation". It was published on 24 August 2012, so it took effect on 8 September 2012. The publication day is from secondary reporting (Bloomberg Law), as no official page found gives it.
- Data Privacy Act: no amending Act was found on the Official Gazette; it has one version. Section 44 amends s. 7 of RA 9372, which is outside this repository.
- Data Privacy Act: the title block, enacting clause, chapter headings (17 centered lines) and the signature blocks after s. 45 are left out of the files.
- Typesetting is normalised once: no-break spaces become spaces, runs of white space collapse, and curly quotes become straight quotes. Italics and bold are dropped. Dashes are kept as printed.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote Lexifina's code and chose the sources. No model wrote or edited legal text: every word is parsed by code from the Official Gazette pages.

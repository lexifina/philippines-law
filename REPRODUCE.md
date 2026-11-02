# How this repository was made (Philippines)

This file is written by the build on 2026-11-02, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
|  | <https://www.officialgazette.gov.ph> | 2026-10-28 | Public domain ("All content is in the public domain unless otherwise stated"; RA 8293 s. 176) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | Internet Archive terms of use |
| Supreme Court E-Library, The Bookshelf (elibrary.judiciary.gov.ph) | <https://elibrary.judiciary.gov.ph/thebookshelf/2> | 2026-11-02 | Works of the Government of the Philippines: no copyright subsists (Republic Act No. 8293, s. 176) |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | The Constitution of the Republic of the Philippines (1987) | 1 | 1987-02-02 to 1987-02-02 |
| `data-privacy-act` | Data Privacy Act of 2012 (Republic Act No. 10173) | 1 | 2012-09-08 to 2012-09-08 |
| `revised-penal-code` | The Revised Penal Code (Act No. 3815) | 1 | 1932-01-01 to 1932-01-01 |
| `labor-code` | The Labor Code of the Philippines (Presidential Decree No. 442) | 1 | 1974-11-01 to 1974-11-01 |
| `revised-corporation-code` | The Revised Corporation Code of the Philippines (Republic Act No. 11232) | 1 | 2019-02-23 to 2019-02-23 |

The build made 5 commits:

| Commits | Kind |
| ---: | --- |
| 5 | first version of an act |
| 0 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-11-02.
- 1 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 5 laws in the record.
- 10 tags.

## Dates

Each commit is dated at noon (Asia/Manila) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Executive Order No. 200 (1987), s. 1, amending Civil Code art. 2: "Laws shall take effect after fifteen days following the completion of their publication either in the Official Gazette or in a newspaper of general circulation in the Philippines, unless it is otherwise provided." https://www.officialgazette.gov.ph/1987/06/18/executive-order-no-200-s-1987/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `42b7cb852d3779399f29c3e3b8582c69bc3521f0732f8ae2e2f38092cfb017b6` (978648 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
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
- Statutes after the Constitution come from the Supreme Court E-Library's public bookshelf. Each act has one version: its text as made, as the E-Library prints it. Later amendments are not applied to it.
- Each act is dated by the day it took effect, worked out by code from its own effectivity clause: "upon approval" gives the approval day; "N days after publication" gives the publication day cited on the E-Library page (the Official Gazette or the newspapers, as the clause requires) plus N days; a stated date, or a period after approval, gives that day. An act whose day cannot be worked out this way is left out.
- For acts approved on or after 29 December 1986 that say they take effect "upon approval", the day is the first publication cited, as Tañada v. Tuvera (G.R. No. L-63915, 29 December 1986) holds that publication is indispensable; such an act with no publication cited is left out.
- Pages that carry editorial amendment notes ("As amended by ...") are consolidations, not acts as made, and are left out.
- The Civil Code (Republic Act No. 386) is held: the E-Library page prints Art. 2 in the wording of Executive Order No. 200 (1987) and the rest as enacted in 1949, so it is neither the Code as made nor its text on any one day. The Family Code (Executive Order No. 209) is held: the E-Library page is a consolidation (Executive Order No. 227 and Republic Act No. 8533 applied).
- Revised Penal Code: in force 1 January 1932 under its Art. 1. Compared word by word with the Official Gazette's page of Act No. 3815: about 97% of words agree; the rest are headings, "Art."/"Article" labels and typing slips in one copy or the other (for example E-Library "irresponsbile", Gazette "reclusi n"). The E-Library text is kept as printed.
- Labor Code: in force 1 November 1974, six months after its promulgation on 1 May 1974 (Art. 2). The text is the Decree as promulgated; decrees that amended it on or before that day (for example Presidential Decree No. 570-A) are not applied. The Official Gazette's page is a consolidation, so it is not a witness for this text.
- Revised Corporation Code: s. 188 makes it take effect upon completion of its publication in the Official Gazette or in at least two newspapers; the E-Library cites the Manila Bulletin of 23 February 2019, the day it took effect.
- Text: one paragraph per line; chapter, title and book headings, the signature blocks and footnotes are left out; the item numbers of numbered lists, which the page leaves to the browser, are written out; no-break spaces and curly quotes are normalised.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote Lexifina's code and chose the sources. No model wrote or edited legal text: every word is parsed by code from the Official Gazette pages.
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote Lexifina's code and chose the sources and the dating rules. No model wrote or edited legal text or dates: every word and every day is parsed by code from the E-Library pages.

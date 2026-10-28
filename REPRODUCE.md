# How this repository was made (Philippines)

This file is written by the build on 2026-10-28, the day the source data was retrieved. Everything below is enough to rebuild this repository hash for hash.

## Sources

| Source | Address | Retrieved | Requests | Licence |
| --- | --- | --- | ---: | --- |
| Official Gazette of the Republic of the Philippines (officialgazette.gov.ph), read through Internet Archive id_ captures | <https://www.officialgazette.gov.ph> | 2026-10-28 | 4 | Public domain ("All content is in the public domain unless otherwise stated"; RA 8293 s. 176) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | None | Internet Archive terms of use |

Every response is cached by the sha256 of its URL, and the table above lists every source with its retrieval date. Lexifina keeps its fetch scripts privately; `tools/parse.py` reads only the cache and writes `corpus.json`, so the same cache always gives the same corpus.

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
- 0 commits on the branch `future`: laws not yet in force on 2026-10-28.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 2 laws in the record.
- 4 tags.

## Dates

Each commit is dated at noon (Asia/Manila) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Executive Order No. 200 (1987), s. 1, amending Civil Code art. 2: "Laws shall take effect after fifteen days following the completion of their publication either in the Official Gazette or in a newspaper of general circulation in the Philippines, unless it is otherwise provided." https://www.officialgazette.gov.ph/1987/06/18/executive-order-no-200-s-1987/

## Commands, in order

```sh
# fill the cache from the sources listed above (network; Lexifina's fetch scripts are kept privately)
python -X utf8 tools/parse.py                  # cache -> corpus.json (no network)
python -X utf8 tools/build.py <folder> --repo <empty folder> --docs-date 2026-10-28
python -X utf8 tools/check_repo.py <repo> --corpus <folder>/corpus.json --write
python -X utf8 tools/build.py <folder> --repo <another empty folder> --docs-date 2026-10-28 --compare <repo>
```

In the main Lexifina repository these files live as follows:
- `fetch.py`, `parse.py` and `repo/`: in `scripts/philippines-law/`.
- `build.py`, `check_repo.py` (`check.py` there) and `on.py`: in `scripts/gitlaw_common/`, with the corpus format in `SCHEMA.md`.

## Exact inputs

- `corpus.json` sha256 `65274bafe5d710e7ad28fccba0bc03b440f60e8d335b598b2ea426e4ca0470b0` (240627 bytes)
- Script blob hashes (`git hash-object`):

| Script | Blob |
| --- | --- |
| build.py | `2bfc4ac9df193a7be844556d7f69cdb9d93ec3f2` |
| check.py | `cd346c7ff9996d450240e3bab52bcae03b2bc865` |
| on.py | `644a6c0857fbcc72562032b58d57aa113fee0641` |
| fetch.py | `397e7bb9243eef2c4298e1c80e4a39f0b229f350` |
| parse.py | `d85961cb337727a6b1a55f6a2702b64295b457ad` |

- Tools:
  - Python 3.14.0
  - git version 2.52.0.windows.1
  - curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP

## Checks

2 versions of 2 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

Not yet run for this build.

These results are from the check run on the build before this one, from the same corpus.

## Decisions made by hand

- The 1987 Constitution has never been amended, so it has one version, in force 2 February 1987, the day of the plebiscite (Art. XVIII, s. 27; De Leon v. Esguerra, G.R. No. 78059, 31 August 1987).
- Constitution: the Gazette page prints Article headings and subheadings as centered lines. Article headings become each file's first line; Article IX's part letters (A to D) are kept in the keys and labels because its sections restart in each part; the other 16 subheadings (for example "Principles", "State Policies") are left out of the files.
- Constitution: the closing "Ratified: February 2, 1987" line, the table of contents and the page's "Source: CDAsia" line are not provision text and are left out.
- Data Privacy Act: Republic Act No. 10173 was approved on 15 August 2012; s. 45 makes it take effect "fifteen (15) days after its publication in at least two (2) national newspapers of general circulation". It was published on 24 August 2012, so it took effect on 8 September 2012. The publication day is from secondary reporting (Bloomberg Law), as no official page found gives it.
- Data Privacy Act: no amending Act was found on the Official Gazette; it has one version. Section 44 amends s. 7 of RA 9372, which is outside this repository.
- Data Privacy Act: the title block, enacting clause, chapter headings (17 centered lines) and the signature blocks after s. 45 are left out of the files.
- Typesetting is normalised once: no-break spaces become spaces, runs of white space collapse, and curly quotes become straight quotes. Italics and bold are dropped. Dashes are kept as printed.

## What AI did and did not do

The fetch, parse and check scripts were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above, through code that anyone can rerun.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote fetch.py and parse.py and chose the sources. No model wrote or edited legal text: every word is parsed by code from the Official Gazette pages.

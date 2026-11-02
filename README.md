# Philippines: law history in git

The law of the Philippines as a git repository: one file per provision, one commit per law on the day it took effect, and the law that made the text as the commit's author. It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law), which places it at `ph/`.

**What is in it now**

| Folder | Act | Versions | History |
| --- | --- | ---: | --- |
| `constitution/` | The 1987 Constitution of the Republic of the Philippines | 1 | As ratified, in force 2 February 1987 |
| `revised-penal-code/` | Act No. 3815, the Revised Penal Code | 1 | As enacted, in force 1 January 1932 |
| `labor-code/` | Presidential Decree No. 442, the Labor Code | 1 | As promulgated, in force 1 November 1974 |
| `revised-corporation-code/` | Republic Act No. 11232, the Revised Corporation Code | 1 | As enacted, in force 23 February 2019 |
| `data-privacy-act/` | Republic Act No. 10173, the Data Privacy Act of 2012 | 1 | As enacted, in force 8 September 2012 |
| `ra-*`, `pd-*`, `bp-*`, `ca-*`, `act-*`, `eo-*` | Other Republic Acts, Presidential Decrees, Batas Pambansa, Commonwealth Acts, Acts and Executive Orders | 1 each | As made, each on the day it took effect |

`data/laws.csv` lists every law in the repository.

**What it does not show.** Each act is its text as made. Later amendments are not applied to the act they amend: an amending act appears as its own folder, but the amended act's files keep their original wording. The publishers print laws as enacted and publish no dated consolidations, so there is no official text to check a rebuilt one against. The Civil Code and the Family Code are not included yet, because the only full texts found online mix the original wording with some later amendments. An act is left out when the day it took effect cannot be worked out from its own text and the publication it cites.

**Sources.** The Constitution and the Data Privacy Act come from the Official Gazette of the Republic of the Philippines, read through Internet Archive copies of its pages. Every other act comes from the Supreme Court E-Library. Chapter and article headings, signature blocks and footnotes are left out of the units. The texts keep the publishers' wording, including their typing errors. The one exception is five evident transcription errors on the Gazette's Constitution page (Art. VIII s. 11, Art. IX-A s. 2, Art. X s. 11, Art. XIII ss. 7 and 9), which were corrected where another publisher's copy and the sense of the sentence agree. The Revised Penal Code was compared word by word with the Official Gazette's copy: about 97% of the words agree, and most of the rest are headings, article labels and typing errors in one copy or the other.

## Dates

Each commit is dated at noon, Asia/Manila, on the day the law took effect, worked out from the law's own effectivity clause:

- "upon approval" means the day it was approved;
- "fifteen days after publication" means fifteen days after the publication the E-Library cites (in the Official Gazette or in newspapers, whichever the clause names);
- a stated date, or a period after approval, means that day.

From 29 December 1986, a law that takes effect "upon approval" is dated by its first publication, because the Supreme Court held in Tañada v. Tuvera that publication cannot be dispensed with.

The Constitution is dated by its ratification, 2 February 1987.

## What "author" means

The author of a commit is the law that made the change, with an e-mail address that cannot exist. The committer is Lexifina.

This is a research aid, not an official version and not legal advice. For anything that matters, read the original.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

See [REPRODUCE.md](REPRODUCE.md).

# Philippines: law history in git

The law of the Philippines as a git repository: one file per provision, one commit per law on the day it took effect, and the law that made the text as the commit's author. It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law), which places it at `ph/`.

**What is in it now**

| Folder | Act | Versions | History |
| --- | --- | ---: | --- |
| `constitution/` | The 1987 Constitution of the Republic of the Philippines | 1 | As ratified, in force 2 February 1987 |
| `data-privacy-act/` | Republic Act No. 10173, the Data Privacy Act of 2012 | 1 | As enacted, in force 8 September 2012 |

**What it does not show.** The Official Gazette prints each law as enacted and publishes no consolidated or dated text, so there is one version of each. The Revised Penal Code and other core statutes are not built, because no official consolidation exists to check a rebuilt text against.

**Source.** The Official Gazette of the Republic of the Philippines, read through Internet Archive copies of its pages. Chapter and article headings are left out of the units. Five evident transcription errors on the Gazette's Constitution page (Art. VIII s. 11, Art. IX-A s. 2, Art. X s. 11, Art. XIII ss. 7 and 9) were corrected where another publisher's copy and the sense of the sentence agree. About 35 other wording differences between the two copies, mostly typing errors in the other copy, keep the Gazette's wording.

## Dates

Each commit is dated at noon, Asia/Manila, on the day the law took effect. The Constitution is dated by its ratification, 2 February 1987. Republic Act No. 10173 was approved on 15 August 2012 and published on 24 August 2012; under Executive Order No. 200 (1987) it took effect fifteen days after publication, on 8 September 2012.

## What "author" means

The author of a commit is the law that made the change, with an e-mail address that cannot exist. The committer is Lexifina.

This is a research aid, not an official version and not legal advice. For anything that matters, read the original.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

See [REPRODUCE.md](REPRODUCE.md).

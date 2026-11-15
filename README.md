# Philippines: law history in git


The law of the Philippines as a git history: one file per article or section, one commit per law on the day it took effect, and the law as the commit's author. `git blame` names the law behind every line; `git log` lists every change to a provision; picking a date gives the text the record holds for that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the Philippines' national law, which global-law reads at `philippines/national/acts/`.

**What is in it now:** the 1987 Constitution and 18,392 laws, each as made, in one version, from Act No. 1 (in force 12 September 1900) to Republic Act No. 12322 (21 August 2026): 10,627 Republic Acts, 3,132 Acts of the Philippine Commission and Legislature, 1,641 Executive Orders, 1,491 Presidential Decrees, 865 Batas Pambansa and 636 Commonwealth Acts. [`data/laws.csv`](data/laws.csv) lists every law with the days it was enacted, published and took effect.

Most acts are in `<kind>/<year>/<number>/`, one file per provision (`pd/1974/442/art-001.md` is Article 1 of the Labor Code, Presidential Decree No. 442); the Constitution is in [`constitution/constitution/`](constitution/constitution/). [`data/paths.json`](data/paths.json) gives every act's folder; before 10 November 2026 each folder was named by the act's id (`labor-code/`), and `git log --follow`, `git blame` and `tools/on.py` read both names.

The text is in English, as the Supreme Court E-Library and the Official Gazette print it, their typing errors included; chapter and article headings, signature blocks and footnotes are left out.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every change to Article 1 of the Labor Code | `git log --follow -p --word-diff -- pd/1974/442/art-001.md` |
| Which law wrote each line of Article 1? | `git blame pd/1974/442/art-001.md` |
| Every version of the Labor Code, with the day each took effect | `git log --no-walk --tags='labor-code/*' --format="%h %(trailers:key=In-force,valueonly,separator=) %an"` |
| Article 1 in the record on 1 January 2000 | `python tools/on.py 2000-01-01 pd/1974/442 1` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about Philippine law](https://global-law.lexifina.com/v1/try_claude?country=philippines)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=philippines)**: the same question in ChatGPT.
- **[Call the API in your browser](https://global-law.lexifina.com/v1/search_law?query=service+incentive+leave&jurisdictions=philippines)**: a search of Philippine law for "service incentive leave", returned as JSON. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in English.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add philippines/national/acts
python3 tools/law.py show 2026-01-01 philippines/national/acts/pd/1974/442/art-001.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, Asia/Manila, on the day the law took effect, and carries it in its `In-force:` trailer, beside the days it was enacted and published where the source gives them. The day is worked out from the law's own effectivity clause:

- "upon approval": the day it was approved; for a law approved from 29 December 1986, the day of its first publication, as the Supreme Court held in Tañada v. Tuvera that publication cannot be dispensed with;
- "fifteen days after publication", or another period: counted from the publication the E-Library cites, in the Official Gazette or in newspapers as the clause requires;
- a stated date, or a period after approval: that day. The Constitution is dated by its ratification, 2 February 1987;
- git cannot store dates before 1970, so the 9,728 laws in force earlier are dated from 1970-01-01, one second apart, with the real day in `In-force:`. Ask for a date with `tools/on.py`, not `git log --before`.

Each law's commit is credited to the law itself (`Presidential Decree No. 442`), with an e-mail address that cannot exist; the committer is Lexifina. An amending law is its own act, so no commit is credited to a later law.

## How it is checked

- `tools/check_repo.py` reads every law back from git on the day it took effect, and on the day before, and compares it with the corpus it was built from; every commit's trailers must parse. [`REPRODUCE.md`](REPRODUCE.md) does not yet record a run.
- `tools/build.py` writes the history from one corpus file (its sha256 is in `data/corpus.sha256`), and the same corpus gives the same commit hashes; no second build has been compared yet.
- The Revised Penal Code was compared word by word with the Official Gazette's copy: about 97% of the words agree, and most of the rest are headings, article labels and typing errors. Five evident transcription errors on the Gazette's page of the Constitution were corrected where another publisher's copy and the sense agree.
- History is append-only (`tools/append.py`): new laws go on top, tags are never moved, and no published commit is rewritten.

## What it does not show

- **Amendments.** Each law is its text as made. An amending law is its own folder; the act it amends keeps its original wording, so a file is not the text in force today. The publishers print laws as made and publish no dated consolidations.
- **Repeals.** A repealed law stays in the record as made; nothing marks it repealed.
- **The Civil Code and the Family Code**, and any page that prints editorial amendment notes ("As amended by ..."): the texts found mix the original wording with later amendments.
- **Laws whose day cannot be worked out** from their own text and the publication cited.
- **Implementing rules, local ordinances and case law.**

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| [Supreme Court E-Library](https://elibrary.judiciary.gov.ph/thebookshelf/2), The Bookshelf | Laws as made: Acts, Commonwealth Acts, Republic Acts, Presidential Decrees, Batas Pambansa, Executive Orders | no, one text per law | Every law but two; the publication each page cites dates the law. The official printed copy prevails over the E-Library's text |
| [Official Gazette](https://www.officialgazette.gov.ph) | The 1987 Constitution and the Data Privacy Act of 2012 | no | Read through [Internet Archive](https://web.archive.org/) copies of its pages |

## Licence

See [`LICENSE`](LICENSE). No copyright subsists in any work of the Government of the Philippines, and statutes may be used for any purpose without prior approval (Republic Act No. 8293, s. 176.1); the Official Gazette states that its content is in the public domain. Lexifina's arrangement, commit messages, tables and tools are CC0 1.0.

No model wrote, translated or corrected legal text, and no model runs at build time; the scripts that read the sources and build this repository were written by an AI model (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published

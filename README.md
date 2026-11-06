# Vilhena (city): law history in git

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the law of Vilhena, Rondônia, Brazil, which global-law reads at `brazil/rondonia/vilhena/acts/`.

The municipal law of the Município de Vilhena, Rondônia (Brazil) as a git history: one file per Artigo, one paragraph per line, so `git blame`, `git log` and `git diff` work line by line. The text is Portuguese, the only official language.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

## What this repository holds

| Folder | Act | Versions |
| --- | --- | ---: |
| `lei-*/`, `lc-*/` | Municipal laws (Leis and Leis Complementares), newest first | one each, as enacted (177) |

**Municipal laws, newest first.** Each law the Câmara's SAPL lists with a PDF that has a text layer of its own, as enacted, credited to itself. Laws are added in parts, working back in time; later amendments by other laws are not worked into earlier laws. Scans and laws that take effect on another day than their publication are left out.

State law is in [brazil-rondonia-law](https://github.com/lexifina/brazil-rondonia-law); federal law is in [brazil-law](https://github.com/lexifina/brazil-law).

## Source

[Câmara Municipal de Vilhena, SAPL](https://sapl.vilhena.ro.leg.br/norma/pesquisar), published by the Câmara Municipal de Vilhena. Each version names the page it was taken from and that page's sha256, in `data/versions.json`.

## Dates

Each law is dated by the publication date SAPL records for it (else by its own date), and only laws whose own vigência clause says they take effect on their publication (or signature) are taken in (Decreto-Lei 4.657/1942, art. 1, would otherwise give 45 days). Commits are at noon in Vilhena.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

Each law's PDF is read from its heading to the closing line that ends in its date (signatures after it are left out); lines repeated at the top or bottom of two or more pages and page numbers are left out; lines are joined into paragraphs, one file per Art.

## How it is checked

Every version is read back from git on the day it took effect (`tools/check_repo.py`) and must match the corpus; an independent letters-and-digits comparison of every version against the source page must show no difference. Results are in `REPRODUCE.md`.

## What "author" means

The author of each commit is the law that made the text, or, for a consolidated text, the publisher, with an e-mail address that cannot exist; the committer is always Lexifina.

## Limits

The record is SAPL's: a version is only as exact as the Câmara's text for it. Only the newest laws are in so far; older ones follow in later parts. The text is not the official version: only the Diário Oficial do Município is authoritative.

## Licence

See [LICENSE](LICENSE): Brazilian law texts are not protected by copyright (Lei 9.610/1998, art. 8, IV). Fonte: Câmara Municipal de Vilhena, SAPL, Câmara Municipal de Vilhena.

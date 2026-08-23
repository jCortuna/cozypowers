# NOTICE — third-party attribution

The `designing-interfaces` skill is derived from **UI/UX Pro Max**.

- **Source:** https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- **Upstream commit:** `bc826e2267a36d98a2dcf5231e16c30ff546770f`
- **Upstream licence:** MIT © 2024 Next Level Builder (full text below)
- **This plugin's licence:** MIT — compatible; see the repository `LICENSE`.

## What was copied, and what was rewritten

| File(s) | Relationship to upstream |
|---|---|
| `data/*.csv`, `data/stacks/*.csv` | **Copied verbatim.** 34 files, 2,374 rows. The single exception is `data/stacks/nextjs.csv`, where one embedded newline inside a `'use cache'` code sample was escaped to `\n` so that every row occupies exactly one line and is retrievable by a line-based search. No row was added, removed, or otherwise altered. |
| `data/catalog-summary.json`, `data/data-provenance.json` | **Copied verbatim.** Inert metadata describing the corpus and its sources. |
| `references/quick-reference.md`, `references/pro-rules.md` | **Copied, lightly adapted.** Four lines that referenced the upstream `search.py` command-line flags were reworded to point at the corresponding CSV files. All rules are unchanged. |
| `SKILL.md` | **Rewritten.** The priority table, the query discipline and the no-match honesty rule are carried over faithfully; the procedure is rewritten for retrieval without a search engine, in this plugin's voice. |
| `references/searching-the-corpus.md` | **New.** Written for this port; it is the zero-code replacement for the upstream search engine. |

## What was deliberately left behind

**The upstream `scripts/` directory** — `search.py`, `core.py`, `design_system.py`,
`reasoning_contract.py`, `validate_data.py` (4,021 lines of Python implementing a
BM25 search engine over these CSVs).

This omission is **a matter of this plugin's principles, not a judgement about
that code**. The upstream scripts were read and audited before being excluded, and
they are clean: Python standard library only, no `subprocess` or `os.system`, no
`eval`/`exec`, no `pickle`, no network calls, and a single opt-in write path
(`--persist`) that explicitly defends against path traversal (`safe_slug()`) and
against clobbering existing files (atomic `os.link()` publish). Nothing harmful
was found.

They are excluded because cozypowers ships **zero executable code** — that is the
whole point of the plugin, and it applies to good code as much as to bad. The
functionality is preserved as a written procedure instead: Claude searches the
corpus with its own built-in tools. Anyone who would rather have the ranked search
engine should install the excellent original, linked above.

**The three bulk upstream catalogues** were also left out, for size rather than
principle: `google-fonts.csv` (1,934 rows), `phosphor-icons-upstream.json`, and
`google-font-licenses.json` — together about 2 MB, none of which carries design
reasoning. The 74 curated font pairings in `data/typography.csv` and the 105
curated icons in `data/icons.csv` are retained in full.

---

## Upstream licence

MIT License

Copyright (c) 2024 Next Level Builder

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

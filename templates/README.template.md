# Marketing handbook

{{header_line}}

One founder's handbook for running marketing with AI agents: connecting Google Ads and Meta to Claude, the analyses I actually run, what to pull out of Search Console, cold-email lessons, and the skills behind it. It is not a directory of everything that exists - if something is here, it earned its place in real work. The longer notes live in [FIELD-NOTES.md](FIELD-NOTES.md). Suggest a link by opening an issue (see [CONTRIBUTING.md](CONTRIBUTING.md)).

Descriptions are my own notes where I wrote one. Where I only saved a link, the description comes from the page, post or repository itself. Ratings like `(Matt: 8/10)` are my personal scores.

## Contents

{{toc}}

{{start_here}}

{{sections}}

## How this list is built

The source is a private Notion page where I keep notes while I work. A sync script in my workspace (`awesome-sync.py`, not in this repo) reads that page through the Notion API and keeps only the sections that are explicitly mapped as public - everything else stays private by default. Three toggles of third-party lesson material are mapped links-only, so their links appear and none of their prose does. The script canonicalizes every URL, drops links to private places, scans every string for secrets and private names, and writes `data/links.csv`, `data/notes.json` and `data/_report.md`.

From there everything is reproducible from this repo alone: `tools/enrich.py` checks every link and records stars, licence, last push and HTTP status; `tools/build.py` renders this README and `FIELD-NOTES.md` deterministically; `tools/lint.py` fails on dead links, thin descriptions, duplicates, tracking parameters and broken anchors. A weekly GitHub Action re-runs the checks and opens a pull request when either file changes.

Nothing here is edited by hand. Fixes go to `data/overrides.json` and the next build picks them up.

{{stats}}

## License

The content of this list is licensed under [CC BY 4.0](LICENSE) - share and adapt it with attribution. The scripts in `tools/` are MIT licensed ([LICENSE-CODE](LICENSE-CODE)).

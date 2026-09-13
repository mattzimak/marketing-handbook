# Marketing handbook

27 entries · last verified 2026-09-11 · 27 links checked · 0 dead

One founder's handbook for running marketing with AI agents: connecting Google Ads and Meta to Claude, the analyses I actually run, what to pull out of Search Console, cold-email lessons, and the skills and prompts behind it. It is not a directory of everything that exists - if something is here, it earned its place in real work. The longer notes live in [FIELD-NOTES.md](FIELD-NOTES.md). Suggest a link by opening an issue (see [CONTRIBUTING.md](CONTRIBUTING.md)).

Descriptions are my own notes where I wrote one. Where I only saved a link, the description comes from the page, post or repository itself. Ratings like `(Matt: 8/10)` are my personal scores.

## Contents

- [Google Ads](#google-ads)
  - [Connecting an account](#connecting-an-account)
- [Meta Ads](#meta-ads)
  - [Connectors](#connectors)
- [SEO](#seo)
- [Cold email](#cold-email)
- [Ads](#ads)
  - [Pipelines](#pipelines)
- [Skills for marketers](#skills-for-marketers)
- [Distribution](#distribution)
- [Strategy](#strategy)
- [Prompts](#prompts)
- [Learning](#learning)
- [How this list is built](#how-this-list-is-built)
- [License](#license)

## Google Ads

Connecting an account to Claude, and the analyses I actually run against it.

- [Connect Claude to Google Ads Step by Step + Prompt examples](https://www.get-ryze.ai/blog/connect-claude-google-ads-step-by-step) - Step-by-step guide to connecting Claude to a Google Ads account, covering the API enablement, OAuth client and refresh token in one pass.

### Connecting an account

- [add test user](https://console.cloud.google.com/auth/audience) - Audience / Test users: → add the Google account that has access to Ads account 354-835-9598.
- [console.cloud.google.com → Create credentials](https://console.cloud.google.com/apis/credentials/oauthclient) - Google Cloud console, Credentials page. Where the OAuth client ID for the Google Ads API is created.
- [console.cloud.google.com → OAuth consent screen](https://console.cloud.google.com/auth/overview) - Google Cloud console, OAuth consent screen. Configure this before creating the client ID or the token exchange fails.
- [Documentation](https://developers.google.com/google-ads/api) - Official Google Ads API documentation: the reference for building applications that read and write a Google Ads account programmatically.
- [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/cloud-project) - Google's own walkthrough for setting up the API Console project behind the Google Ads API, using the OAuth desktop flow.
- [Google Ads API Center](https://ads.google.com/aw/apicenter) - (open this while signed into the Ads account) → confirm whether your token jl5-uISP_WMAzsy_1ewk-g is Test, Basic, or Standard access. Test access can only call test accounts; you'd need to apply for Basic access to hit your live 354-835-9598 account. · also: [support.google.com](https://support.google.com/adspolicy/contact/new_token_application)
- [google-ads-python](https://github.com/googleads/google-ads-python/blob/main/examples/authentication/generate_user_credentials.py) - Google's official Python client library for the Google Ads API. The path of least resistance if you are scripting reports rather than wiring an MCP server. · 746 stars · Apache-2.0 · updated 2026-09
- [Scope](https://developers.google.com/google-ads/api/docs/oauth/internals#scope) - The OAuth scope string the Google Ads API requires. Worth keeping to hand: the wrong scope is the most common cause of a silent auth failure. · also: [googleapis.com](https://www.googleapis.com/auth/adwords)

My notes on this section: [Google Ads](FIELD-NOTES.md#google-ads) (49 notes).

## Meta Ads

Connectors, the MCP path, and what the agents can do once they are wired in.

- [Claude MCP for Meta Ads (LinkedIn)](https://www.linkedin.com/posts/aashams1992_claude-mcp-for-meta-ads-is-a-cheat-code-share-7440289941068214272-kWNh) - Short post on wiring Meta Ads into Claude over MCP and what it unlocks once the connection holds.
- [Meta Ads Library](https://www.facebook.com/ads/library?active_status=active&ad_type=all&country=CZ&is_targeted_country=false&media_type=all&sort_data%5Bmode%5D=total_impressions&sort_data%5Bdirection%5D=desc) - Meta's public ad library. The fastest way to see exactly what a competitor is running, with no account and no scraping.
- [Ten Claude Code skills that manage Meta ads](https://www.linkedin.com/posts/anantha-koppa_i-built-10-claude-code-skills-that-manage-share-7446808829050187776-Psj6) - An operator who turned the repetitive Meta Ads Manager work into ten Claude Code skills and published them, aimed at the clicking, exporting and screenshotting that eats a media buyer's day.

### Connectors

- [mcp.facebook.com/ads](https://mcp.facebook.com/ads) - MCP is a standard that lets AI agents talk to outside tools and data. Think of it like an API. If you live in the Claude or ChatGPT app, this is the one for you. Paste as a connector, sign in with Facebook, done.

My notes on this section: [Meta Ads](FIELD-NOTES.md#meta-ads) (9 notes).

## SEO

What to pull out of Search Console and what to do with it.

- [Own the reviews page for your own brand](https://www.instagram.com/reel/DYYgTGDPBrB) - Argues for buying yourbrand-reviews as a domain and publishing your reviews there, so the page an AI assistant finds when someone checks you out is one you control.

My notes on this section: [SEO](FIELD-NOTES.md#seo) (18 notes).

## Cold email

Deliverability, sequencing and the lessons that cost me something to learn.

- [Cold email deliverability walkthrough (Loom)](https://www.loom.com/share/4f2bf50235cc4cedb0b3e26584512aaf) - A practitioner's video on building a cold-email dashboard and what the first weeks taught them: secondary sending domains, many mailboxes, and a daily send ceiling.
- [Mailforge](https://mailforge.ai) - Bulk mailbox provisioning for cold email. The common reason to use it is spreading send volume across many inboxes on secondary domains instead of burning one. · also: [instantly.ai](https://instantly.ai)
- [r/coldemail](https://www.reddit.com/r/coldemail) - The subreddit where high-volume cold emailers compare deliverability, offers and sequencing. Worth reading many threads rather than trusting any single one.

## Ads

Creative, libraries and pipelines that are not platform-specific.

- [Launching 100+ Facebook ads in 30 minutes (Instagram reel)](https://www.instagram.com/reel/DWOjnYtESQn) - Shows Claude Code driving bulk Facebook ad creation, roughly a hundred ads in half an hour. The interesting part is the batching pattern, not the exact numbers.
- [Lead-gen setup walkthrough (Instagram reel)](https://www.instagram.com/reel/DV8ctOMgcJt) - Short reel walking through an n8n plus Claude skills lead-generation setup. The guide itself is gated behind a comment, so treat the reel as the index, not the instructions.

### Pipelines

- [Agentic social scheduler thread (@shannholmberg)](https://x.com/shannholmberg/status/2039636480101118430) - Thread breaking down how an operator runs an agentic social-media scheduler end to end with AI skills, including the claimed revenue behind it. Useful as a pipeline shape, sceptical on the figure.

My notes on this section: [Ads](FIELD-NOTES.md#ads) (4 notes).

## Skills for marketers

Claude skills that do real marketing work.

- [Brand Guidelines](https://github.com/anthropics/skills/tree/main/skills/brand-guidelines) - Encode your brand into a skill. Auto-applies everywhere. · 175k stars · updated 2026-09
- [Claude SEO](https://github.com/AgriciDaniel/claude-seo) - Full-site audits, schema validation. 12 sub-skills. · 16k stars · MIT · updated 2026-09
- [Marketing Skills by Corey Haines](https://github.com/coreyhaines31/marketingskills) - 20+ skills: CRO, copywriting, SEO, email sequences, growth. · 49k stars · MIT · updated 2026-09

## Distribution

Getting the thing seen: virality mechanics and posting straight from the terminal.

- [Going viral on X (@coreyganim)](https://x.com/coreyganim/status/2039699858760638747) - Video post on what actually drives reach on X. Saved for the distribution mechanics rather than for the creator's niche.

My notes on this section: [Distribution](FIELD-NOTES.md#distribution) (1 notes).

## Strategy

The thinking above the tactics.

- [Building a coaching offer that sells](https://www.instagram.com/reel/DW8TbCSDWOZ) - Breakdown of building and scaling a coaching or consulting offer without the copy-paste funnel playbook. The full roadmap is comment-gated.

## Prompts

Long prompts worth keeping.

My notes on this section: [Prompts](FIELD-NOTES.md#prompts) (271 notes).

## Learning

People and sources worth your time.

- [AI marketing masterclass, beginner to expert in 60 minutes](https://www.youtube.com/watch?v=fVUlrpaWNxg) - Greg Isenberg's hour-long overview of the current AI marketing stack. The best single starting point here if you are new to this.
- [Using AI tools to create viral IG reels](https://www.youtube.com/watch?v=0b8qQx3FaLE) - Greg Isenberg walking through a reel-production stack built on Manus, Freepik and friends. Watch it for the pipeline, not the specific tools.

## How this list is built

The source is a private Notion page where I keep notes while I work. A sync script in my workspace (`awesome-sync.py`, not in this repo) reads that page through the Notion API and keeps only the sections that are explicitly mapped as public - everything else stays private by default. Three toggles of third-party lesson material are mapped links-only, so their links appear and none of their prose does. The script canonicalizes every URL, drops links to private places, scans every string for secrets and private names, and writes `data/links.csv`, `data/notes.json` and `data/_report.md`.

From there everything is reproducible from this repo alone: `tools/enrich.py` checks every link and records stars, licence, last push and HTTP status; `tools/build.py` renders this README and `FIELD-NOTES.md` deterministically; `tools/lint.py` fails on dead links, thin descriptions, duplicates, tracking parameters and broken anchors. A weekly GitHub Action re-runs the checks and opens a pull request when either file changes.

Nothing here is edited by hand. Fixes go to `data/overrides.json` and the next build picks them up.

Current build: 27 entries in 10 sections, 352 field notes. Links checked: 27, dead: 0, last check: 2026-09-11. What the sync excluded and why is in `data/_report.md`. The field notes are rendered into `FIELD-NOTES.md` by the same build.

## License

The content of this list is licensed under [CC BY 4.0](LICENSE) - share and adapt it with attribution. The scripts in `tools/` are MIT licensed ([LICENSE-CODE](LICENSE-CODE)).

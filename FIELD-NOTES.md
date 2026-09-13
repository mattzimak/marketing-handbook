# Marketing field notes

81 notes in 5 sections · built from the same data as README.md

The long-form notes behind [README.md](README.md): setup walkthroughs, analysis recipes and prompts that are too long to sit in a link list.

## Contents

- [Google Ads](#google-ads) (49 notes)
  - [Connecting an account](#connecting-an-account)
  - [Analysis recipes](#analysis-recipes)
- [Meta Ads](#meta-ads) (9 notes)
  - [Connectors](#connectors)
- [SEO](#seo) (18 notes)
  - [Search Console audit](#search-console-audit)
- [Ads](#ads) (4 notes)
  - [Pipelines](#pipelines)
- [Distribution](#distribution) (1 notes)

## Google Ads

Links for this section are in [README.md](README.md#google-ads).

- Prompts
- Google Ads Tracking blueprint - not sure of quality/relevance

### Connecting an account

- **Step 1 - Enable the Google Ads API**
- **Step 2 - Configure the OAuth consent screen**
- App name: Marketing Manager (or anything)
- User support email: matt.zimak@gmail.com
- User Type: External
- Developer contact: matt.zimak@gmail.com
- Skip the Scopes screen
- Leave publishing status as Testing (refresh tokens last 7 days in Testing mode for sensitive scopes - fine for personal use, but if you hit expiry, click Publish app to move to Production)
- **Step 3 - Create the OAuth Client ID**
- Application type: Desktop app
- Name: anything (e.g. "agentmatik-manager")
- Click Create → Download JSON
- This gives you client_id and client_secret.
- **Step 4 - Get a refresh token**
- Once you have the client JSON, run the OAuth flow locally. Reference docs:
- **Step 5 - Check developer token access level**
- Run on terminal
  ```bash
  cd ~/marketing-manager/google-ads
  python3 -m venv .venv
  source .venv/bin/activate
  pip install -r requirements.txt
  python auth.py
  ```
- auth.py will:
- Open your browser
- Ask you to sign in - use the Gmail that has manager access on 852-402-1823
- Show a "Google hasn't verified this app" warning → click Advanced → Go to Marketing Manager (unsafe)
- Print a GOOGLE_ADS_REFRESH_TOKEN=... line in the terminal
- Paste that line into .env (replace the empty GOOGLE_ADS_REFRESH_TOKEN=).
- Then:
- python list_accounts.py
- You should see your MCC 354-835-9598 and the client account 852-402-1823. Paste the output back here and I'll help with the first real query.

### Analysis recipes

- Identifies keywords burning budget without generating conversions. Claude analyzes spend vs. conversion data across all campaigns, flags keywords with disproportionate cost-to-conversion ratios, and recommends bid reductions or negative keyword additions. This single workflow typically saves 10-15% of monthly ad spend.
- Example prompt - Find all keywords with spend > $100 and conversions &lt; 2 in the last 30 days. Calculate cost per conversion where conversions > 0. Rank by total wasted spend. Recommend bid adjustments or negative keyword additions.
- ompares effectiveness across Google’s network types to optimize budget allocation. Claude analyzes CTR, conversion rates, CPA, and ROAS for Search, Display, YouTube, and Shopping campaigns. Many accounts discover their Display campaigns have 3-5x higher CPA than Search, revealing easy optimization opportunities.
- Example prompt Compare performance across Search, Display, Shopping, and YouTube campaigns for the last 60 days. Show CTR, CPC, conversion rate, CPA, and ROAS for each network. Recommend budget reallocation based on efficiency metrics.
- Evaluates which headlines, descriptions, and extensions generate the highest engagement and conversions. Claude examines thousands of ad variations simultaneously, identifies top-performing messaging patterns, and suggests new ad copy variations based on proven elements. Ad copy testing can improve CTR by 20-40% when done systematically.
- Example prompt - Analyze all active responsive search ads. Compare CTR and conversion rates by headline position, description, and ad extensions. Identify top-performing message patterns. Generate 5 new ad variations using winning elements.
- Identifies keywords with low Quality Scores that increase cost-per-click and reduce ad visibility. Claude analyzes keyword relevance, ad relevance, landing page experience, and expected CTR components. A 1-point Quality Score improvement can reduce CPC by 7-9%, making this optimization extremely cost-effective.
- Example prompt - Find all keywords with Quality Score &lt; 6. Group by campaign and ad group. Analyze keyword relevance, ad text alignment, and landing page match. Recommend specific improvements for keyword grouping and ad copy optimization.
- Reveals how mobile, desktop, and tablet users interact differently with your ads. Claude compares conversion rates, average order values, and user behavior across devices. Many B2B campaigns convert better on desktop (2-3x higher rates), while e-commerce often sees stronger mobile performance, especially for impulse purchases.
- Example prompt - Analyze campaign performance by device type for the last 90 days. Compare mobile, desktop, and tablet metrics: CTR, conversion rate, CPA, and average order value. Recommend bid adjustments and budget allocation by device.
- Uncovers which locations drive profitable conversions versus those that drain budget. Claude analyzes cost-per-conversion by city, state, or country, identifies geographic outliers, and recommends location bid adjustments or exclusions. Regional performance often varies by 200-300% within the same country.
- Example prompt - Analyze geographic performance for the last 60 days. Show cost, conversions, and CPA by state/country. Flag locations with CPA > 50% above account average. Recommend location bid adjustments and potential exclusions.
- Determines optimal times of day and days of week for ad delivery. Claude examines hourly and daily performance patterns, identifies peak conversion windows, and suggests bid schedules. E-commerce accounts often see 40-60% higher conversion rates during evening hours (6-9 PM) compared to early morning.
- Example prompt - Analyze performance by hour of day and day of week for the last 90 days. Show conversion rate, CPA, and impression volume by time period. Recommend bid schedule adjustments to maximize conversions during peak hours.
- Finds irrelevant search terms that trigger your ads and waste budget. Claude analyzes search term reports, identifies patterns in non-converting queries, and suggests negative keyword lists. Proper negative keyword management can reduce wasted spend by 15-25% while improving ad relevance.
- Example prompt - Review search term report for the last 30 days. Find queries with impressions > 100, clicks > 5, but 0 conversions. Group similar irrelevant terms and suggest negative keyword additions at campaign and ad group levels.
- Examines auction insights data to understand competitive landscape and identify opportunities. Claude analyzes impression share, average position, and overlap rates with competitors. This data reveals when competitors are increasing bids, launching new campaigns, or pulling back from certain keywords.
- Example prompt - Pull auction insights for my top-spending campaigns over the last 60 days. Analyze impression share, position, and overlap with competitors. Identify keywords where we're losing significant impression share.
- Generates comprehensive account summaries with actionable insights for stakeholders. Claude compiles key metrics, identifies trends, highlights top performers and problem areas, and creates executive-friendly reports. Manual report creation typically takes 2-3 hours; Claude completes this in 60-90 seconds.
- Example prompt - Generate a weekly Google Ads report for April 1-7, 2026. Include executive summary, key metrics table, top 5 performing campaigns, top 3 concerns requiring attention, and 5 action items for next week. Write for CMO-level audience.

## Meta Ads

Links for this section are in [README.md](README.md#meta-ads).

- scrape ads that are running above 14-28 days = winners

### Connectors

- first official, first-party way to plug your AI agents into your Meta ad account
- **What your agents can now do**
  - Pull performance. "Show spend, ROAS, and CTR for every active campaign, sorted by CTR."
  - Auto-pause losers. "Pause anything spending more than $100/day with ROAS under 1.2."
  - Build campaigns from a brief. "Spin up a Summer Sale campaign with these 3 creatives, $50/day budget, US targeting. Leave it paused for me to review."
  - Diagnose pixel health. "Check my Conversions API setup and tell me where to invest."
  - Manage product catalogs. "Import these 50 SKUs into a new catalog."
  - Search the Meta Help Center inline. "Why was this ad disapproved?"

## SEO

Links for this section are in [README.md](README.md#seo).

### Search Console audit

- **What to export from Google Search Console**
- Performance → Search results (last 16 months, all queries):
- Queries tab → Export as CSV - top queries, clicks, impressions, CTR, position
- Pages tab → Export - top landing pages with same metrics
- Countries tab + Devices tab → Export
- Compare last 3 months vs previous 3 months → Export (catches drops)
- Indexing → Pages:
- 5. Screenshot or export the "Why pages aren't indexed" table (all reasons + counts)
- 6. List of indexed pages count vs submitted
- Indexing → Sitemaps:
- 7. Screenshot of submitted sitemaps + discovered URL counts
- Experience → Core Web Vitals:
- 8. Mobile + Desktop reports (screenshot the pass/fail counts)
- Enhancements (if present): any errors in Sitelinks, Breadcrumbs, Logos, etc.
- Links:
- 9. Top linking sites + top linked pages (export both)
- Manual actions / Security:
- 10. Screenshot - should be "No issues" but worth confirming

## Ads

Links for this section are in [README.md](README.md#ads).

- Meta Ads Agent with Openclaw
- Untitled

### Pipelines

- the skill stack he runs:
- > Postiz for scheduling and posting to social media agent-media for creating UGC pictures Larry for generating TikTok slideshows Virlo for finding trending topics on social media GStack so the marketing copy doesnt sound like AI

## Distribution

Links for this section are in [README.md](README.md#distribution).

- you can send DMs via Zernio using CC - (paid community post)

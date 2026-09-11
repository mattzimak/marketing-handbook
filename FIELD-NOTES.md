# Marketing field notes

368 notes in 7 sections · built from the same data as README.md

The long-form notes behind [README.md](README.md): setup walkthroughs, analysis recipes and prompts that are too long to sit in a link list.

## Contents

- [Google Ads](#google-ads) (49 notes)
  - [Connecting an account](#connecting-an-account)
  - [Analysis recipes](#analysis-recipes)
- [Meta Ads](#meta-ads) (9 notes)
  - [Connectors](#connectors)
- [SEO](#seo) (18 notes)
  - [Search Console audit](#search-console-audit)
- [Cold email](#cold-email) (16 notes)
- [Ads](#ads) (4 notes)
  - [Pipelines](#pipelines)
- [Distribution](#distribution) (1 notes)
- [Prompts](#prompts) (271 notes)
  - [Landing page mega-prompt](#landing-page-mega-prompt)

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

## Cold email

Links for this section are in [README.md](README.md#cold-email).

- (paid community post)
- Two weeks into cold emailing (very low volume) and the number of things I've learned has been absolutely insane. This post is going to be the TLDR; version. If you want more in depth, watch the video and / or download read the document attached.
- I built my Outreach Dashboard (working name, I use with Claude) to be part of my cold email infrastructure. It's where I can view stats like deliverability, replies, bookings, etc. The first week was mostly tweaking the workflows, database, campaign structures, and email lists. The second week was finding posts about cold mailing to help further tweak things.
- Yesterday, I sent my first 20 "real" emails. Even throughout the day I was learning stuff. Every lesson learned, Claude saved, so I could reference back to them.
- Here are some of my learnings in no particular order:
- Don't read a singular post about cold emailing and think "Oh, I'm good, I know what to do". Read dozens, or hundreds if you can. Many, many of them will reiterate the same things, which is good. That means those items are important, but occasionally, you'll find a tiny nugget in a single thread that could change things tremendously. Those nuggets are included in the .md doc, and I'll try to point them out here as well.
- 2. Mailgun is NOT the mailing software to use. Mailgun is only good for transactional emails. Cold emails (marketing emails) are against their TOS
- 3. Never use your primary domain for emailing. You need your primary domain to be clean and solid for your clients.
- 4. Text only emails. If you send HTML emails, in theory, you can get open rates in your dashboard, but the tradeoff is HTML emails will marginally hurt deliverability. Once you get to thousands of emails per day, any tiny marginal difference can be HUGE. The ONLY advantage to HTML emails is being able to see if there was an open.
- 5. Speaking of opens... they don't matter. All that matters is reply rate. I'm trying to find the thread, but I remember reading yesterday that at scale, you want to see 2 - 5%. Much lower than what I originally thought. For guys seeing over 10%, they're able to send hyper personalized emails. That requires a list I don't know how to build yet... when I figure it out, I'll let you know.
- 7. Email validation is non-negotiable. You MUST use an email validation service on all your lists, regardless of where you got the list. I personally don't trust the "we do it all" places that will build, enrich and validate. Validation is something I do with a specialized email validator like Neverbounce or Zerobounce. I have used both. I like Neverbounce better. It's cheaper, allows you to pay as you go, and doesn't give me a huge zip file full of files I don't need.
- 9. Do NOT mail to MSN accounts. Anything that is part of Microsoft's network: Hotmail, Live, MSN, etc. Microsoft is the killer of deliverability. Why? I have no idea, but I know from practical experience that my personal email gets more non-spam in the spam box than any other I've ever used. Limit your emails to Gmail and Google workspace for better deliverability.
- 10. Adding to this deliverability is King. Nothing else matters if you can't hit inboxes. The more inboxes you hit, the more eyes will see your emails, the more will open, the more will respond, but it all starts with deliverability.
- 11. Less is more. According to one golden thread in r/coldemail by a guy sending 2000+ emails per day, the third email and beyond significantly increases the spam rate. According to him, the first two are your golden ticket, after that, MAYBE a third, but it has to be something like a breakup email. Otherwise, he only emails a two email sequence.
- Okay, that's enough typing. Read the attached, watch the video, and I'll report back as I get data and solid numbers flowing in.
- Cheers!

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

## Prompts

Links for this section are in [README.md](README.md#prompts).

- Hyliox website

### Landing page mega-prompt

- https://www.hyliox.io/en/prompt?mcp_token=eyJwaWQiOjQ3NjUwNzcsInNpZCI6MTg3NjQyOTkxNywiYXgiOiI2YTFlMmJkOGE4NmNlMzc0ZTdhZWIxMjkxNGZlZmY3YiIsInRzIjoxNzc3NDU4MzE5LCJleHAiOjE3Nzk4Nzc1MTl9.qYaEXUlb3byh1GSBraG5yudazKIXelJsLjfYx8y4gSA&fbclid=PARlRTSARevLpleHRuA2FlbQIxMABzcnRjBmFwcF9pZA8xMjQwMjQ1NzQyODc0MTQAAaeDxcg3PE_J_rloPUPgMrRuWVTSxLY5qhaAGLZOCLjkYt_ob6lknwlUwy0SHw_aem_5KODiSyS4KQZHNQHgUh8mQ
- **MEGA-PROMPT TEMPLATE - One-Shot Cinematic Landing Page (Video Scroll-Scrub)**
- > Fill every {{PLACEHOLDER}} below, then paste the whole document into your generating model (Lovable, v0, Cursor, Claude, etc.) as a SINGLE prompt. Do NOT split it. The model must produce a working Vite app in one shot.
- **0. BRIEF (read first, do not skip)**
- You are building a premium, single-page marketing site in the spirit of Apple's AirPods Pro page, Stripe's landing, and Sony Bravia launch sites. The signature interaction is a scroll-scrubbed video rendered as a canvas frame sequence in the hero. The rest of the page is editorial, cinematic, liquid-glass, Google-Stitch-tier quality.
- Target stack - non-negotiable:
- Vite + React 18 + TypeScript
- Tailwind CSS v4 (with @theme directive)
- shadcn/ui (button, accordion)
- Framer Motion (motion/react) for text + element animations
- lucide-react for icons
- @fontsource/\* for self-hosted fonts
- Language of the site UI copy: {{LANG}} (e.g. fr-CH, en-US).
- Design intent (re-read before every section you build):
- Editorial, premium, cinematic. Think fashion-magazine meets SaaS.
- "Google Stitch"-tier polish: every spacing, every corner radius, every weight must feel intentional.
- No generic AI-slop: no emoji decorations, no default violet gradients, no stock-looking drop shadows, no text-center on everything, no placeholder lorem left behind.
- Mobile first but optimized for desktop narrative (1440px is the primary canvas).
- Dark theme by default. Light surfaces are ivory/cream, not pure white.
- What success looks like: npm run dev starts on first try, all 9 sections render, the hero frame-sequence scrubs smoothly with scroll, the marquees loop seamlessly, the FAQ accordion opens, no console errors, LCP &lt; 2.5s on a 10 Mbps connection.
- **1. PLACEHOLDERS LEGEND**
- Fill every entry in this table before submitting. The table is the single source of truth - every placeholder in the sections below is defined here.
- **Placeholder | Type | Example | Default**
- {{LANG}} | BCP-47 code | fr-CH | fr-CH
- {{BRAND_NAME}} | string | ABP | Atelier
- {{BRAND_TAGLINE}} | 3-6 words | Déménagement d'exception | Built for what's next
- {{LOGO_PATH}} | image path | /logo.svg | /logo.svg
- {{NAV_ITEMS}} | array of {label,href} | \[{"label":"Services","href":"#services"},...\] | 4-5 items
- {{CTA_LABEL}} | 1-3 words | Devis gratuit | Get Started
- {{CTA_HREF}} | anchor/url | #devis | #cta
- {{FRAMES_PATH}} | public path prefix | /frames | /frames
- {{FRAME_COUNT}} | integer | 240 | 240
- {{FRAME_EXT}} | jpg or webp | jpg | jpg
- {{FPS}} | integer | 30 | 30
- {{HERO_HEADLINE}} | 2-5 words | Bouger, sans bruit. | Move, quietly.
- {{HERO_SUB}} | 1-2 sentences | Du studio au penthouse. L'art du déménagement, signé {{BRAND_NAME}}. | One move. Zero friction.
- {{HERO_CTA_PRIMARY}} | 1-3 words | Devis gratuit | Start now
- {{HERO_CTA_SECONDARY}} | 1-3 words | Voir le film | Watch film
- {{PARTNERS}} | array of 5-6 strings | \["Christie's","Sotheby's","Piaget"\] | 5 brand names
- {{SERVICES}} | array of 6 {icon,title,body} | see Section 13 | 6 entries
- {{REASONS}} | array of 4 {icon,title,body} | see Section 14 | 4 entries
- {{PROCESS_STEPS}} | array of 3-4 {n,title,body} | see Section 15 | 4 entries
- {{STATS}} | array of 4 {value,label} | \[{"value":"2500+","label":"déménagements"}\] | 4 entries
- {{STATS_BG_VIDEO}} | HLS or MP4 URL | https://stream.mux.com/xxx.m3u8 | placeholder URL
- {{TESTIMONIALS}} | array of ≥6 {quote,name,role} | see Section 17 | 6 entries
- {{FAQ_ITEMS}} | array of 5-8 {q,a} | see Section 18 | 6 entries
- {{CTA_BG_VIDEO}} | HLS or MP4 URL | https://stream.mux.com/yyy.m3u8 | placeholder URL
- {{CTA_HEADLINE}} | 4-7 words | Prêts à partir? | Ready to move?
- {{CTA_SUB}} | 1 sentence | Un entretien. Un plan. Un déménagement. | One call. Done.
- {{FOOTER_LINKS}} | array of {label,href} | \[{"label":"Mentions","href":"/legal"}\] | 4 entries
- {{COPYRIGHT}} | string | © 2026 {{BRAND_NAME}} SA. Tous droits réservés. | © 2026 {{BRAND_NAME}}. All rights reserved.
- {{COLOR_INK}} | HSL triplet | 20 15% 9% | 20 15% 9%
- {{COLOR_CREAM}} | HSL triplet | 40 30% 90% | 40 30% 90%
- {{COLOR_OCHRE}} | HSL triplet | 32 55% 65% | 32 55% 65%
- {{COLOR_TERRA}} | HSL triplet | 14 55% 31% | 14 55% 31%
- {{FONT_DISPLAY}} | Google-Font family | Oswald | Oswald
- {{FONT_BODY}} | Google-Font family | Inter | Inter
- **2. PRE-STEP - VIDEO → JPG FRAME PIPELINE**
- The hero uses a scroll-scrubbed frame sequence, not a &lt;video> tag. The user supplies ONE short video (5-15s is ideal) which is extracted into still frames that the canvas swaps per scroll position. This is the pattern Apple uses on AirPods Pro / MacBook marketing pages.
- Instructions the generating model MUST include in the project README:
  ```bash
  # 1. Drop the source video at /input/source.mp4 in the project root.
  mkdir -p input public/frames

  # 2. Extract frames with ffmpeg (requires ffmpeg installed locally).
  ffmpeg -i input/source.mp4 \\
  -vf "fps={{FPS}},scale='min(1920,iw)':'-2':flags=lanczos" \\
  -q:v 3 \\
  public/frames/frame_%04d.{{FRAME_EXT}}

  # 3. Count the frames and paste the number into FRAME_COUNT in App.tsx.
  ls public/frames | wc -l

  # Optional: convert to WebP for smaller payload (~40% size drop, same visual quality).
  # for f in public/frames/*.jpg; do
  # cwebp -q 82 "$f" -o "${f%.jpg}.webp" && rm "$f"
  # done
  ```
- Rules for the model:
- Do NOT hardcode a specific frame count. Read it from the FRAME_COUNT constant at the top of App.tsx, which is a {{FRAME_COUNT}} placeholder.
- Filenames MUST be zero-padded 4-digit (frame_0001.jpg ... frame_NNNN.jpg). If the user chooses WebP, same pattern with .webp.
- /input stays gitignored. /public/frames ships.
- If the build target is a platform with a 25 MB limit (Vercel hobby), warn the user in the README if total frame size exceeds 20 MB.
- Fallback (no ffmpeg on the user's machine): document a Node script using @ffmpeg/ffmpeg (WASM) as a scripts/extract-frames.mjs that does the same extraction. Do not implement it unless the user asks; just mention its existence in the README.
- **3. PROJECT BOOTSTRAP**
- Run these commands in order. Every command is exact.
  ```bash
  npm create vite@latest. -- --template react-ts
  npm install
  npm install -D tailwindcss@next @tailwindcss/vite @tailwindcss/postcss autoprefixer
  npm install motion lucide-react
  npm install @fontsource/{{FONT_DISPLAY | lower}} @fontsource/{{FONT_BODY | lower}}

  # shadcn/ui
  npx shadcn@latest init -d
  npx shadcn@latest add button accordion
  ```
- vite.config.ts: import @tailwindcss/vite plugin and wire it. Add a @ path alias to src/.
- tsconfig.json: add "paths": { "@/\*": \["./src/\*"\] } and the matching "baseUrl": ".".
- File structure the model must create:
  ```text
  src/
  App.tsx
  main.tsx
  index.css
  components/
  ScrubSequence.tsx # the canvas frame renderer
  Navbar.tsx
  Hero.tsx
  ServicesBento.tsx
  Pourquoi.tsx
  Process.tsx
  Stats.tsx
  Testimonials.tsx
  Faq.tsx
  CtaFooter.tsx
  BlurText.tsx # reusable word-stagger animation
  ui/
  button.tsx
  accordion.tsx
  lib/
  utils.ts
  constants.ts # FRAME_COUNT, FRAMES_PATH, etc. - single source of truth
  public/
  frames/ # frame_0001.{{FRAME_EXT}} ... frame_NNNN.{{FRAME_EXT}}
  {{LOGO_PATH}}
  ```
- **4. DESIGN TOKENS (index.css)**
- Add at the top of src/index.css, ABOVE the Tailwind import:
  ```css
  @import "@fontsource/{{FONT_DISPLAY | lower}}/300.css";
  @import "@fontsource/{{FONT_DISPLAY | lower}}/400.css";
  @import "@fontsource/{{FONT_DISPLAY | lower}}/500.css";
  @import "@fontsource/{{FONT_DISPLAY | lower}}/600.css";
  @import "@fontsource/{{FONT_DISPLAY | lower}}/700.css";
  @import "@fontsource/{{FONT_BODY | lower}}/300.css";
  @import "@fontsource/{{FONT_BODY | lower}}/400.css";
  @import "@fontsource/{{FONT_BODY | lower}}/500.css";
  @import "@fontsource/{{FONT_BODY | lower}}/600.css";

  @import "tailwindcss";

  :root {
  /* Raw palette (HSL triplets - no hsl() wrapper, so we can do alpha in Tailwind) */
  --ink: {{COLOR_INK}};
  --cream: {{COLOR_CREAM}};
  --ochre: {{COLOR_OCHRE}};
  --terra: {{COLOR_TERRA}};

  /* Semantic tokens */
  --background: var(--ink);
  --foreground: var(--cream);
  --card: var(--ink);
  --card-foreground: var(--cream);
  --popover: var(--ink);
  --popover-foreground:var(--cream);
  --primary: var(--ochre);
  --primary-foreground: var(--ink);
  --secondary: var(--terra);
  --secondary-foreground: var(--cream);
  --muted: 240 4% 16%;
  --muted-foreground: 40 6% 72%;
  --accent: var(--ochre);
  --accent-foreground: var(--ink);
  --destructive: 0 72% 51%;
  --destructive-foreground: var(--cream);
  --border: 40 30% 90% / 0.18;
  --input: 40 30% 90% / 0.18;
  --ring: var(--ochre);
  --radius: 0.75rem;

  /* Typography roles */
  --font-display: "{{FONT_DISPLAY}}", "Impact", "Arial Narrow", sans-serif;
  --font-body: "{{FONT_BODY}}", -apple-system, BlinkMacSystemFont, "Helvetica Neue", system-ui, sans-serif;

  /* Layout */
  --gutter: clamp(20px, 4.2vw, 56px);
  --max: 1440px;
  }

  html, body, #root { background: hsl(var(--background)); color: hsl(var(--foreground)); }
  html { scroll-behavior: smooth; }
  body {
  font-family: var(--font-body);
  font-size: 16px;
  line-height: 1.55;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
  overflow-x: hidden;
  }
  .font-display { font-family: var(--font-display); }
  .font-body { font-family: var(--font-body); }
  ```
- Add inside index.css under @layer components. These two classes are the visual backbone of every card, pill, and CTA.
- **6. TAILWIND v4 CONFIG (inside index.css)**
- Tailwind v4 uses the @theme at-rule INSIDE CSS. Place this block after @import "tailwindcss";.
  ```css
  @theme {
  --color-background: hsl(var(--background));
  --color-foreground: hsl(var(--foreground));
  --color-card: hsl(var(--card));
  --color-card-foreground: hsl(var(--card-foreground));
  --color-popover: hsl(var(--popover));
  --color-popover-foreground: hsl(var(--popover-foreground));
  --color-primary: hsl(var(--primary));
  --color-primary-foreground: hsl(var(--primary-foreground));
  --color-secondary: hsl(var(--secondary));
  --color-secondary-foreground: hsl(var(--secondary-foreground));
  --color-muted: hsl(var(--muted));
  --color-muted-foreground: hsl(var(--muted-foreground));
  --color-accent: hsl(var(--accent));
  --color-accent-foreground:hsl(var(--accent-foreground));
  --color-destructive: hsl(var(--destructive));
  --color-border: hsl(var(--border));
  --color-input: hsl(var(--input));
  --color-ring: hsl(var(--ring));

  --font-display: "{{FONT_DISPLAY}}", sans-serif;
  --font-body: "{{FONT_BODY}}", sans-serif;

  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --radius-2xl: calc(var(--radius) + 10px);
  --radius-3xl: calc(var(--radius) + 18px);

  --animate-marquee: marquee 28s linear infinite;
  --animate-marquee-rev: marquee-rev 32s linear infinite;
  --animate-fade-up: fade-up 0.7s cubic-bezier(0.22, 1, 0.36, 1) forwards;
  }

  @keyframes marquee { from { transform: translateX(0) } to { transform: translateX(-50%) } }
  @keyframes marquee-rev { from { transform: translateX(-50%) } to { transform: translateX(0) } }
  @keyframes fade-up {
  from { opacity: 0; transform: translate3d(0, 24px, 0); filter: blur(6px); }
  to { opacity: 1; transform: translate3d(0, 0, 0); filter: blur(0); }
  }
  ```
- **7. SHADCN BUTTON VARIANTS**
- Open src/components/ui/button.tsx (generated by npx shadcn add button). Add these three variants in the buttonVariants cva variants.variant block:
  ```typescript
  hero: "bg-primary text-primary-foreground rounded-full px-7 py-3.5 text-base font-medium tracking-[-0.01em] hover:bg-primary/90 transition-colors",
  heroGlass: "liquid-glass-strong text-foreground rounded-full px-7 py-3.5 text-base font-normal tracking-[-0.01em] hover:bg-white/5 transition-colors",
  heroSolid: "bg-foreground text-background rounded-full px-7 py-3.5 text-base font-medium tracking-[-0.01em] hover:bg-foreground/90 transition-colors",
  ```
- Usage: &lt;Button variant="hero">...&lt;/Button>.
- **8. SCRUB SEQUENCE COMPONENT - src/components/ScrubSequence.tsx**
- This is the centerpiece. Reproduce this component verbatim. It renders the hero video as a frame-indexed canvas tied to scroll position.
  ```typescript
  import { useEffect, useRef } from "react";

  export type ScrubSequenceProps = {
  framesPath: string; // e.g. "/frames"
  frameCount: number; // e.g. 240
  ext?: "jpg" | "webp"; // default "jpg"
  className?: string;
  /** Padding element the scrub reads its scroll range from. Should wrap the hero. */
  scrollTargetRef: React.RefObject<HTMLElement>;
  };

  const pad4 = (n: number) => String(n).padStart(4, "0");

  export function ScrubSequence({
  framesPath,
  frameCount,
  ext = "jpg",
  className,
  scrollTargetRef,
  }: ScrubSequenceProps) {
  const canvasRef = useRef<HTMLCanvasElement>(null);
  const imagesRef = useRef<HTMLImageElement[]>([]);
  const rafRef = useRef<number | null>(null);
  const visible = useRef(true);
  const prefersReduced = useRef(
  typeof window !== "undefined" &&
  window.matchMedia("(prefers-reduced-motion: reduce)").matches
  );

  // --- Preload all frames ---
  useEffect(() => {
  const imgs: HTMLImageElement[] = [];
  const urls = Array.from(
  { length: frameCount },
  (_, i) => `${framesPath}/frame_${pad4(i + 1)}.${ext}`
  );
  // Priority-load frame 1 so first paint is immediate
  const first = new Image();
  first.src = urls[0];
  // @ts-ignore - fetchpriority is valid but typings lag
  first.fetchPriority = "high";
  imgs[0] = first;

  // Load the rest in parallel
  urls.slice(1).forEach((src, i) => {
  const img = new Image();
  img.src = src;
  imgs[i + 1] = img;
  });
  imagesRef.current = imgs;
  }, [framesPath, frameCount, ext]);

  // --- Resize canvas to viewport with dpr ---
  useEffect(() => {
  const canvas = canvasRef.current;
  if (!canvas) return;
  const resize = () => {
  const dpr = Math.min(window.devicePixelRatio || 1, 2);
  canvas.width = window.innerWidth * dpr;
  canvas.height = window.innerHeight * dpr;
  canvas.style.width = "100%";
  canvas.style.height = "100%";
  drawFrame(currentIndex());
  };
  resize();
  window.addEventListener("resize", resize);
  return () => window.removeEventListener("resize", resize);
  // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  // --- Pause rAF when off-screen ---
  useEffect(() => {
  const el = scrollTargetRef.current;
  if (!el) return;
  const io = new IntersectionObserver(
  ([entry]) => { visible.current = entry.isIntersecting; },
  { threshold: 0 }
  );
  io.observe(el);
  return () => io.disconnect();
  }, [scrollTargetRef]);

  // --- rAF scroll loop ---
  useEffect(() => {
  const tick = () => {
  if (visible.current && !prefersReduced.current) {
  drawFrame(currentIndex());
  }
  rafRef.current = requestAnimationFrame(tick);
  };
  tick();
  return () => { if (rafRef.current) cancelAnimationFrame(rafRef.current); };
  // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  // --- Static fallback for reduced motion ---
  useEffect(() => {
  if (prefersReduced.current) {
  const mid = Math.floor(frameCount / 2);
  const img = imagesRef.current[mid];
  if (img?.complete) drawImage(img);
  else img?.addEventListener("load", () => drawImage(img), { once: true });
  }
  }, [frameCount]);

  const currentIndex = () => {
  const el = scrollTargetRef.current;
  if (!el) return 0;
  const rect = el.getBoundingClientRect();
  const total = el.offsetHeight - window.innerHeight;
  const progress = total > 0
  ? Math.min(1, Math.max(0, -rect.top / total))
  : 0;
  return Math.min(frameCount - 1, Math.floor(progress * (frameCount - 1)));
  };

  const drawFrame = (idx: number) => {
  const img = imagesRef.current[idx];
  if (img && img.complete && img.naturalWidth > 0) drawImage(img);
  };

  const drawImage = (img: HTMLImageElement) => {
  const canvas = canvasRef.current;
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  if (!ctx) return;
  const cw = canvas.width, ch = canvas.height;
  const iw = img.naturalWidth, ih = img.naturalHeight;
  // object-cover math
  const scale = Math.max(cw / iw, ch / ih);
  const dw = iw * scale, dh = ih * scale;
  const dx = (cw - dw) / 2, dy = (ch - dh) / 2;
  ctx.clearRect(0, 0, cw, ch);
  ctx.drawImage(img, dx, dy, dw, dh);
  };

  return (
  <canvas
  ref={canvasRef}
  className={className}
  style={{ transform: "translateZ(0)", willChange: "contents" }}
  />
  );
  }
  ```
- Key rules for the generating model:
- The hero wraps &lt;Hero> content inside a &lt;section ref={scrollTargetRef} className="relative h-\[250vh\]">. The 250vh gives the scrub enough scroll distance to play the whole sequence. Tune to 200vh400vh depending on FRAME_COUNT.
- The canvas is position: fixed; inset: 0; z-index: 0; inside a &lt;div className="sticky top-0 h-screen"> - so it stays pinned while the outer section scrolls.
- Content above the canvas (headline, CTAs) has z-index: 10 and sticky positioning so it stays in the viewport with the canvas.
- Do NOT use &lt;video> for the hero. Do NOT use position: absolute on the canvas - it must be sticky-fixed.
- **9. BLURTEXT COMPONENT - src/components/BlurText.tsx**
- Reusable word-stagger headline animation. Every section heading uses this.
  ```typescript
  import { motion, useInView } from "motion/react";
  import { useRef } from "react";

  type Props = {
  text: string;
  className?: string;
  delay?: number; // seconds between words
  startDelay?: number; // seconds before first word
  as?: keyof JSX.IntrinsicElements;
  };

  export function BlurText({
  text,
  className = "",
  delay = 0.07,
  startDelay = 0,
  as: Tag = "h2",
  }: Props) {
  const ref = useRef<HTMLElement>(null);
  const inView = useInView(ref, { once: true, amount: 0.3 });
  const words = text.split(" ");

  return (
  <Tag ref={ref as any} className={className}>
  {words.map((w, i) => (
  <motion.span
  key={i}
  className="inline-block will-change-[filter,transform,opacity]"
  initial={{ filter: "blur(10px)", opacity: 0, y: 24 }}
  animate={inView? { filter: "blur(0)", opacity: 1, y: 0 }: undefined}
  transition={{
  duration: 0.7,
  ease: [0.22, 1, 0.36, 1],
  delay: startDelay + i * delay,
  }}
  >
  {w}
  {i < words.length - 1? "\\u00A0": ""}
  </motion.span>
  ))}
  </Tag>
  );
  }
  ```
- **10. CONSTANTS FILE - src/lib/constants.ts**
  ```typescript
  export const FRAMES_PATH = "{{FRAMES_PATH}}";
  export const FRAME_COUNT = {{FRAME_COUNT}};
  export const FRAME_EXT = "{{FRAME_EXT}}" as const;
  ```
- Every component imports from here; there are no magic numbers scattered in the code.
- **SECTION 1 - NAVBAR (floating liquid-glass pill)**
- File: src/components/Navbar.tsx
- Layout: Fixed at the top, centered, floating 16px from the viewport top. A single liquid-glass rounded-full pill containing logo, center links, and a primary CTA on the right.
- Spec:
- Container: fixed top-4 left-1/2 -translate-x-1/2 z-50 w-\[min(1200px,calc(100vw-32px))\].
- Inner: liquid-glass rounded-full px-2 py-2 flex items-center justify-between gap-4.
- Left: logo wrapper flex items-center gap-2 pl-3, logo &lt;img src="{{LOGO_PATH}}" className="h-6 w-auto" />, brand text &lt;span className="font-display text-lg tracking-tight">{{BRAND_NAME}}&lt;/span>.
- Center: &lt;nav className="hidden md:flex items-center gap-1"> containing {{NAV_ITEMS}} rendered as &lt;a className="px-3.5 py-2 text-sm text-foreground/80 hover:text-foreground transition-colors font-body">{item.label}&lt;/a>.
- Right: primary CTA &lt;Button variant="heroSolid" size="sm" className="rounded-full px-4 py-1.5 text-sm">{{CTA_LABEL}} &lt;ArrowUpRight className="ml-1 size-4" />&lt;/Button>.
- Mobile (&lt; md): replace center links with a right-aligned &lt;Menu /> icon button that opens a full-screen liquid-glass sheet with the links stacked.
- Behavior:
- On scroll > 40px: apply backdrop-blur-xl via data-\[scrolled=true\] attribute, and reduce top offset from top-4 to top-2. Use Framer Motion's useScroll + useMotionValueEvent.
- Active link: if the section in view matches the anchor, render text as text-foreground and add a subtle dot h-1 w-1 rounded-full bg-primary below.
- **SECTION 2 - HERO (scrub sequence + headline + CTAs)**
- File: src/components/Hero.tsx
- Structure:
  ```typescript
  <section ref={scrollRef} className="relative h-[250vh] bg-background">
  <div className="sticky top-0 h-screen w-full overflow-hidden">
  {/* Frame sequence canvas */}
  <ScrubSequence
  framesPath={FRAMES_PATH}
  frameCount={FRAME_COUNT}
  ext={FRAME_EXT}
  scrollTargetRef={scrollRef}
  className="absolute inset-0 w-full h-full z-0"
  />
  {/* Cinematic vignette */}
  <div className="absolute inset-0 z-[1] bg-[radial-gradient(120%_80%_at_50%_60%,transparent_40%,rgba(0,0,0,0.55)_100%)]" />
  {/* Bottom fade into next section */}
  <div className="absolute bottom-0 inset-x-0 h-[40vh] z-[2] gradient-fade-b" />
  {/* Content */}
  <div className="absolute inset-0 z-10 flex flex-col items-center justify-center text-center px-6">
  <motion.div initial={{opacity:0, y:12}} animate={{opacity:1, y:0}} transition={{delay:0.2}}>
  <div className="liquid-glass rounded-full px-1 py-1 inline-flex items-center gap-2">
  <span className="bg-foreground text-background rounded-full px-3 py-1 text-xs font-semibold">{{LANG === "fr-CH"? "Nouveau": "New"}}</span>
  <span className="pr-3 text-sm text-foreground/85">{{BRAND_TAGLINE}}</span>
  </div>
  </motion.div>

  <BlurText
  text="{{HERO_HEADLINE}}"
  as="h1"
  className="mt-6 font-display uppercase text-[clamp(56px,9vw,144px)] leading-[0.92] tracking-[-0.02em] text-foreground max-w-[14ch]"
  delay={0.09}
  startDelay={0.15}
  />

  <motion.p
  initial={{filter:"blur(10px)", opacity:0, y:16}}
  animate={{filter:"blur(0)", opacity:1, y:0}}
  transition={{delay:0.9, duration:0.7, ease:[0.22,1,0.36,1]}}
  className="mt-6 font-body text-base md:text-lg text-foreground/70 max-w-xl leading-relaxed"
  >
  {{HERO_SUB}}
  </motion.p>

  <motion.div
  initial={{opacity:0, y:12}}
  animate={{opacity:1, y:0}}
  transition={{delay:1.1, duration:0.6}}
  className="mt-10 flex items-center gap-3"
  >
  <Button variant="hero" asChild>
  <a href="{{CTA_HREF}}">{{HERO_CTA_PRIMARY}} <ArrowUpRight className="ml-1 size-4" /></a>
  </Button>
  <Button variant="heroGlass">
  <Play className="mr-1.5 size-4 fill-current" /> {{HERO_CTA_SECONDARY}}
  </Button>
  </motion.div>

  {/* Partners row - absolute bottom */}
  <div className="absolute bottom-10 inset-x-0 flex flex-col items-center gap-4">
  <span className="liquid-glass rounded-full px-4 py-1.5 text-xs font-body text-foreground/80">
  {{LANG === "fr-CH"? "Ils nous font confiance": "Trusted by"}}
  </span>
  <div className="flex items-center gap-8 md:gap-14 flex-wrap justify-center px-6">
  {{PARTNERS}}.map(p => (
  <span className="font-display italic text-xl md:text-2xl text-foreground/70 tracking-tight">
  {p}
  </span>
  ))
  </div>
  </div>
  </div>
  </div>
  </section>
  ```
- Rules:
- The section height is 250vh. The inner .sticky top-0 h-screen keeps the scrub pinned while the outer section scrolls through 2.5 viewports - this is what "plays" the sequence.
- Headline is font-display uppercase, letter-spacing 0.02em, leading 0.92. Caps are non-negotiable for editorial feel. Max 14ch wrap.
- CTA row: 1 solid ochre + 1 glass outline. Icons are 16px from lucide-react.
- Partners row: absolutely positioned bottom, not in flex flow, to survive on short hero.
- **SECTION 3 - SERVICES BENTO**
- File: src/components/ServicesBento.tsx
- Intent: Show 6 offerings as an asymmetric bento (1 tall + 3 small + 1 wide + 1 small). Every card is liquid-glass, rounded-2xl, hover-lifts with a subtle scale.
- Grid (desktop):
  ```text
  [ tall ][ small ][ small ]
  [ tall ][ wide ]
  ```
- Implemented as:
  ```typescript
  <div className="grid grid-cols-1 md:grid-cols-3 gap-4 md:gap-5 max-w-[var(--max)] mx-auto px-[var(--gutter)]">
  {/* idx 0: tall - row-span-2 */}
  {/* idx 1, 2: small */}
  {/* idx 3: wide - col-span-2 */}
  {/* idx 4: small (next to wide, same row) - actually occupy col 3 of row 2 */}
  {/* idx 5: row 3 full-width card */}
  </div>
  ```
- Use explicit per-card classes:
- Card 0: md:row-span-2 md:col-span-1 p-8 min-h-\[480px\]
- Card 1: md:col-span-1 p-6 min-h-\[228px\]
- Card 2: md:col-span-1 p-6 min-h-\[228px\]
- Card 3: md:col-span-2 p-7 min-h-\[228px\] (wide)
- Card 4: md:col-span-1 p-6 min-h-\[228px\] (next to wide - actually needs to be on the wide's row; restructure if needed)
- Card 5: md:col-span-3 p-7 min-h-\[200px\] (full-width)
- Each card structure:
  ```typescript
  <motion.div
  className="liquid-glass rounded-2xl p-6 relative overflow-hidden group"
  whileHover={{ y: -4 }}
  transition={{ type: "spring", stiffness: 260, damping: 26 }}
  >
  <div className="liquid-glass-strong rounded-full w-11 h-11 flex items-center justify-center mb-5">
  <Icon className="size-5 text-foreground" />
  </div>
  <h3 className="font-display uppercase text-2xl md:text-3xl leading-[0.95] tracking-tight mb-3 max-w-[18ch]">
  {service.title}
  </h3>
  <p className="font-body text-sm text-foreground/65 max-w-[38ch] leading-relaxed">
  {service.body}
  </p>
  <ArrowUpRight className="absolute top-6 right-6 size-5 text-foreground/30 group-hover:text-foreground/80 transition-colors" />
  </motion.div>
  ```
- Section wrapper:
- &lt;section id="services" className="relative py-28 md:py-40"> with a small badge above the grid: &lt;span className="liquid-glass rounded-full px-4 py-1.5 text-xs text-foreground/80">{{LANG === "fr-CH"? "Nos services": "What we do"}}&lt;/span>.
- Big &lt;BlurText> heading above: "Tout ce qui bouge. Sous un seul toit." (or the EN equivalent - this headline is also a placeholder {{SERVICES_HEADLINE}} - add to the legend if the user has strong opinions; otherwise default).
- {{SERVICES}} array shape:
  ```typescript
  [
  { icon: "Truck", title: "Déménagement", body: "..." },
  { icon: "Package", title: "Emballage", body: "..." },
  { icon: "Warehouse", title: "Garde-meubles",body: "..." },
  { icon: "Globe", title: "International",body: "..." },
  { icon: "Building2", title: "Bureaux", body: "..." },
  { icon: "Sparkles", title: "Sur-mesure", body: "..." },
  ]
  ```
- **SECTION 4 - POURQUOI NOUS (4-column "why us" grid)**
- File: src/components/Pourquoi.tsx
- Intent: Four reassurance pillars, tight and dense. This is the rational-counterpart to the emotional hero.
- Spec:
- Wrapper: &lt;section className="relative py-28 md:py-40 border-t border-border/40">.
- Heading (BlurText): font-display uppercase text-4xl md:text-6xl leading-\[0.9\] max-w-\[18ch\] mx-auto text-center tracking-tight, plus a one-sentence sub under it in text-foreground/65.
- Grid: grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-5 mt-16 max-w-\[var(--max)\] mx-auto px-\[var(--gutter)\].
- Each card: liquid-glass rounded-2xl p-7 flex flex-col gap-5 min-h-\[260px\].
  - Icon in a liquid-glass-strong rounded-full w-11 h-11 flex items-center justify-center.
  - Title: font-display uppercase text-xl tracking-tight.
  - Body: font-body text-sm text-foreground/65 leading-relaxed.
  - A thin bottom-accent: &lt;div className="mt-auto h-px w-10 bg-gradient-to-r from-primary to-transparent" />.
- {{REASONS}} array shape (4 entries, each {icon, title, body}):
  ```typescript
  [
  { icon: "ShieldCheck", title: "Assuré intégralement", body: "..." },
  { icon: "Clock", title: "Ponctuels", body: "..." },
  { icon: "Leaf", title: "Éco-conscients", body: "..." },
  { icon: "Award", title: "Certifiés Swiss Moving", body: "..." },
  ]
  ```
- **SECTION 5 - PROCESS STEPS (horizontal numbered flow)**
- File: src/components/Process.tsx
- Intent: How it works in 3 or 4 steps. Numbered, horizontal on desktop, vertical on mobile, with connector lines that animate in on scroll.
- Layout (desktop):
- grid grid-cols-1 md:grid-cols-4 gap-0 relative (gap-0 because connectors fill the gap).
- Each step:
  ```typescript
  <div className="relative px-6 md:px-10 py-10 md:py-14 flex flex-col gap-4 items-start">
  <span className="font-display text-[96px] md:text-[140px] leading-none text-primary/25 -mb-6 select-none">
  {n.padStart(2, "0")}
  </span>
  <h3 className="font-display uppercase text-2xl md:text-3xl tracking-tight">
  {step.title}
  </h3>
  <p className="font-body text-sm text-foreground/65 leading-relaxed max-w-[30ch]">
  {step.body}
  </p>
  </div>
  ```
- Between steps, a horizontal rule: absolute top-16 right-0 translate-x-1/2 w-px h-\[calc(100%-64px)\] bg-gradient-to-b from-transparent via-border to-transparent hidden md:block. For desktop horizontal flow, switch to a horizontal rule: absolute top-20 -right-0 h-px w-full bg-gradient-to-r from-border via-border to-transparent.
- Heading pattern: same badge + BlurText as every section.
- {{PROCESS_STEPS}} array shape (3-4 entries, each {n, title, body}): n is "1".."4".
- **SECTION 6 - STATS BAND**
- File: src/components/Stats.tsx
- Intent: Social-proof numbers on a cinematic desaturated video background - same pattern as Prompt2.md Stats section.
- Spec:
- &lt;section className="relative py-32 md:py-44 overflow-hidden">.
- Background: a &lt;video> at autoPlay loop muted playsInline with src="{{STATS_BG_VIDEO}}" (MP4 or via hls.js for .m3u8), absolute-positioned inset-0 w-full h-full object-cover filter saturate(0). If the URL is .m3u8, lazy-import hls.js and attach; if .mp4, set src directly.
- Top + bottom 200px gradient fades (gradient-fade-t, gradient-fade-b).
- Inner card: liquid-glass rounded-3xl p-10 md:p-14 mx-\[var(--gutter)\] max-w-\[var(--max)\] md:mx-auto relative z-10.
- Inside: grid grid-cols-2 md:grid-cols-4 gap-8 md:gap-12.
  - Each stat: value font-display italic text-5xl md:text-6xl lg:text-7xl leading-none text-foreground, label below font-body text-sm text-foreground/60 mt-3 tracking-wide uppercase.
  - Separator between items (desktop only): &lt;div className="hidden md:block absolute top-1/2 -translate-y-1/2 w-px h-12 bg-border" /> positioned at the 25%, 50%, 75% marks.
- Animate each stat value with a motion.span counting from 0 to the number when in view (if the value is purely numeric - strip non-digits, preserve suffix like +).
- {{STATS}} array shape (exactly 4 entries, each {value, label}):
  ```typescript
  [
  { value: "2500+", label: "Déménagements" },
  { value: "98%", label: "Clients satisfaits" },
  { value: "24h", label: "Délai de devis" },
  { value: "15 ans",label: "Métier" },
  ]
  ```
- **SECTION 7 - TESTIMONIALS MARQUEE**
- File: src/components/Testimonials.tsx
- Intent: Two rows of testimonials scrolling in opposite directions - infinite marquee.
- Spec:
- &lt;section id="testimonials" className="relative py-28 md:py-40">.
- Badge + &lt;BlurText as="h2"> heading as every section. Heading: {{LANG === "fr-CH"? "Ils parlent mieux que nous.": "Don't take our word for it."}}.
- Two rows below the heading, each a horizontal marquee: (the animate-\[...\] utility uses the theme tokens declared in the @theme block.)
  ```typescript
  <div className="relative mt-16 flex flex-col gap-5 overflow-hidden [mask-image:linear-gradient(to_right,transparent,black_8%,black_92%,transparent)]">
  <div className="flex gap-5 w-max animate-[marquee_var(--animate-marquee)]">
  {[...TESTIMONIALS, ...TESTIMONIALS].map((t, i) => <Card key={i} {...t} />)}
  </div>
  <div className="flex gap-5 w-max animate-[marquee-rev_var(--animate-marquee-rev)]">
  {[...TESTIMONIALS.slice(3), ...TESTIMONIALS.slice(0,3), ...TESTIMONIALS.slice(3), ...TESTIMONIALS.slice(0,3)].map((t, i) => <Card key={i} {...t} />)}
  </div>
  </div>
  ```
- Each card: liquid-glass rounded-2xl p-7 w-\[340px\] md:w-\[400px\] shrink-0 flex flex-col gap-5.
  - &lt;Quote className="size-5 text-primary/70" /> at top.
  - Quote body: font-body text-foreground/85 italic leading-relaxed text-\[15px\].
  - Author row: &lt;div className="mt-auto flex items-center gap-3"> containing an avatar placeholder (&lt;div className="size-9 rounded-full bg-gradient-to-br from-primary/60 to-secondary/60" />), name font-body font-medium text-sm, role font-body text-xs text-foreground/55 uppercase tracking-wide.
- {{TESTIMONIALS}} array shape (≥6, each {quote, name, role}).
- Pause on hover: add hover:\[animation-play-state:paused\] to each row container, and group + group-hover:\[animation-play-state:paused\] so both rows pause when either is hovered.
- **SECTION 8 - FAQ ACCORDION**
- File: src/components/Faq.tsx
- Intent: Classic editorial FAQ using shadcn Accordion, but with a two-column layout: title on the left (sticky), accordion on the right. Desktop only; on mobile it stacks.
- Spec:
- &lt;section id="faq" className="relative py-28 md:py-40">.
- &lt;div className="max-w-\[var(--max)\] mx-auto px-\[var(--gutter)\] grid grid-cols-1 md:grid-cols-\[0.9fr_1.1fr\] gap-16">
- Left column (sticky, md:sticky md:top-24 md:self-start):
  - Badge.
  - &lt;BlurText as="h2" text="{{LANG === "fr-CH"? "Questions fréquentes.": "Frequently asked."}}" className="font-display uppercase text-5xl md:text-6xl leading-\[0.9\] tracking-tight mt-4" />.
  - A paragraph + a Button variant="heroGlass" "Nous contacter".
- Right column: &lt;Accordion type="single" collapsible> with items:
  ```typescript
  <AccordionItem value={`item-${i}`} className="border-border/40">
  <AccordionTrigger className="font-display uppercase text-lg md:text-xl tracking-tight py-6 hover:no-underline data-[state=open]:text-primary">
  {item.q}
  </AccordionTrigger>
  <AccordionContent className="font-body text-foreground/70 text-[15px] leading-relaxed pb-6 max-w-[60ch]">
  {item.a}
  </AccordionContent>
  </AccordionItem>
  ```
- {{FAQ_ITEMS}} array shape (5-8 entries, each {q, a}).
- **SECTION 9 - CTA + FOOTER CINÉMATIQUE**
- File: src/components/CtaFooter.tsx
- Intent: Final beat. Huge italic headline on a cinematic video background. Two CTAs. Footer bar under it.
- Spec (CTA part):
- &lt;section className="relative min-h-\[100vh\] flex flex-col items-center justify-center overflow-hidden">.
- Background: HLS or MP4 video same pattern as Stats - {{CTA_BG_VIDEO}}, filter: brightness(0.55). No desaturate here (vs stats which is saturate(0)).
- Top + bottom gradient fades (200px).
- Content (z-10, centered):
  - &lt;BlurText as="h2" text="{{CTA_HEADLINE}}" className="font-display italic text-\[clamp(56px,10vw,180px)\] leading-\[0.88\] tracking-\[-0.02em\] text-center max-w-\[16ch\]" />
  - &lt;p className="mt-8 font-body text-base md:text-lg text-foreground/75 max-w-xl text-center">{{CTA_SUB}}&lt;/p>.
  - Buttons row: &lt;div className="mt-10 flex items-center gap-3 flex-wrap justify-center"> containing &lt;Button variant="hero">{{CTA_LABEL}}&lt;/Button> and &lt;Button variant="heroGlass">{{LANG === "fr-CH"? "Nos tarifs": "Pricing"}}&lt;/Button>.
- Spec (footer bar):
- Below the hero block, inside the same section at the bottom:
  ```typescript
  <div className="relative z-10 w-full border-t border-border/40 mt-auto">
  <div className="max-w-[var(--max)] mx-auto px-[var(--gutter)] py-8 flex flex-col md:flex-row items-center justify-between gap-4">
  <span className="font-body text-xs text-foreground/50">{{COPYRIGHT}}</span>
  <nav className="flex items-center gap-6">
  {{FOOTER_LINKS}}.map(l => <a className="font-body text-xs text-foreground/50 hover:text-foreground/80 transition-colors">{l.label}</a>)
  </nav>
  </div>
  </div>
  ```
- **20. GLOBAL ANIMATION PATTERNS (recap - reuse verbatim)**
- Every animation in the site comes from one of these five primitives. Do not invent new ones.
- BlurText - section headings. Word-by-word stagger, 0.07s between words, 0.7s duration per word, cubic-bezier(0.22, 1, 0.36, 1).
- Fade-up-on-view - subtext and CTAs. initial={{opacity:0, y:16, filter:"blur(8px)"}} → whileInView={{opacity:1, y:0, filter:"blur(0)"}}, viewport={{once:true, amount:0.3}}.
- Scroll-scrub canvas - hero only. The single mandatory interactive element. Implementation in Section 8 of this prompt.
- Marquee - partners row in hero, testimonials row. 28s one direction, 32s reverse; gradient mask on each end; pause on hover.
- Liquid-glass ::before mask border - every card, pill, button. Gives the thin glowing top/bottom border. Never replace with a regular border.
- **21. PAGE COMPOSITION - src/App.tsx**
  ```typescript
  import { useRef } from "react";
  import { Navbar } from "@/components/Navbar";
  import { Hero } from "@/components/Hero";
  import { ServicesBento } from "@/components/ServicesBento";
  import { Pourquoi } from "@/components/Pourquoi";
  import { Process } from "@/components/Process";
  import { Stats } from "@/components/Stats";
  import { Testimonials } from "@/components/Testimonials";
  import { Faq } from "@/components/Faq";
  import { CtaFooter } from "@/components/CtaFooter";

  export default function App() {
  const heroRef = useRef<HTMLElement>(null);
  return (
  <div className="bg-background text-foreground min-h-screen">
  <Navbar />
  <main>
  <Hero scrollRef={heroRef} />
  <ServicesBento />
  <Pourquoi />
  <Process />
  <Stats />
  <Testimonials />
  <Faq />
  <CtaFooter />
  </main>
  </div>
  );
  }
  ```
- Hero receives scrollRef as a prop so App.tsx owns the reference that both the outer tall section and the inner &lt;ScrubSequence> need.
- **22. ANTI-SLOP GUARDRAILS (read before submitting)**
- Every violation of these rules is a defect - the generating model must self-check before returning.
- No emoji anywhere. Not in copy, not in card headers, not in buttons.
- No default violet/purple gradients. The palette is warm (ochre + terra + cream + ink). Gradients use -primary → transparent, never from-blue-500 to-purple-600.
- No shadow-2xl on cards. Shadows on liquid-glass are the ::before border and the inset highlight only. If you need depth, use backdrop blur, not drop shadow.
- No rounded-3xl on buttons. Buttons are rounded-full. Cards are rounded-2xl. Inner pills are rounded-full. There is no rounded-xlmid-level rhythm in this design.
- No placeholder lorem ipsum in the final output. If the user has not filled a placeholder, output a clearly-flagged \[TODO: {{PLACEHOLDER_NAME}}\] instead, so it's obvious at first glance.
- No text-center on body paragraphs except the hero and CTA section. Body prose is left-aligned by default - centered prose on a card is the #1 AI-slop tell.
- Headings are font-display uppercase (with tracking-tight) OR font-display italic - never both on the same element, and never plain sentence-case serif on a dark background.
- Every section has a badge + heading + sub pattern at the top, except the hero (which is its own world) and the footer (which is bare). Badges are liquid-glass rounded-full px-4 py-1.5 text-xs.
- No stock icons outside lucide-react. No heroicons, no Material, no custom SVGs unless supplied by the user.
- Never use &lt;video> for the hero. The hero is a canvas. &lt;video> appears only in Stats and CTA backgrounds.
- No motion.div with a long transition={{ duration: 2 }}. Every fade-in completes in ≤ 0.9s. Sites that feel slow feel bad.
- No console.log, no commented-out code, no empty files, no unused imports in the delivered project.
- Copy: the site is in {{LANG}}. Do not auto-translate placeholders. If a placeholder is {{HERO_SUB}} and the user wrote French, leave it French.
- Responsive: desktop 1440 is the hero canvas, but every section must render cleanly at 375px (iPhone SE) with no horizontal scroll.
- Accessibility: every interactive element has a visible focus ring (focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 focus-visible:ring-offset-background). The canvas has aria-hidden="true" and a visually-hidden sibling &lt;p className="sr-only"> summarising the hero video.
- **23. VERIFICATION (run before declaring done)**
- The generating model must execute these checks and report in the final message:
- Build:
- npm run dev - starts with no error, prints a localhost URL.
- npm run build - completes with no TypeScript error and no Vite error.
- Visual:
- Hero first paint shows frame 1 within 300ms (the priority-preloaded frame).
- Scrolling the hero scrubs the canvas smoothly (no visible stall > 50ms) through ≥ FRAME_COUNT / 2.5 distinct frames.
- Marquee rows loop seamlessly (duplicate the array so the midpoint is invisible).
- FAQ accordion opens and closes with smooth height animation.
- Navbar pill reduces top-4 → top-2 when scrolled > 40px.
- Mobile 375px: no horizontal overflow, hero scrub still renders, bento collapses to single column, testimonials marquee still animates.
- Console:
- No React warnings.
- No 404s on frame URLs. If any frame 404s, the user forgot to run the ffmpeg extraction - the model should print a clear banner in the dev HTML page pointing them to Section 2 of this prompt.
- Perf:
- Lighthouse Performance ≥ 85 on desktop.
- LCP &lt; 2.5s (the first frame is the LCP element - preload it with &lt;link rel="preload" as="image" href="/frames/frame_0001.{{FRAME_EXT}}" fetchpriority="high"> in index.html).
- **24. FINAL NOTE TO THE GENERATING MODEL**
- You receive this entire document as one prompt. Do not ask clarifying questions. Do not trim sections. Do not substitute Next.js for Vite. Do not swap Framer Motion for GSAP. Do not skip the scroll-scrub canvas and replace it with a &lt;video> - that single decision is the difference between this being a great site and a generic one.
- If a {{PLACEHOLDER}} is empty in the version you received, leave a clearly visible \[TODO\] marker at that location in the output - don't invent plausible-sounding filler.
- Build it.

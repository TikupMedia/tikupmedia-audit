---
name: tikupmedia
description: TikupMedia proprietary SEO+GEO audit engine. Analyzes a prospect's website and produces a sales-ready HTML audit focused on revenue loss, lost keywords, and competitive analysis. Use when user types `/tikupmedia <url>` or asks for a commercial audit, prospect analysis, sales-oriented audit, or "chauffer un client".
---

# TikupMedia Audit Engine

## What this skill does

Generates a **complete commercial SEO+GEO audit** of a prospect's website and outputs a self-contained HTML report designed to **convert** the prospect into a client.

The audit covers :
- Technical SEO + Core Web Vitals
- Schema.org structured data analysis
- AI search readiness (Google AIO, ChatGPT, Perplexity, Claude, Copilot, Apple Intelligence)
- Content quality + E-E-A-T scoring
- Brand authority signals
- Keyword opportunity (15 strategic keywords with volume + position)
- Competitor analysis (top 3 with traffic estimates)
- **Revenue loss calculation** (industry-specific formulas)
- ROI projection (3-month, 12-month recovery scenarios)
- Action plan (Quick Wins / Medium Term / Strategic)

Output : `~/Downloads/audit-<domain>-<YYYY-MM-DD>.html` — fully self-contained, brandable, ready to send by email.

## When to invoke

- User typed `/tikupmedia <url>`
- User asked for "audit commercial", "audit prospect", "audit pour vente"
- User wants to analyze a competitor for sales outreach
- User wants a single sales-ready deliverable for a prospect

## Execution plan

### Phase 0 — Setup (30s)

1. Read `~/.claude/skills/tikupmedia/config.json` for branding
2. Extract domain from input URL
3. Create workdir : `mkdir -p /tmp/tikupmedia-<domain>`
4. Fetch homepage via WebFetch → save to `/tmp/tikupmedia-<domain>/homepage.html`
5. Detect business type :
   - `local_service` : phone visible, address, Maps embed
   - `saas` : Pricing/Sign up, /app, API docs
   - `ecommerce` : products, cart, prices, Product schema
   - `agency` : portfolio, case studies, services
   - `restaurant` : menu, opening hours, reservation
   - `publisher` : blog, bylines, dates
   - `personal_brand` : individual name, portfolio, freelance signals
   - `other` : default

### Phase 1 — Parallel analyses (90s)

Launch **4 specialized agents in parallel** (one Agent call per agent, all in a SINGLE message) :

#### Agent A — Technical audit
- Tech stack detection (CMS, frameworks)
- Schema.org count + types present
- Security headers (HSTS, X-Content, CSP, etc.)
- Performance signals (page weight, image formats, lazy-loading)
- Mobile-friendly (viewport, responsive)
- HTTP status, sitemap, robots.txt, llms.txt
- Crawlability + indexability
- AI crawlers allowed/blocked

#### Agent B — Keywords + competitors
- Identify the prospect's main service/product
- Generate 12-15 strategic keywords adapted to business type :
  - 1 brand keyword
  - 4 service primary
  - 4 long-tail
  - 3 commercial intent
- Estimate volumes (Google Suggest + market knowledge)
- Estimate current position (WebSearch for prospect's domain in top 50)
- Identify top 3 competitors via WebSearch
- Estimate competitor monthly traffic
- Identify what competitors do better

#### Agent C — Content & E-E-A-T
- About page presence + author bio
- Expertise signals (certifications, years exp, named clients)
- Experience signals (real projects, testimonials, photos)
- Authoritativeness (press mentions, LinkedIn, Wikipedia)
- Trust (mentions légales, SIRET, CGV, contact)
- Content depth + freshness (blog, copyright year)
- Detect AI-generated vs human content

#### Agent D — Brand & schemas
- Brand presence on : LinkedIn, Crunchbase, Trustpilot, Wikipedia, Wikidata, social media
- Press mentions (WebSearch)
- Schemas currently present
- Schemas critical missing (with ready-to-paste JSON-LD generated)
- sameAs entity disambiguation signals

Each agent writes its JSON output to `/tmp/tikupmedia-<domain>/<agent-name>.json`.

### Phase 2 — Business intelligence (60s)

Run the business analysis agent from `agents/business.md` with :
- `BUSINESS_TYPE` from Phase 0
- `KEYWORDS_DATA` from Agent B
- `OUTPUT_DIR`

This unique TikupMedia agent calculates :
- **Monthly revenue loss** per keyword using industry benchmarks
- **Total revenue loss / month + / year**
- **Recovery projections** (3m / 6m / 12m)
- **Potential leads/clients lost per month**

Output : `business.json`

### Phase 3 — Synthesis (60s)

Read all 5 outputs and consolidate into `synthesis.json` with these fields :

```json
{
  "url": "https://prospect.com",
  "brand_name_prospect": "Prospect",
  "domain": "prospect.com",
  "business_type": "local_service",
  "audit_date": "2026-05-27",

  "score_composite": 26,
  "score_breakdown": {
    "ai_citability": 28,
    "brand_authority": 32,
    "content_eeat": 12,
    "technical": 48,
    "schema": 0,
    "platform_optimization": 31
  },

  "platforms_readiness": {
    "google_aio": 28,
    "chatgpt": 35,
    "perplexity": 22,
    "claude": 30,
    "copilot": 32,
    "apple_intelligence": 40
  },

  "keywords": [...],
  "competitors_top3": [...],
  "schemas_missing": [...],
  "schemas_present": [...],

  "revenue_loss": {
    "monthly": 16740,
    "yearly": 200880,
    "potential_leads_per_month": 56,
    "currency": "EUR"
  },

  "recovery": {
    "month_1_score": 52,
    "month_3_score": 75,
    "month_12_score": 85,
    "month_12_revenue_recovered": 200880
  },

  "key_findings": [
    { "severity": "critical", "category": "schema", "title": "...", "description": "..." }
  ],

  "action_plan": {
    "quick_wins": [...],
    "medium_term": [...],
    "strategic": [...]
  }
}
```

### Phase 4 — HTML generation (30s)

1. Load template : `~/.claude/skills/tikupmedia/templates/audit.html.template`
2. Replace ALL `{{PLACEHOLDER}}` tokens with `synthesis.json` values
3. Generate keyword table rows HTML
4. Generate competitor cards HTML
5. Generate findings HTML
6. Generate action plan columns HTML
7. Write to `~/Downloads/audit-<domain>-<YYYY-MM-DD>.html`
8. `open ~/Downloads/audit-<domain>-<YYYY-MM-DD>.html`

### Phase 5 — Report (10s)

Tell the user :
- ✅ Audit complet généré : `~/Downloads/audit-<domain>.html`
- Score : X/100
- Manque à gagner : Y € / mois
- 3 top findings critiques
- Suggestion : ouvrir le HTML, ajuster les chiffres si besoin, envoyer au prospect

## Adaptation par business type

| Business type | Focus dans l'audit |
|---|---|
| `local_service` | Local Pack + Google Business Profile + Apple Maps |
| `saas` | Pages de comparaison + Knowledge Graph + entity |
| `ecommerce` | Product schemas + reviews + cart abandonment |
| `agency` | Portfolio + brand authority + case studies |
| `publisher` | E-E-A-T + author credentials + article schema |
| `personal_brand` | Person schema + sameAs + social proof |

## Important rules

1. **NEVER invent data** : if an agent returns 0 results, write "0" not "estimated X"
2. **Always include disclaimers** : `±20% estimates` block in the HTML
3. **Adapt CA calculation to industry** : use `agents/business.md` benchmarks
4. **Don't name competitors you can't verify** : use "Concurrent #1 (anonymisé)" if WebSearch fails
5. **Respect robots.txt** : never override
6. **Brand the output** : every HTML uses config.json values, not hardcoded values
7. **Cite real sources** in the audit footer (Backlinko, Gartner, OpenAI public data)

## Customization

Edit `~/.claude/skills/tikupmedia/config.json` to customize :
- Agency identity (name, logo, tagline)
- Design (5 colors, fonts)
- What you sell (services, prices, guarantees)
- Audience (industries, geographies, ICP)
- Audit tone (punchy / professional / friendly)
- CTAs (email, WhatsApp, Calendly)

Or run the setup wizard :
```
/tikupmedia setup
```

## File structure

```
~/.claude/skills/tikupmedia/
├── SKILL.md                   ← This file (orchestrator)
├── README.md                  ← Documentation
├── SHARING.md                 ← Distribution guide
├── LICENSE                    ← MIT
├── config.json                ← Active config (gitignored)
├── config.example.json        ← Template with comments
├── agents/
│   └── business.md            ← Industry revenue loss calculation
├── scripts/
│   └── setup-wizard.md        ← Interactive configurator
└── templates/
    └── audit.html.template    ← HTML output template
```

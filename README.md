<div align="center">

# tikupmedia

**Commercial SEO + GEO audit engine for Claude Code.**

Generate sales-ready HTML audits in 3 minutes — focused on revenue loss, lost keywords, and competitive analysis. White-label brandable per agency.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-7c3aed)](https://claude.com/claude-code)
[![Made by TikupMedia](https://img.shields.io/badge/Made%20by-TikupMedia-e8392b)](https://tikupmedia.com)

[Live demo](https://tikupmedia.com/tikupmedia-demo) · [Documentation](#documentation) · [TikupMedia](https://tikupmedia.com)

</div>

---

## What it does

`tikupmedia` is a Claude Code skill that transforms a prospect's URL into a **persuasive HTML audit** designed to convert them into a paying client.

Unlike traditional SEO audits (score-focused, 50-page PDFs), `tikupmedia` outputs a **commercial deliverable** :

- 🎯 Hero with monthly revenue loss (computed per industry)
- 📋 Keyword table with volume + position + lost revenue per keyword
- 🏆 Top 3 competitors capturing the prospect's traffic
- ⚔️ Side-by-side comparison (current site vs modern 2026 standard)
- 🚨 "Why it will get worse in 2027" section (AI disruption)
- 📈 12-month recovery timeline with score projection
- 💰 Projected ROI (monthly + yearly recovery)
- 📞 Branded CTAs (email + WhatsApp pre-filled)

Output : a single self-contained HTML file in `~/Downloads/audit-<domain>.html` — ready to send to the prospect by email.

---

## How it works (TL;DR in 3 steps)

1. **You install** the skill in your Claude Code (5 min, free)
2. **You configure** your branding once (email, color, what you sell — 10 min)
3. **You type** `/tikupmedia https://any-prospect.com` → 3 minutes later, an HTML audit branded with YOUR colors and YOUR contact info opens in your browser, ready to send to the prospect

That's it. No SaaS subscription, no recurring fee. The skill runs on YOUR Claude Code, with YOUR API key. You own everything you generate.

---

## Setup (5 min, one-time)

### Step 1 — Install the skill

```bash
cd ~/.claude/skills/
git clone https://github.com/tikupmedia/tikupmedia.git
cd tikupmedia
cp config.example.json config.json
```

### Step 2 — Configure YOUR agency (this is the important part)

Open `~/.claude/skills/tikupmedia/config.json` in any text editor and fill in YOUR information. Every audit will use these values.

#### 🏢 Your identity (required)

```json
"agency": {
  "brand_name": "Your Agency Name",
  "site_url": "https://your-website.com",
  "logo_url": "https://your-website.com/your-logo.png",
  "tagline": "What you do, in one short sentence",
  "founded_year": 2020,
  "team_size": "5 people",
  "country": "France"
}
```

→ The `brand_name` appears in the audit footer. `logo_url` must be a public PNG/SVG (host it on your site). `tagline` is shown when you brand the HTML.

#### 🎨 Your colors (required — this is what makes the audit YOURS)

```json
"design": {
  "color_primary": "#e8392b",
  "color_primary_accent": "#ff4a3a",
  "color_background": "#0a0a0c",
  "color_surface": "#14141a",
  "color_text": "#c4c4cc",
  "color_text_bright": "#fafafa"
}
```

5 ready-to-use palettes are included (just copy-paste) :

| Palette | primary | background |
|---|---|---|
| **Blood Dark** (default) | `#e8392b` | `#0a0a0c` |
| **Emerald Dark** | `#10b981` | `#0a0f0c` |
| **Blue Dark** | `#3b82f6` | `#0a0b14` |
| **Purple Dark** | `#8b5cf6` | `#0d0a14` |
| **Minimal Light** | `#0a0a0c` | `#fafafa` |

→ Or pick any hex code you want from your brand.

#### 📞 Your contact details (REQUIRED — this is how the prospect reaches you)

```json
"cta": {
  "email": "you@your-agency.com",
  "whatsapp": "+33612345678",
  "calendly": "https://calendly.com/your-username/30min",
  "phone": "+33 6 12 34 56 78",
  "primary_button_text": "Book a call · 30 min",
  "secondary_button_text": "WhatsApp",
  "email_subject_template": "Audit for {{PROSPECT_URL}} — let's talk",
  "email_body_template": "Hi,\n\nI received your audit showing {{LOSS}} of monthly revenue loss.\n\nI'd like to discuss the action plan.\n\nMy phone: \nMy availability: \n\nThanks."
}
```

→ When the prospect clicks "Book a call" in the audit, an email opens pre-filled with the subject and body above, sent to YOUR email. WhatsApp button opens directly a chat with YOUR number.

→ **⚠️ Without these fields, the audit has no way to convert.** Always fill them.

#### 💼 What you sell (recommended — adapts the action plan)

```json
"what_you_sell": {
  "primary_offer": "What you mainly sell (one sentence)",
  "services_list": [
    "Service 1",
    "Service 2",
    "Service 3"
  ],
  "price_range": {
    "min": 1500,
    "max": 25000,
    "currency": "€",
    "billing_model": "fixed_quote",
    "show_in_audit": false
  },
  "guarantees": [
    "What you promise the client #1",
    "What you promise the client #2",
    "What you promise the client #3"
  ]
}
```

→ `billing_model` can be `fixed_quote`, `monthly_retainer`, `hourly`, `per_project`.
→ `show_in_audit: true` adds your prices visibly in the HTML (transparent agencies love this). Default `false` lets you discuss pricing on the call.

#### 🎯 Who you target (helps adapt the language)

```json
"who_you_target": {
  "ideal_client_profile": "Describe your typical client in one line",
  "industries": ["SaaS", "E-commerce", "Local services"],
  "geographies": ["France", "Belgium"],
  "pain_points_addressed": [
    "Problem #1 your clients have",
    "Problem #2 your clients have"
  ]
}
```

#### 🗣️ Your tone

```json
"audit_tone": {
  "style": "punchy_honest"
}
```

Options :
- `punchy_honest` — direct, shocking numbers (recommended for sales)
- `consultant_professional` — neutral, factual
- `friendly_advisor` — warm, advisory
- `urgent_alarm` — FOMO + AI disruption framing

---

### Step 3 — (Easier alternative) Run the wizard

If editing JSON manually scares you, just type in Claude Code :

```
/tikupmedia setup
```

The skill will ask you 20 questions in plain language and write the config.json for you.

---

### Step 4 — Generate your first audit

In Claude Code :

```
/tikupmedia https://any-prospect-website.com
```

Wait 3 minutes. The HTML opens in your browser. Done.

The file is saved at `~/Downloads/audit-<domain>-<date>.html`. It's a single self-contained file (no images, no external CSS) — just attach it to an email and send.

---

## What you sell (so the audit converts)

The audit is designed to make the prospect think :
1. *"Wow, this agency really analyzed my site in depth"*
2. *"I'm losing X€ every month because of these issues"*
3. *"My competitors are eating my lunch"*
4. *"I should book that call NOW"*

For this to work, your `config.json` must tell the skill :
- **What you do** (so the action plan matches your services)
- **How to contact you** (email + WhatsApp + Calendly)
- **Your brand** (colors, logo, tagline)

The skill does NOT invent prospects' phone numbers or other personal data — it analyzes their public website only. All scores are based on industry benchmarks (Backlinko, Gartner, OpenAI public data) with a `±20%` disclaimer in the footer.

---

## What's analyzed

The audit covers 6 weighted dimensions :

| Dimension | Weight | What's measured |
|---|---|---|
| AI Citability & Visibility | 25% | Citable passages, content structure, AI bot access |
| Brand Authority | 20% | External presence (LinkedIn, press, directories), entity, mentions |
| Content & E-E-A-T | 20% | Expertise, experience, authority, trust, content quality |
| Technical Foundations | 15% | Performance, HTTPS, security headers, mobile, sitemap |
| Structured Data | 10% | JSON-LD present, critical schemas missing |
| Platform Optimization | 10% | Google AIO, ChatGPT, Perplexity, Apple Intelligence, Copilot |

Plus the unique TikupMedia layer :
- Monthly revenue loss calculation (industry-specific formulas)
- Top 3 competitors with traffic estimates
- 12-month ROI projection
- Prioritized action plan (Quick Wins / Medium / Strategic)

---

## Adapts to business type

The skill detects the prospect's business type automatically and adapts the audit :

| Business type | Focus |
|---|---|
| `local_service` | Local Pack + Google Business Profile + Apple Maps |
| `saas` | Comparison pages + Knowledge Graph + entity |
| `ecommerce` | Product schemas + reviews + conversion |
| `agency` | Portfolio + brand authority + case studies |
| `publisher` | E-E-A-T + author credentials + Article schema |
| `personal_brand` | Person schema + sameAs + social proof |
| `restaurant` | Local + reviews + Reservation schema |

---

## White-label customization

Everything is configurable in `config.json` :

- **Identity** : agency name, logo, tagline, founding year, team size
- **Design** : 5 colors palette, fonts, optional sections (5 ready-to-use palettes)
- **What you sell** : services list, price range, billing model, guarantees
- **Audience** : ICP, industries, geographies, pain points addressed
- **Audit tone** : punchy / professional / friendly / urgent — loss vs opportunity framing
- **CTAs** : email, WhatsApp, Calendly, pre-filled email subject and body
- **Sections** : enable/disable competitors, AI disruption block, timeline, etc.

---

## Honesty built-in

1. **Never invents data** : if an analysis returns 0, the audit says "0", not "estimated X"
2. **±20% disclaimer** always present in the HTML footer
3. **Competitors anonymized** if not verifiable via search
4. **Industry-realistic CA calculations** (no inflated numbers)
5. **Real sources cited** in the footer (Backlinko, Gartner, OpenAI public data)
6. **Respects robots.txt** without override

---

## File structure

```
tikupmedia/
├── SKILL.md                   # Claude instructions (the brain)
├── README.md                  # Internal documentation
├── SHARING.md                 # Distribution guide for white-label users
├── LICENSE                    # MIT
├── config.example.json        # Template config (commented)
├── config.json                # Active config (gitignored, user-specific)
├── agents/
│   └── business.md            # Industry-specific revenue loss calculations
├── scripts/
│   └── setup-wizard.md        # Interactive config wizard
└── templates/
    └── audit.html.template    # White-label HTML template
```

---

## Requirements

- [Claude Code](https://claude.com/claude-code) installed
- Anthropic API key configured
- macOS, Linux, or Windows

No external API keys needed by default (uses free signals like Google Suggest, public web data). Optional SerpAPI integration coming soon.

---

## Roadmap

- [ ] PDF export via headless Playwright
- [ ] Multilingual support (EN, DE, ES, IT)
- [ ] Optional SerpAPI integration for exact volumes
- [ ] CRM pipeline (Pipedrive, HubSpot webhooks)
- [ ] Auto-generated commercial proposal after audit
- [ ] Batch mode (audit 10 prospects in one command)
- [ ] Web UI (run audits from a browser, no Claude Code required)
- [ ] Slack / Discord webhooks on audit completion

---

## Contributing

Pull requests welcome. For major changes, please open an issue first to discuss what you would like to change.

For inspiration : check `agents/business.md` for industry benchmarks that could be improved with more accurate ticket data.

---

## License

[MIT](LICENSE) — Use, modify, sell. Just keep the copyright notice.

---

## Author

Built by **[TikupMedia](https://tikupmedia.com)** — French software development studio. 12 in-house developers based in Paris and Toulouse. 150+ products delivered since 2020.

We build mobile apps, SaaS platforms, e-commerce, and AI automations for clients across France, Belgium, Switzerland, Luxembourg, and Canada. No outsourcing, no offshoring.

If `tikupmedia` saves you time, consider :
- ⭐ Starring this repo
- 🐦 Sharing on Twitter / LinkedIn
- 💬 Sending us feedback at [contact@tikupmedia.com](mailto:contact@tikupmedia.com)
- 🚀 Hiring us : [tikupmedia.com](https://tikupmedia.com)

---

<div align="center">

**Made in France 🇫🇷 — Brought to you by [TikupMedia](https://tikupmedia.com)**

[Website](https://tikupmedia.com) · [Blog](https://tikupmedia.com/blog) · [LinkedIn](https://www.linkedin.com/company/tikupmedia/) · [Crunchbase](https://www.crunchbase.com/organization/tikupmedia) · [Wikidata](https://www.wikidata.org/wiki/Q139936672)

</div>

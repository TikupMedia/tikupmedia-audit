# TikupMedia — Commercial SEO+GEO Audit Engine

Skill Claude Code propriétaire qui génère un **audit SEO+GEO commercial complet** sur n'importe quel site prospect en 3 minutes.

Sortie : un fichier HTML auto-suffisant brandable, prêt à envoyer au prospect par mail. Orienté **conversion** — pas score technique froid.

---

## 🚀 Usage

Dans Claude Code, tape :
```
/tikupmedia https://prospect-site.com
```

Ou en langage naturel :
> "Fais un audit commercial pour ce prospect : https://example.com"
> "Audit complet SEO GEO pour pitcher ce client : https://example.com"

---

## 📊 Ce qui est analysé

L'audit couvre 6 dimensions pondérées :

| Dimension | Poids | Ce qui est mesuré |
|---|---|---|
| AI Citability & Visibility | 25% | Passages citables par IA, structure de contenu, autorisations bots IA |
| Brand Authority | 20% | Présence externe (LinkedIn, presse, annuaires), entité, mentions |
| Content & E-E-A-T | 20% | Expertise, expérience, autorité, confiance, qualité rédactionnelle |
| Technical Foundations | 15% | Performance, HTTPS, security headers, mobile, sitemap, robots |
| Structured Data | 10% | JSON-LD présents, schémas critiques manquants |
| Platform Optimization | 10% | Google AIO, ChatGPT, Perplexity, Apple Intelligence, Copilot |

+ Calcul exclusif TikupMedia :
- **CA perdu / mois** (formules par industrie)
- **Top 3 concurrents** qui captent ce trafic
- **ROI projeté** sur 12 mois
- **Plan d'action** Quick Wins / Moyen terme / Stratégique

---

## ⚙️ Workflow (3 min)

| Phase | Durée | Action |
|---|---|---|
| 0 | 30 s | Setup, détection business type |
| 1 | 90 s | 4 agents spécialisés en parallèle (technical / keywords + competitors / content E-E-A-T / brand + schemas) |
| 2 | 60 s | Calcul CA perdu (par industrie) |
| 3 | 30 s | Synthèse → JSON consolidé |
| 4 | 30 s | Génération HTML + ouverture browser |

**Total : ~3 min** pour un audit qui prendrait 45 min manuel.

---

## 📁 Sortie

`~/Downloads/audit-<domain>-<YYYY-MM-DD>.html` avec :

- 🎯 **Cover** : "Vous perdez X€/mois" + 4 KPIs choc
- 📋 **Tableau mots-clés** : 15 keywords + volume + position + CA perdu par mot
- 🏆 **Top 3 concurrents** nommés (ou anonymisés si non trouvés) + leur trafic
- ⚔️ **Comparatif** "votre site vs site moderne 2026"
- 🚨 **Section "Pourquoi ça va empirer en 2027"** (Gartner, OpenAI)
- 📈 **Timeline 12 mois** : trajectoire du score
- 💰 **ROI projeté** : récupération mensuelle + annuelle
- 📞 **CTA brandé** : email + WhatsApp pré-remplis

---

## 🎨 Customisation complète

Édite `~/.claude/skills/tikupmedia/config.json` pour adapter :

### Identité agence
- Nom, logo, tagline, année, taille équipe, pays

### Design (palette en hex)
- 5 couleurs : primary, accent, background, surface, text
- Font family
- Sections optionnelles (concurrents, AI disruption, etc.)
- 5 palettes prêtes à l'emploi (Blood Dark, Emerald Dark, Blue Dark, Purple Dark, Minimal Light)

### Ce que vous vendez
- Offre principale, liste de services
- Fourchette de prix, mode de facturation
- Garanties offertes

### Audience cible
- ICP, industries, géographies, taille équipe
- Pain points adressés

### Ton de l'audit
- Punchy & honnête / Consultant pro / Conseiller chaleureux / Alarme urgente
- Loss framing vs Opportunity framing
- 5 templates de headline au choix

### CTA
- Email, WhatsApp, Calendly, téléphone
- Sujet et body email pré-remplis
- Message d'urgence

Ou utilise le wizard interactif :
```
/tikupmedia setup
```

---

## 🧩 Adaptation par business type

Le skill détecte automatiquement le type et adapte l'audit :

| Business type détecté | Focus particulier |
|---|---|
| `local_service` | Local Pack + Google Business + Apple Maps |
| `saas` | Pages de comparaison + Knowledge Graph + entité |
| `ecommerce` | Product schemas + reviews + conversion |
| `agency` | Portfolio + brand authority + case studies |
| `publisher` | E-E-A-T + auteur + Article schema |
| `personal_brand` | Person + sameAs + social proof |
| `restaurant` | Local + reviews + Reservation schema |

---

## 🛡️ Règles d'honnêteté intégrées

1. **Jamais d'invention** : si un agent renvoie 0, on écrit "0"
2. **Estimations ±20%** : disclaimer présent dans chaque HTML
3. **Concurrents anonymisés** si introuvables (jamais inventés)
4. **CA loss réaliste** : benchmarks `agents/business.md` par industrie
5. **Respect robots.txt** : pas d'override
6. **Sources réelles** citées dans le footer (Backlinko, Gartner, OpenAI public data)

---

## 📁 Structure du skill

```
~/.claude/skills/tikupmedia/
├── SKILL.md                   ← Instructions Claude
├── README.md                  ← Cette doc
├── SHARING.md                 ← Guide distribution / vente
├── LICENSE                    ← MIT
├── config.json                ← Branding actif (gitignored)
├── config.example.json        ← Template
├── agents/
│   └── business.md            ← Calcul CA loss par industrie
├── scripts/
│   └── setup-wizard.md        ← Wizard config interactif
└── templates/
    └── audit.html.template    ← HTML brandable
```

---

## 🔮 Roadmap

- [ ] Version PDF via Playwright headless
- [ ] Support multilingue (EN, DE, ES, IT)
- [ ] Intégration SerpAPI optionnelle pour volumes exacts
- [ ] Pipeline CRM (Pipedrive, HubSpot)
- [ ] Auto-génération de proposition commerciale après audit
- [ ] Mode batch (auditer 10 prospects en une commande)
- [ ] Web UI (lancer un audit depuis le navigateur)
- [ ] Webhooks Slack / Discord à la fin d'un audit
- [ ] Comparison automatique entre 2 prospects

---

## 📜 Licence

MIT — Utilisation libre, commerciale ou non.

---

**Créé par [TikupMedia](https://tikupmedia.com)** — Studio de développement français, 12 développeurs en CDI exclusifs, 150+ produits livrés depuis 2020.

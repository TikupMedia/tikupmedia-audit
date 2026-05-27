---
name: tikupmedia-audit
description: Moteur d'audit SEO+GEO commercial propriétaire TikupMedia. Analyse le site d'un prospect et produit un audit HTML prêt à envoyer, orienté revenus perdus, mots-clés manqués et analyse concurrentielle. Utilise quand l'utilisateur tape `/tikupmedia-audit <url>` ou demande "audit commercial", "audit prospect", "audit pour vente" ou "chauffer un client".
---

# Moteur d'Audit TikupMedia

## Ce que fait ce skill

Génère un **audit SEO+GEO commercial complet** du site d'un prospect et produit un fichier HTML autonome conçu pour **convertir** ce prospect en client.

L'audit couvre :
- SEO technique + Core Web Vitals
- Données structurées Schema.org
- Visibilité IA (Google AIO, ChatGPT, Perplexity, Claude, Copilot, Apple Intelligence)
- Qualité de contenu + score E-E-A-T
- Signaux de brand authority
- Opportunité mots-clés (15 keywords stratégiques avec volume + position)
- Analyse concurrents (top 3 avec trafic estimé)
- **Calcul du CA perdu** (formules par industrie)
- Projection ROI (scénarios 3 mois et 12 mois)
- Plan d'action (Quick Wins / Moyen terme / Stratégique)

Sortie : `~/Downloads/audit-<domaine>-<YYYY-MM-DD>.html` — autonome, brandable, prêt à envoyer par mail.

## Quand l'invoquer

- L'utilisateur a tapé `/tikupmedia-audit <url>`
- L'utilisateur a demandé "audit commercial", "audit prospect", "audit pour vente"
- L'utilisateur veut analyser un concurrent pour de la prospection
- L'utilisateur veut un livrable unique pour un prospect

## Plan d'exécution

### Phase 0 — Setup (30s)

1. Lire `~/.claude/skills/tikupmedia-audit/config.json` pour le branding
2. Extraire le domaine de l'URL d'entrée
3. Créer le workdir : `mkdir -p /tmp/tikupmedia-<domaine>`
4. Récupérer la homepage via WebFetch → sauvegarder dans `/tmp/tikupmedia-<domaine>/homepage.html`
5. Détecter le type de business :
   - `local_service` : téléphone visible, adresse, Maps embed
   - `saas` : Pricing/Sign up, /app, API docs
   - `ecommerce` : produits, panier, prix, Product schema
   - `agency` : portfolio, études de cas, services
   - `restaurant` : menu, horaires, réservation
   - `publisher` : blog, signatures, dates
   - `personal_brand` : nom individuel, portfolio, freelance
   - `other` : par défaut

### Phase 1 — Analyses parallèles (90s)

Lancer **4 agents spécialisés en parallèle** (un appel Agent par agent, tous dans UN SEUL message) :

#### Agent A — Audit technique
- Détection stack (CMS, frameworks)
- Compte Schema.org + types présents
- Security headers (HSTS, X-Content, CSP, etc.)
- Signaux performance (poids page, formats images, lazy-loading)
- Mobile-friendly (viewport, responsive)
- Status HTTP, sitemap, robots.txt, llms.txt
- Crawlabilité + indexabilité
- Bots IA autorisés/bloqués

#### Agent B — Mots-clés + concurrents
- Identifier le service/produit principal du prospect
- Générer 12-15 keywords stratégiques adaptés au type de business :
  - 1 brand keyword
  - 4 services primaires
  - 4 long-tail
  - 3 commercial intent
- Estimer volumes (Google Suggest + connaissance marché)
- Estimer position actuelle (WebSearch pour le domaine du prospect en top 50)
- Identifier top 3 concurrents via WebSearch
- Estimer trafic mensuel concurrents
- Identifier ce que les concurrents font mieux

#### Agent C — Contenu & E-E-A-T
- Présence page About + bio auteur
- Signaux expertise (certifs, années exp, clients nommés)
- Signaux expérience (projets réels, témoignages, photos)
- Autorité (mentions presse, LinkedIn, Wikipedia)
- Trust (mentions légales, SIRET, CGV, contact)
- Profondeur + fraîcheur contenu (blog, année copyright)
- Détecter contenu généré par IA vs humain

#### Agent D — Brand & schemas
- Présence marque sur : LinkedIn, Crunchbase, Trustpilot, Wikipedia, Wikidata, social media
- Mentions presse (WebSearch)
- Schemas actuellement présents
- Schemas critiques manquants (avec JSON-LD prêt à coller généré)
- Signaux sameAs disambiguation entité

Chaque agent écrit son output JSON dans `/tmp/tikupmedia-<domaine>/<agent-name>.json`.

### Phase 2 — Business intelligence (60s)

Lancer l'agent d'analyse business depuis `agents/business.md` avec :
- `BUSINESS_TYPE` de la Phase 0
- `KEYWORDS_DATA` de l'Agent B
- `OUTPUT_DIR`

Cet agent TikupMedia unique calcule :
- **CA perdu mensuel** par keyword en utilisant benchmarks d'industrie
- **CA perdu total / mois + / an**
- **Projections de récupération** (3m / 6m / 12m)
- **Leads/clients perdus par mois**

Output : `business.json`

### Phase 3 — Synthèse (60s)

Lire tous les 5 outputs et consolider dans `synthesis.json`.

### Phase 4 — Génération HTML (30s)

1. Charger le template : `~/.claude/skills/tikupmedia-audit/templates/audit.html.template`
2. Remplacer TOUS les `{{PLACEHOLDER}}` avec les valeurs de `synthesis.json`
3. Générer les lignes du tableau de keywords HTML
4. Générer les cartes concurrents HTML
5. Générer les findings HTML
6. Générer les colonnes du plan d'action HTML
7. Écrire dans `~/Downloads/audit-<domaine>-<YYYY-MM-DD>.html`
8. `open ~/Downloads/audit-<domaine>-<YYYY-MM-DD>.html`

### Phase 5 — Rapport (10s)

Dire à l'utilisateur :
- ✅ Audit complet généré : `~/Downloads/audit-<domaine>.html`
- Score : X/100
- Manque à gagner : Y € / mois
- 3 top findings critiques
- Suggestion : ouvrir le HTML, ajuster les chiffres si besoin, envoyer au prospect

## Adaptation par type de business

| Type de business | Focus dans l'audit |
|---|---|
| `local_service` | Local Pack + Google Business Profile + Apple Maps |
| `saas` | Pages de comparaison + Knowledge Graph + entité |
| `ecommerce` | Product schemas + reviews + abandon de panier |
| `agency` | Portfolio + brand authority + études de cas |
| `publisher` | E-E-A-T + credentials auteur + Article schema |
| `personal_brand` | Person schema + sameAs + preuve sociale |

## Règles importantes

1. **JAMAIS d'invention** : si un agent renvoie 0, écrire "0" pas "estimé X"
2. **Toujours inclure les disclaimers** : bloc `±20% estimates` dans le HTML
3. **Adapter le calcul CA à l'industrie** : utiliser `agents/business.md` benchmarks
4. **Ne pas nommer de concurrents non vérifiables** : utiliser "Concurrent #1 (anonymisé)" si WebSearch échoue
5. **Respecter robots.txt** : jamais override
6. **Brander l'output** : chaque HTML utilise les valeurs de config.json, pas hardcodées
7. **Citer les vraies sources** dans le footer (Backlinko, Gartner, OpenAI public data)

## Personnalisation

Édite `~/.claude/skills/tikupmedia-audit/config.json` pour personnaliser :
- Identité agence (nom, logo, tagline)
- Design (5 couleurs, fonts)
- Ce que tu vends (services, prix, garanties)
- Audience (industries, géographies, ICP)
- Ton de l'audit (punchy / professionnel / chaleureux)
- CTAs (email, WhatsApp, Calendly)

Ou lance le setup wizard :
```
/tikupmedia-audit setup
```

## Structure des fichiers

```
~/.claude/skills/tikupmedia-audit/
├── SKILL.md                   ← Ce fichier (orchestrateur)
├── README.md                  ← Documentation
├── PARTAGE.md                 ← Guide distribution
├── LICENSE                    ← MIT
├── config.json                ← Config active (gitignored)
├── config.example.json        ← Template commenté
├── agents/
│   └── business.md            ← Calcul CA perdu par industrie
├── scripts/
│   └── setup-wizard.md        ← Wizard config interactif
└── templates/
    └── audit.html.template    ← Template HTML brandable
```

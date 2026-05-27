<div align="center">

# tikupmedia-audit

**Générateur d'audits SEO + GEO commerciaux pour Claude Code.**

Produit en 3 minutes un audit HTML brandé prêt à envoyer au prospect — orienté revenus perdus, mots-clés manqués et analyse concurrentielle. Personnalisable agence par agence.

[![License: MIT](https://img.shields.io/badge/Licence-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-7c3aed)](https://claude.com/claude-code)
[![Fait par TikupMedia](https://img.shields.io/badge/Fait%20par-TikupMedia-e8392b)](https://tikupmedia.com)

[Démo](https://tikupmedia.com) · [Documentation](#comment-ça-marche) · [TikupMedia](https://tikupmedia.com)

</div>

---

## Comment ça marche (en 3 étapes)

1. **Tu installes** le skill dans ton Claude Code (5 min, gratuit)
2. **Tu configures** ton branding une seule fois (email, couleurs, ce que tu vends — 10 min)
3. **Tu tapes** `/tikupmedia-audit https://site-prospect.com` → 3 minutes plus tard, un audit HTML brandé avec TES couleurs et TES coordonnées s'ouvre dans ton navigateur, prêt à envoyer au prospect

C'est tout. Pas d'abonnement SaaS, pas de frais récurrents. Le skill tourne sur TON Claude Code, avec TA clé API. Tu possèdes tout ce que tu génères.

---

## Ce que ça produit

Un fichier HTML auto-suffisant avec :

- 🎯 **Hero** : "Vous perdez X €/mois" + 4 KPIs choc
- 📋 **Tableau de 15 mots-clés** avec volume mensuel + position actuelle + CA perdu par mot
- 🏆 **Top 3 concurrents** nommés qui captent ce trafic + leur audience estimée
- ⚔️ **Comparatif** "votre site actuel vs site moderne 2026"
- 🚨 **Section "Pourquoi ça va empirer en 2027"** (Gartner, OpenAI, etc.)
- 📈 **Timeline 12 mois** : trajectoire du score de récupération
- 💰 **ROI projeté** : récupération mensuelle + annuelle
- 📞 **Boutons CTA brandés** : email + WhatsApp pré-remplis

Fichier sauvegardé dans `~/Downloads/audit-<domaine>-<date>.html` — autonome, prêt à attacher en pièce jointe d'email.

---

## Setup (5 min, à faire une fois)

### Étape 1 — Installer le skill

```bash
cd ~/.claude/skills/
git clone https://github.com/TikupMedia/tikupmedia-audit.git
cd tikupmedia-audit
cp config.example.json config.json
```

### Étape 2 — Configurer TON agence (partie importante)

Ouvre `~/.claude/skills/tikupmedia-audit/config.json` dans un éditeur texte et remplis TES informations. Chaque audit utilisera ces valeurs.

#### 🏢 Ton identité (obligatoire)

```json
"agency": {
  "brand_name": "Nom de ton agence",
  "site_url": "https://ton-site.com",
  "logo_url": "https://ton-site.com/ton-logo.png",
  "tagline": "Ce que tu fais, en une phrase",
  "founded_year": 2020,
  "team_size": "5 personnes",
  "country": "France"
}
```

→ `brand_name` apparaît dans le footer de l'audit. `logo_url` doit être un PNG/SVG public (héberge-le sur ton site). `tagline` est affichée quand tu personnalises le HTML.

#### 🎨 Tes couleurs (obligatoire — c'est ce qui rend l'audit À TOI)

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

5 palettes prêtes à l'emploi (copier-coller direct) :

| Palette | primary | background |
|---|---|---|
| **Blood Dark** (défaut) | `#e8392b` | `#0a0a0c` |
| **Emerald Dark** | `#10b981` | `#0a0f0c` |
| **Blue Dark** | `#3b82f6` | `#0a0b14` |
| **Purple Dark** | `#8b5cf6` | `#0d0a14` |
| **Minimal Light** | `#0a0a0c` | `#fafafa` |

→ Ou choisis n'importe quel code hex de ta marque.

#### 📞 Tes coordonnées (OBLIGATOIRE — c'est comme ça que le prospect te contacte)

```json
"cta": {
  "email": "toi@ton-agence.com",
  "whatsapp": "+33612345678",
  "calendly": "https://calendly.com/ton-user/30min",
  "phone": "+33 6 12 34 56 78",
  "primary_button_text": "Programmer un appel · 30 min",
  "secondary_button_text": "WhatsApp",
  "email_subject_template": "Audit pour {{PROSPECT_URL}} — discutons",
  "email_body_template": "Bonjour,\n\nJ'ai bien reçu votre audit qui montre {{LOSS}} de manque à gagner mensuel.\n\nJe souhaite discuter du plan d'action.\n\nMon téléphone : \nMa disponibilité : \n\nMerci."
}
```

→ Quand le prospect clique "Programmer un appel" dans l'audit, un email s'ouvre pré-rempli avec le sujet et le body ci-dessus, adressé à TON email. Le bouton WhatsApp ouvre directement un chat avec TON numéro.

→ **⚠️ Sans ces champs, l'audit n'a aucun moyen de convertir.** Remplis-les toujours.

#### 💼 Ce que tu vends (recommandé — adapte le plan d'action)

```json
"what_you_sell": {
  "primary_offer": "Ce que tu vends principalement (une phrase)",
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
    "Ce que tu promets au client #1",
    "Ce que tu promets au client #2",
    "Ce que tu promets au client #3"
  ]
}
```

→ `billing_model` peut être `fixed_quote`, `monthly_retainer`, `hourly`, `per_project`.
→ `show_in_audit: true` affiche tes prix dans le HTML (les agences transparentes adorent). Défaut `false` te laisse négocier au téléphone.

#### 🎯 Qui tu cibles (aide à adapter le langage)

```json
"who_you_target": {
  "ideal_client_profile": "Décris ton client type en une ligne",
  "industries": ["SaaS", "E-commerce", "Services locaux"],
  "geographies": ["France", "Belgique"],
  "pain_points_addressed": [
    "Problème #1 de tes clients",
    "Problème #2 de tes clients"
  ]
}
```

#### 🗣️ Ton ton

```json
"audit_tone": {
  "style": "punchy_honest"
}
```

Options :
- `punchy_honest` — direct, chiffres choc (recommandé pour vente)
- `consultant_professional` — neutre, factuel
- `friendly_advisor` — chaleureux, conseil
- `urgent_alarm` — FOMO + disruption IA

---

### Étape 3 — (Alternative plus simple) Lance le wizard

Si éditer du JSON manuellement t'effraie, tape dans Claude Code :

```
/tikupmedia-audit setup
```

Le skill te pose 20 questions en français et écrit le config.json pour toi.

---

### Étape 4 — Génère ton premier audit

Dans Claude Code :

```
/tikupmedia-audit https://n-importe-quel-prospect.com
```

Attends 3 minutes. L'HTML s'ouvre dans ton navigateur. Terminé.

Le fichier est sauvegardé dans `~/Downloads/audit-<domaine>-<date>.html`. C'est un seul fichier autonome (zéro image externe, zéro CSS externe) — attache-le simplement à un email et envoie.

---

## Ce qui est analysé

L'audit couvre 6 dimensions pondérées :

| Dimension | Poids | Ce qui est mesuré |
|---|---|---|
| AI Citability & Visibility | 25% | Passages citables par les IA, structure de contenu, accès des bots IA |
| Brand Authority | 20% | Présence externe (LinkedIn, presse, annuaires), entité, mentions |
| Content & E-E-A-T | 20% | Expertise, expérience, autorité, confiance, qualité rédactionnelle |
| Technical Foundations | 15% | Performance, HTTPS, security headers, mobile, sitemap |
| Structured Data | 10% | JSON-LD présents, schémas critiques manquants |
| Platform Optimization | 10% | Google AIO, ChatGPT, Perplexity, Apple Intelligence, Copilot |

Plus la valeur ajoutée TikupMedia :
- Calcul du CA perdu mensuel (formules spécifiques par industrie)
- Top 3 concurrents avec estimations de trafic
- Projection ROI sur 12 mois
- Plan d'action priorisé (Quick Wins / Moyen terme / Stratégique)

---

## S'adapte au type de business

Le skill détecte automatiquement le type d'activité du prospect et adapte l'audit :

| Type détecté | Focus particulier |
|---|---|
| `local_service` | Local Pack + Google Business Profile + Apple Maps |
| `saas` | Pages de comparaison + Knowledge Graph + entité |
| `ecommerce` | Product schemas + reviews + conversion |
| `agency` | Portfolio + brand authority + études de cas |
| `publisher` | E-E-A-T + auteur + Article schema |
| `personal_brand` | Person schema + sameAs + preuve sociale |
| `restaurant` | Local + reviews + Reservation schema |

---

## Ce que tu vends (pour que l'audit convertisse)

L'audit est conçu pour que le prospect pense :
1. *« Wow, cette agence a vraiment analysé mon site en profondeur »*
2. *« Je perds X € chaque mois à cause de ces problèmes »*
3. *« Mes concurrents bouffent mon déjeuner »*
4. *« Je devrais réserver cet appel MAINTENANT »*

Pour que ça marche, ton `config.json` doit dire au skill :
- **Ce que tu fais** (pour que le plan d'action matche tes services)
- **Comment te contacter** (email + WhatsApp + Calendly)
- **Ton branding** (couleurs, logo, tagline)

Le skill n'invente AUCUNE donnée personnelle du prospect — il analyse uniquement son site public. Tous les scores sont basés sur des benchmarks d'industrie (Backlinko, Gartner, OpenAI public data) avec une mention `±20%` dans le footer.

---

## Honnêteté intégrée

1. **Jamais d'invention** : si une analyse renvoie 0, l'audit écrit "0", pas "estimé X"
2. **Disclaimer ±20%** toujours présent dans le footer
3. **Concurrents anonymisés** si non vérifiables via recherche
4. **Calculs CA réalistes** par industrie (pas de chiffres gonflés)
5. **Sources réelles** citées dans le footer
6. **Respecte robots.txt** sans override

---

## Structure des fichiers

```
tikupmedia-audit/
├── SKILL.md                   # Instructions Claude (le cerveau)
├── README.md                  # Documentation publique (ce fichier)
├── PARTAGE.md                 # Guide pour utilisateurs white-label
├── LICENSE                    # MIT
├── config.example.json        # Template config (commenté)
├── config.json                # Config active (gitignored, perso à chaque user)
├── agents/
│   └── business.md            # Calculs CA perdu par industrie
├── scripts/
│   └── setup-wizard.md        # Wizard config interactif
└── templates/
    └── audit.html.template    # Template HTML white-label
```

---

## Prérequis

- [Claude Code](https://claude.com/claude-code) installé
- Clé API Anthropic configurée
- macOS, Linux ou Windows

Pas de clé API externe nécessaire par défaut (utilise des signaux gratuits comme Google Suggest, données web publiques). Intégration SerpAPI optionnelle bientôt.

---

## Roadmap

- [ ] Export PDF via Playwright headless
- [ ] Support multilingue (EN, DE, ES, IT)
- [ ] Intégration SerpAPI optionnelle pour volumes exacts
- [ ] Pipeline CRM (Pipedrive, HubSpot webhooks)
- [ ] Génération automatique de proposition commerciale après audit
- [ ] Mode batch (auditer 10 prospects en une commande)
- [ ] Interface web (lancer des audits depuis un navigateur, sans Claude Code)
- [ ] Webhooks Slack / Discord à la fin d'un audit

---

## Contribuer

Pull requests bienvenues. Pour des changements majeurs, ouvre d'abord une issue pour discuter de ce que tu voudrais changer.

Pour t'inspirer : regarde `agents/business.md` pour les benchmarks d'industrie qui pourraient être améliorés avec des données de tickets plus précises.

---

## Licence

[MIT](LICENSE) — Utilisation libre, commerciale ou non. Garde juste la notice de copyright.

---

## Auteur

Créé par **[TikupMedia](https://tikupmedia.com)** — Studio de développement français. 12 développeurs en CDI exclusifs entre Paris et Toulouse. 150+ produits livrés depuis 2020.

On construit des applications mobiles, plateformes SaaS, sites e-commerce et automatisations IA pour des clients en France, Belgique, Suisse, Luxembourg et Canada. Aucune sous-traitance, aucun offshoring.

Si `tikupmedia-audit` te fait gagner du temps, pense à :
- ⭐ Star ce repo
- 🐦 Partager sur Twitter / LinkedIn
- 💬 Nous envoyer ton feedback à [contact@tikupmedia.com](mailto:contact@tikupmedia.com)
- 🚀 Nous embaucher : [tikupmedia.com](https://tikupmedia.com)

---

<div align="center">

**Made in France 🇫🇷 — Brought to you by [TikupMedia](https://tikupmedia.com)**

[Site](https://tikupmedia.com) · [Blog](https://tikupmedia.com/blog) · [LinkedIn](https://www.linkedin.com/company/tikupmedia/) · [Crunchbase](https://www.crunchbase.com/organization/tikupmedia) · [Wikidata](https://www.wikidata.org/wiki/Q139936672)

</div>

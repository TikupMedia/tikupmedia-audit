# 📦 Guide de partage / vente de tikupmedia

Ce skill est conçu pour être **white-label** (chaque agence configure ses couleurs, son offre, ses CTA). Voici comment le partager ou le vendre.

---

## 🎯 Décisions à prendre avant de partager

### 1. Modèle économique

| Option | Public | Prix recommandé | Effort |
|---|---|---|---|
| **Open-source gratuit** | Communauté dev, audience marketing | 0 € (avec lien vers tes services) | Faible |
| **Freemium** | Acquisition d'agences | Version basique gratuite + version Pro à 49€ | Moyen |
| **Premium B2B** | Agences SEO/dev sérieuses | 99-299 € licence | Élevé |
| **SaaS** | Tout le monde | 29 €/mois récurrent | Très élevé |

### 2. Cible

Tu vends à qui ?

- **Agences SEO indépendantes** (les plus susceptibles d'acheter, ROI rapide pour eux)
- **Freelances marketing/dev** (besoin d'outil pro à petit prix)
- **Studios web** (concurrents directs : leur vendre = bizarre ; mais white-label OK)
- **Consultants vente B2B** (qui veulent un audit pour pitcher)

### 3. Positionnement marketing

| Message | À qui ça parle |
|---|---|
| "Génère un audit en 3 min au lieu de 4h" | Pros pressés |
| "Le seul audit SEO orienté CONVERSION (pas score technique)" | Vendeurs |
| "16 skills SEO spécialisés en 1 commande" | Power users Claude |
| "White-label : ton logo, tes couleurs, ton pitch" | Agences |

---

## 📦 Méthode 1 — GitHub public (open-source)

### Pourquoi
- Acquisition organique via GitHub trending
- Crédibilité tech (vu par devs et CTO)
- Backlinks naturels (le repo est cité = SEO TikupMedia boosté)

### Setup (5 min)

```bash
cd ~/.claude/skills/tikupmedia

# 1. Initialise le repo
git init
git add .
git commit -m "Initial commit: tikupmedia v2"

# 2. Crée le repo GitHub
gh repo create tikupmedia \
  --public \
  --description "Commercial SEO/GEO audit generator for Claude Code. White-label HTML audits in 3 min." \
  --source=. \
  --push

# 3. Ajoute des topics pour la découvrabilité
gh repo edit tikupmedia --add-topic claude-code,seo,geo,audit,sales,white-label,french-agency
```

### Fichiers à ajouter avant push

#### `.gitignore`
```
config.json
*.local
.DS_Store
```
→ ⚠️ **Ignore config.json** : c'est ta config personnelle TikupMedia, ne la partage pas.

#### `LICENSE` (MIT recommandé)
```
MIT License

Copyright (c) 2026 TikupMedia

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

### Promotion (1 fois pushé)

- 🐦 Tweet announce avec demo gif
- 📰 Reddit : r/SEO, r/marketing, r/Claude
- 💼 LinkedIn post personnel + page TikupMedia
- 🎯 ProductHunt launch (le mercredi pour viralité)
- 📰 Soumets sur HackerNews (Show HN)

---

## 💰 Méthode 2 — Vendre sur Gumroad / Lemon Squeezy

### Pourquoi
- Gumroad : 0 € setup, 8.5% commission par vente
- Lemon Squeezy : meilleure TVA EU, 5% + 50¢

### Setup (15 min)

#### 1. Crée le zip de vente

```bash
cd ~/.claude/skills/
# Nettoie d'abord
rm -f tikupmedia/config.json  # ne pas inclure ta config perso

# Crée le ZIP
zip -r tikupmedia-v2.zip tikupmedia/ \
  -x "*.DS_Store" \
  -x "tikupmedia/.git/*" \
  -x "tikupmedia/config.json"

ls -lh tikupmedia-v2.zip
```

#### 2. Crée la page produit

**Titre** : `TikupMedia · L'audit SEO commercial Claude Code`

**Description** :
```
Génère un audit SEO/GEO complet et persuasif en 3 minutes au lieu de 4h.

Pour les agences, freelances et consultants qui veulent chauffer
des prospects avec un livrable visuel impactant — pas un rapport
technique de 50 pages.

✨ Ce qui est inclus :
• Skill Claude Code prêt à l'emploi
• 4 agents spécialisés en parallèle en parallèle
• Calcul du CA perdu mensuel (formule industrie)
• Template HTML auto-suffisant brandable
• Documentation FR + EN
• Setup wizard interactif
• Updates 12 mois inclus

🎯 Personnalisation :
• Logo, couleurs, fonts
• Offre, services, garanties
• Audience cible
• Headlines, CTA, ton de pitch

📊 Sortie :
• HTML autonome (50 KB) prêt à envoyer
• Branding 100% à toi
• Open dans navigateur, imprimable, partageable

💰 Modèle :
• Achat unique : 99 €
• Licence agence (5 users) : 299 €

Prérequis : Claude Code + clé Anthropic API
```

**Galerie d'images** :
- 1 screenshot du HTML généré (le hero)
- 1 screenshot de la config.json personnalisée
- 1 screenshot du tableau mots-clés
- 1 screenshot du timeline

**Prix** :
- Particulier : **99 €**
- Agence (multi-user) : **299 €**
- Lifetime updates : **+50 €**

### 3. Le buyer fait

1. Achète sur Gumroad → reçoit le `.zip`
2. Suit le `README.md` :
   ```bash
   unzip tikupmedia-v2.zip -d ~/.claude/skills/
   ```
3. Lance le wizard :
   ```
   /tikupmedia setup
   ```
4. Génère son premier audit :
   ```
   /tikupmedia https://son-prospect.com
   ```

---

## 🏪 Méthode 3 — Claude Code Plugin (format officiel Anthropic)

### Pourquoi
- Format natif Claude Code (installation 1 clic)
- Sera dans le futur marketplace Anthropic (à venir)
- Crédibilité maximale

### Setup (20 min)

#### 1. Crée le `plugin.json` manifest

```bash
cd ~/.claude/skills/tikupmedia
cat > plugin.json <<'EOF'
{
  "$schema": "https://anthropic.com/schemas/claude-code-plugin-v1.json",
  "name": "tikupmedia",
  "version": "2.0.0",
  "description": "Generate persuasive commercial SEO/GEO audits in 3 minutes. White-label HTML reports brandable per agency. Orchestrates 16 SEO/GEO skills in parallel.",
  "author": {
    "name": "TikupMedia",
    "url": "https://tikupmedia.com",
    "email": "contact@tikupmedia.com"
  },
  "license": "MIT",
  "homepage": "https://tikupmedia.com/tikupmedia",
  "repository": "https://github.com/JamesDmne/tikupmedia",
  "keywords": ["seo", "geo", "audit", "commercial", "sales", "white-label"],
  "skills": [
    "./SKILL.md",
    "./scripts/setup-wizard.md"
  ],
  "agents": [
    "./agents/business.md"
  ],
  "resources": [
    "./templates/audit.html.template",
    "./config.example.json",
    "./README.md"
  ],
  "requires": {
    "claude_code": ">=2.0",
    "skills": []
  }
}
EOF
```

#### 2. Crée le `.plugin` archive

```bash
cd ~/.claude/skills/
zip -r tikupmedia.plugin tikupmedia/ \
  -x "*.DS_Store" \
  -x "tikupmedia/config.json"
```

#### 3. L'utilisateur installe

```
/plugin install /chemin/vers/tikupmedia.plugin
```

Ou si publié sur Anthropic Marketplace :
```
/plugin install tikupmedia/tikupmedia
```

---

## 🎯 Méthode 4 — Cloner-coller direct (le plus simple)

Pour partager rapidement à 1-2 amis sans tout le setup :

```bash
cd ~/.claude/skills/
tar -czf tikupmedia.tar.gz tikupmedia/ --exclude="config.json"

# Envoie le .tar.gz par WeTransfer / AirDrop / Drive
```

L'ami fait :
```bash
cd ~/.claude/skills/
tar -xzf tikupmedia.tar.gz
cp tikupmedia/config.example.json tikupmedia/config.json
# édite config.json avec ses valeurs
```

---

## 📊 Comparatif des méthodes

| Méthode | Setup | Audience | Revenu | Crédibilité |
|---|---|---|---|---|
| GitHub public | 5 min | Devs / SEO | 0 € | ⭐⭐⭐ |
| Gumroad | 15 min | Agences | 99-299 € / vente | ⭐⭐ |
| Plugin officiel | 20 min | Power users Claude | 0 € ou marketplace | ⭐⭐⭐⭐ |
| Zip direct | 1 min | Amis / network | 0 € | ⭐ |

---

## 🚀 Stratégie recommandée pour TikupMedia

Plan en 3 phases :

### Phase 1 — Beta (semaine 1)
1. ✅ Configure ton config.json (déjà fait)
2. ✅ Teste sur 3 prospects réels
3. Donne le `.tar.gz` à 3 collègues du milieu (feedback)

### Phase 2 — Public (semaine 2-3)
1. Push sur GitHub public sous MIT
2. Tweet + LinkedIn post avec démo vidéo
3. Soumets sur Reddit r/SEO, r/marketing_agency
4. Article blog sur tikupmedia.com : *"On vend un audit SEO 99€ en 3 min — voilà comment"*

### Phase 3 — Monétisation (mois 2)
1. Publie sur Gumroad à 99€
2. Promo lancement -50% le premier mois
3. Affiliation : 30% de commission aux agences qui revendent à leurs clients
4. (Optionnel) Convertis en SaaS quand tu as 50+ ventes

---

## 💡 Pourquoi ça peut marcher

- **Niche** : pas d'équivalent direct (audits SEO commerciaux orientés conversion)
- **Distribution** : Claude Code a une audience tech qui paie volontiers les bons outils
- **Format** : skills Claude Code = nouveau format = early-mover advantage
- **Marge** : 100% de marge (zéro coût marginal)
- **Effet boule de neige** : chaque vente = un audit affiché publiquement = pub gratuite pour TikupMedia

---

## ⚠️ Avant de pousser publiquement

Checklist :

- [ ] `config.json` retiré du zip / git (contient ton email + ton WhatsApp perso)
- [ ] Logo TikupMedia retiré du template HTML par défaut (ou mets-le en exemple)
- [ ] README en EN si tu vises international
- [ ] LICENSE MIT ou Apache 2.0
- [ ] Vidéo démo 2 min (Loom ou Screen Studio)
- [ ] Page de vente sur tikupmedia.com/tikupmedia
- [ ] Email de support : support@tikupmedia.com (ou contact@)

Une fois prêt, dis-moi et je te génère :
- Le tweet d'annonce
- Le post LinkedIn
- Le script vidéo démo de 2 min
- La page de vente HTML

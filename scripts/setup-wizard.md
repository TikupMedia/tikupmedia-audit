---
name: tikupmedia-setup
description: Wizard interactif pour personnaliser le skill tikupmedia avant la première utilisation. Pose les questions essentielles et écrit le config.json correspondant.
---

# Setup Wizard — TikupMedia

## Quand l'invoquer

- L'utilisateur tape `/tikupmedia setup` ou `/tikupmedia configure`
- C'est la première fois que l'utilisateur lance tikupmedia (config.json identique au template)
- L'utilisateur demande "personnalise tikupmedia pour moi" ou "configure le skill audit"

## Procédure

Pose les questions ci-dessous **par bloc** (3-5 questions max par message) en utilisant `AskUserQuestion` quand possible. Adapte les options aux réponses précédentes.

### Bloc 1 — Identité agence (CRITIQUE)

1. **Nom de votre agence ?** *(text input)*
2. **URL de votre site ?** *(text input)*
3. **Email pour les CTA d'audit ?** *(text input)*
4. **Tagline en 1 phrase ?** *(text input, suggérer un template)*
5. **Année de création ?** *(text input)*

### Bloc 2 — Ce que vous vendez (CRITIQUE)

6. **Offre principale ?** *(text input — ex: "Refonte SEO + GEO", "Audit + accompagnement 6 mois")*
7. **Fourchette de prix ?** *(options: < 1500€ / 1.5K-5K€ / 5K-25K€ / 25K-80K€ / > 80K€)*
8. **Mode de facturation ?** *(options: Devis fixe / Mensuel récurrent / TJM / Au projet)*
9. **Listez 4-6 services concrets** *(text input, format liste)*
10. **3 garanties que vous offrez** *(text input ou présélection)*

### Bloc 3 — Audience cible

11. **Quel type de clients ciblez-vous ?** *(multi-select : Startups / PME / Grands comptes / Solo founders / Agences)*
12. **Industries que vous servez ?** *(multi-select : SaaS / E-commerce / Local services / Médias / Conseil / Autre)*
13. **Géographies servies ?** *(text input, ex: "France, Belgique, Suisse")*
14. **3 pain points que vos clients ont avant de vous appeler** *(text input)*

### Bloc 4 — Design

15. **Couleur principale de votre marque ?** *(input couleur hex ou choix palette : Rouge sang / Vert émeraude / Bleu profond / Violet / Noir minimal)*
16. **Logo URL (PNG/SVG) ?** *(text input)*
17. **Style audit préféré ?** *(options: Punchy & honnête / Consultant pro / Conseiller chaleureux / Alarme urgente)*

### Bloc 5 — CTA & contact

18. **WhatsApp pour CTA secondaire ?** *(text input, format +33...)*
19. **Calendly URL si vous en avez ?** *(text input, optionnel)*
20. **Headline préféré pour le hero ?** *(options multi):*
    - "Vous perdez {{LOSS}} de chiffre d'affaires chaque mois"
    - "Votre site rate {{CLIENTS}} clients par mois"
    - "Sur 100 recherches, vous récupérez {{PCT}}%"
    - "{{NAME}}, voici les {{LOSS}} que vous laissez à vos concurrents"
    - "Diagnostic urgent : {{SCORE}}/100 — voici comment passer à 85+"

## Action finale

Une fois toutes les réponses collectées, **écrire** le fichier `~/.claude/skills/tikupmedia/config.json` avec toutes les valeurs personnalisées.

Confirmer à l'utilisateur :
- ✅ Configuration sauvegardée
- Résumé des choix clés
- Suggestion : `/tikupmedia https://prospect-test.com` pour tester

## Validation

Avant d'écrire le fichier, vérifier :
- L'email contient `@` et un TLD
- Le site URL commence par `https://`
- La couleur hex est valide (`#xxxxxx`)
- Les prix sont des nombres positifs
- Le logo URL retourne 200 (test rapide via curl)

Si une valeur est invalide → reposer la question avec l'erreur explicite.

## Important

- **Ne pas écraser** le `config.example.json` (c'est le template)
- **Toujours créer** `config.json` (la config active)
- Si un `config.json` existe déjà, demander confirmation avant d'écraser
- Sauvegarder l'ancien en `config.backup-{date}.json`

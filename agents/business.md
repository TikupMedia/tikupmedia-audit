---
name: tikupmedia-business
description: Business model analysis subagent. Determines industry-standard average ticket, conversion rates, and CA calculation parameters for the prospect's business type.
---

# Business Agent — Tikup Audit

## Input
- `BUSINESS_TYPE` : from recon agent
- `MAIN_SERVICE` : from keywords agent
- `GEOGRAPHY` : from keywords agent (FR / EU / global)
- `LANGUAGE` : fr / en
- `OUTPUT_DIR` : `/tmp/tikupmedia-<domain>/`

## Steps

### 1. Determine industry parameters

Based on `MAIN_SERVICE` + `GEOGRAPHY`, pick the right parameters from this lookup (or extrapolate if not listed) :

**LOCAL SERVICE — France**
| Service | Average ticket | Visit→Lead | Lead→Sale |
|---|---|---|---|
| Plombier (dépannage) | 280€ | 4% | 35% |
| Plombier (rénovation) | 1500€ | 3% | 25% |
| Électricien | 250€ | 4% | 30% |
| Serrurier urgence | 220€ | 5% | 40% |
| Restaurant | 35€ | 2% | 60% (réservation) |
| Coiffeur | 65€ | 3% | 50% |
| Dentiste | 180€ | 2.5% | 35% |
| Avocat | 1200€ | 1.5% | 20% |
| Notaire | 800€ | 1% | 25% |
| Garage auto | 450€ | 3.5% | 35% |
| Déménageur | 1200€ | 2.5% | 25% |
| Pressing | 25€ | 2% | 50% |

**SAAS / AGENCY — France**
| Service | Average ticket (1st sale) | Visit→Lead | Lead→Sale |
|---|---|---|---|
| Agence dev web | 8000€ | 1.5% | 15% |
| Agence dev mobile | 25000€ | 1% | 10% |
| Agence SEO | 1500€/mois | 2% | 18% |
| Agence marketing | 2500€/mois | 1.8% | 15% |
| SaaS B2B (LCV) | 1200€/an | 2% | 8% |
| Consultant freelance | 5000€ | 1.2% | 12% |

**E-COMMERCE — France**
| Vertical | Panier moyen | Visit→Sale |
|---|---|---|
| Mode / vêtements | 75€ | 1.8% |
| Beauté / cosmétiques | 55€ | 2.2% |
| Maison / déco | 95€ | 1.5% |
| Sport / outdoor | 110€ | 1.6% |
| Tech / gadgets | 180€ | 1.2% |
| Alimentaire | 45€ | 2.5% |
| Pièces auto/moto | 95€ | 1.8% |

### 2. Calculate per-keyword CA loss

For each keyword from `keywords.json`, compute :
```
CA_loss = visits_lost × (visit_to_lead × lead_to_sale × avg_ticket)
```

For e-commerce (no lead step) :
```
CA_loss = visits_lost × (visit_to_sale × avg_basket)
```

### 3. Total CA loss
Sum across all keywords for the monthly figure. Round to nearest 100€.

### 4. Project recovery scenarios

3 scenarios :
- **Pessimistic (3 months)** : 30% of CA loss recovered (basic SEO fixes)
- **Realistic (6 months)** : 60% of CA loss recovered (SEO + brand authority)
- **Optimistic (12 months)** : 90% of CA loss recovered (full SEO + GEO + content)

## Output

Write to `<OUTPUT_DIR>/business.json` :

```json
{
  "business_type": "local_service",
  "main_service": "plombier",
  "industry_params": {
    "avg_ticket_eur": 280,
    "visit_to_lead_rate": 0.04,
    "lead_to_sale_rate": 0.35,
    "avg_basket_eur": null,
    "visit_to_sale_rate": null,
    "notes": "Standards dépannage plomberie urgence résidentielle Lyon (FFB 2024 + CAPEB 2024)"
  },
  "per_keyword_losses": [
    { "keyword": "plombier lyon", "visits_lost": 3960, "ca_lost_eur": 5940 },
    { "keyword": "plombier urgence lyon", "visits_lost": 1140, "ca_lost_eur": 2280 }
  ],
  "totals": {
    "monthly_ca_lost_eur": 16740,
    "yearly_ca_lost_eur": 200880,
    "potential_interventions_lost": 56
  },
  "recovery_projections": {
    "pessimistic_3m": { "ca_recovered_eur": 5022, "percentage": 30 },
    "realistic_6m":   { "ca_recovered_eur": 10044, "percentage": 60 },
    "optimistic_12m": { "ca_recovered_eur": 15066, "percentage": 90 }
  },
  "ai_search_disruption_2027": {
    "narrative": "Gartner prévoit -50% du trafic Google classique d'ici 2028. ChatGPT déjà 900M utilisateurs/sem. Sur 'plombier urgence Lyon', 2027 = 1 réponse IA citant 1-3 plombiers max.",
    "estimated_additional_loss_2027": 8000
  }
}
```

⚠️ Always add a `notes` field with the source/assumption for the average ticket so the prospect understands it's based on industry benchmarks, not invented numbers.

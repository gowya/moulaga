# Veille finance perso

Ce repo héberge une routine automatisée (Claude Code, cron hebdomadaire — dimanche 20h Paris) qui régénère une page de suivi financier personnel, publiée via GitHub Pages :

👉 **https://gowya.github.io/moulaga/**

## Ce que ça fait

- Suit des seuils de prix sur des lignes PEA (ETF larges ±7 %, actions individuelles ±10 %) et crypto (BTC/ETH en EUR, ±15 %)
- Vérifie mensuellement la valeur des fonds ERES (PER-I Libre / PEI) — pas de seuil, valorisation non quotidienne
- Repère 1-2 instruments financiers "tendance" liés à la diversification hors marchés US
- Résume l'actu macro / sectorielle / crypto de la semaine et le calendrier des prochaines échéances (résultats, BCE, Fed, CPI)

## Ce que ça ne fait PAS

Aucune recommandation d'achat, de vente, de prix d'ordre ou d'allocation. Purement informatif — la décision reste manuelle.

## Pourquoi ce repo est public

Contournement temporaire : au moment de la mise en place, l'app GitHub utilisée par les routines cloud Claude Code n'avait pas d'accès configuré aux repos privés sur ce compte. À repasser en privé si ce point est résolu — voir `CLAUDE.md` pour le contexte complet et les conséquences (Pages nécessite un forfait payant sur repo privé).

## Structure

- `index.html` — page publiée, régénérée chaque semaine (le CSS/gabarit visuel est conservé d'une exécution à l'autre)
- `veille/YYYY-MM-DD.md` — archive datée de chaque relevé
- `last-snapshot.json` — référence pour calculer les variations et la cadence de vérification des fonds ERES
- `robots.txt` + balise `noindex` dans `index.html` — évitent l'indexation par les moteurs de recherche malgré la visibilité publique

Voir `CLAUDE.md` pour les règles précises suivies par l'automatisation à chaque exécution.

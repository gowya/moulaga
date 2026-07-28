# Veille finance perso — règles de l'automatisation

Ce repo est le support d'une routine Claude Code (cloud, cron hebdomadaire dimanche 20h Paris) qui régénère `index.html`. Ce fichier documente la démarche pour qu'elle reste cohérente si la routine est un jour modifiée ou reprise.

## Contrainte non négociable

Ne jamais calculer, suggérer ou recommander un prix d'ordre, une allocation, un achat/vente, ou toute décision d'investissement. Rapporter des faits uniquement (prix, variations, actualités sourcées, dates de calendrier). Jamais de formulation type "tu devrais" / "le bon moment pour" / "je recommande". La décision reste entièrement manuelle, chez l'utilisatrice.

## Portefeuille suivi

- **ETF larges PEA** — seuil ±7 % : Amundi PEA S&P 500 (FR0011871128), Amundi MSCI World (LU1681043599), Amundi Stoxx Europe Select Dividend (LU1812092168)
- **Actions PEA** — seuil ±10 % : Danone (BN), Sanofi (SAN), Stellantis (STLAP/STLA)
- **Crypto** — seuil ±15 %, en EUR directement (BTC/EUR, ETH/EUR via CoinGecko/Kraken ou équivalent — jamais de conversion manuelle depuis l'USD)
- **Fonds ERES** (PER-I Libre / PEI) — vérifiés mensuellement seulement (~28 jours), pas de seuil car valorisation non quotidienne : ERES Sélection Monétaire P (QS0009118421, sur PER-I Libre et PEI), ERES Sélection S&P 500 P (QS0009118918, PEI), ERES Sycomore Europe Eco (QS0009133891, PEI)

## Étapes à chaque exécution

1. Lire `last-snapshot.json` (référence de la semaine précédente)
2. Chercher les prix actuels des ETF/actions (EUR) et crypto (EUR directement)
3. Comparer aux seuils ci-dessus, marquer "SEUIL FRANCHI" si dépassé
4. Repérer 1-2 valeurs tendance liées à la diversification hors marchés US — factuel seulement, jamais une suggestion d'achat
5. Vérifier `eres_last_checked` dans `last-snapshot.json` — ne rechercher les valeurs ERES que si ≥28 jours se sont écoulés ; sinon garder les dernières valeurs affichées avec leur date
6. Chercher l'actu des 7 derniers jours : macro (BCE/Fed, inflation), sectoriel (Sanofi, Danone, Stellantis, S&P 500/MSCI World), crypto
7. Chercher le calendrier des prochaines échéances connues (résultats trimestriels, réunions BCE/Fed, publications CPI)
8. Pour Danone/Sanofi/Stellantis : rapporter les fondamentaux (P/E, croissance du CA, marges, consensus analystes attribué avec cible de prix) — jamais de note de synthèse (voir contrainte non négociable)
9. Pour Danone/Sanofi/Stellantis + BTC/ETH : rapporter les métriques de risque (volatilité historique, bêta rapporté, max drawdown si trouvable) — jamais de note "faible/élevé"
10. Pour Danone/Sanofi/Stellantis + BTC/ETH : rapporter les faits techniques (prix vs moyennes mobiles 50/200j, RSI/MACD avec seuils conventionnels cités comme définitions, niveaux de support/résistance) — jamais de signal Bullish/Bearish
11. Régénérer `index.html` en conservant le CSS et la structure existants — ne remplacer que le contenu des sections (bandeau date, stats, seuils, fondamentaux, risque, technique/charts, fonds ERES, valeur tendance, actualité, calendrier, footer)
12. Écrire l'archive datée `veille/YYYY-MM-DD.md`
13. Mettre à jour `last-snapshot.json` (prix relevés + `eres_last_checked`)
14. Committer et pousser sur `main`, message `Veille hebdo YYYY-MM-DD`

## Historique / décisions

- **28.07.2026** — Repo rendu public : contournement d'un problème d'accès de l'app GitHub pour les routines cloud (aucune installation trouvée donnant accès aux repos privés sur ce compte à l'époque). À repasser en privé si le problème est résolu côté Anthropic — attention, Pages nécessite alors un forfait GitHub payant sur repo privé.
- **28.07.2026** — `robots.txt` + balise `noindex` ajoutés pour limiter l'indexation par les moteurs de recherche malgré la visibilité publique.
- **28.07.2026** — Le tout premier commit avait été fait par erreur avec l'identité git réelle de l'utilisatrice (nom + email personnel) ; les commits suivants utilisent une identité générique (`gowya`). Le premier commit n'a pas été réécrit par défaut (ça demanderait un force-push volontaire).

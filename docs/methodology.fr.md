<p align="right"><a href="methodology.md">English</a></p>

# Méthodologie — Lesotho (2014–2025)

## Données et nettoyage

VIIRS DNB mensuel (VCMSLCFG) et annuel VNL V2, DMSP–VIIRS harmonisé, Black Marble quotidien, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, Banque mondiale. Nettoyage : pixels valides si cf_cvg ≥ 2, unité-mois gardée si ≥ 80 % de pixels observés, pics remplacés, fond et torchères masqués.

## 📈 Cas d'usage 1 — Dynamiques temporelles

- **Question** — L'activité accélère-t-elle ou ralentit-elle, hors effet de saison ?
- **Données** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Méthode** — STL robuste (période 12) sur log(somme des lumières) ; pente de Theil–Sen et test de Mann–Kendall sur les composites annuels ; détection d'anomalies et de ruptures.
- **Validation** — Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (**p-value = 0,0010**)
- **Incertitude** — IC 95 % de la croissance annuelle : +3,3 % à +8,1 %
- **Limites** — Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Cleveland et al. (1990) STL ; Sen (1968) ; Elvidge et al. (2017).
- **Page du tableau de bord** — [`#time`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#time)

**Résultats de cette exécution**

- `F02` Entre 2014 et 2025, la lumière nocturne de Lesotho a évolué de +5,8 % par an (IC 95 % : +3,3 % à +8,1 %). Sur les 12 derniers mois, le niveau désaisonnalisé est +10,2 % par rapport aux 12 mois précédents. (confiance élevée : tendance significative (p < 0,01 ; n = 12))
- `F65` Validation : Significativité de la tendance (Mann–Kendall) et cohérence mensuel/annuel (p-value = 0,0010). Incertitude : IC 95 % de la croissance annuelle : +3,3 % à +8,1 % Limites : Couverture nuageuse et nuits courtes en été ; la lumière n'est pas la valeur ajoutée. Statut : statistique expérimentale ; confiance élevée.

## 🗺️ Cas d'usage 2 — Croissance régionale et convergence

- **Question** — Quelles régions décollent, lesquelles décrochent ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Méthode** — Croissance robuste par unité (Theil–Sen, Mann–Kendall), classes croissance/stagnation/déclin, β- et σ-convergence, indice de Herfindahl.
- **Validation** — Corrélation de rang avec le NO₂ troposphérique (source indépendante) (**Spearman ρ = 0,31**)
- **Incertitude** — Classe attribuée seulement si |pente| ≥ seuil et p < α ; IC de β (erreurs robustes).
- **Limites** — Petites unités : bruit et débordement de lumière (blooming) entre voisins.
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Barro et Sala-i-Martin (1992) convergence ; Henderson, Storeygard et Weil (2012).
- **Page du tableau de bord** — [`#regions`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#regions)

**Résultats de cette exécution**

- `F03` Sur 78 unités ADM2, 55 sont en croissance significative, 19 stagnent et 1 déclinent. L'activité lumineuse reste concentrée : Maseru District concentre 41 % de la lumière nationale. (confiance moyenne : classement sur 78 unités, seuil ±1 %/an et p < 0,10)
- `F04` Entre unités ADM2, la lumière par habitant converge : les unités les moins éclairées rattrapent leur retard. (confiance moyenne : β = −0,046 [−0,056 ; −0,037], n = 65)
- `F24` Maseru District (ADM1, 2025) : part de la lumière nationale 40,7 %, croissance annuelle +4,0 % (IC +1,8 % à +5,5 %, classe Croissance), lumière par habitant 0,230, population 0,03 M, dans le noir 22 %, PIB estimé (expérimental) 0,98 Md USD.
- `F25` Berea District (ADM1, 2025) : part de la lumière nationale 16,7 %, croissance annuelle +6,8 % (IC +3,3 % à +10,8 %, classe Croissance), lumière par habitant 0,152, population 0,02 M, dans le noir 33 %, PIB estimé (expérimental) 0,40 Md USD.

## 💹 Cas d'usage 3 — Relation lumières–PIB

- **Question** — Peut-on estimer la croissance avant sa publication, et le PIB régional ?
- **Données** — VIIRS, PIB réel (Banque mondiale, WDI)
- **Méthode** — log(lumière) ~ log(PIB) en niveaux et en croissance, MCO avec écarts-types HAC ; prévision hors échantillon ; PIB régional = PIB national réparti au prorata de la lumière.
- **Validation** — Suivi hors échantillon de la croissance officielle (**corrélation / EAM (points) = -0,96 / 3,6**)
- **Incertitude** — IC 95 % de l'élasticité : -3,41 à 2,75 ; intervalles de prévision 80 % et 95 %.
- **Limites** — Échantillon annuel court ; le PIB régional est une statistique expérimentale à confronter aux comptes régionaux.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Henderson et al. (2012) AER ; Chen et Nordhaus (2011) PNAS ; Gibson et al. (2021) JDE.
- **Page du tableau de bord** — [`#time`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#time)

**Résultats de cette exécution**

- `F05` L'élasticité de la lumière au PIB réel est de −0,33 en niveaux (IC 95 % : −3,41 à 2,75, R² = 0,00, 12 années) et de −0,19 en taux de croissance (IC : −1,82 à 1,44). Hors échantillon, la croissance des lumières suit celle du PIB avec une corrélation de −0,96 (erreur absolue moyenne : 3,6 point de croissance). (confiance faible : n = 12, non significatif (p = 0,83))
- `F37` Élasticité lumières–PIB réel en niveaux : β = -0,33 (IC 95 % -3,41 à 2,75, R² = 0,00, n = 12, confiance faible : n = 12, non significatif (p = 0,83)). +1 % de PIB ↔ +β % de lumière.
- `F38` Élasticité lumières–PIB réel en taux de croissance : β = -0,19 (IC 95 % -1,82 à 1,44, R² = 0,00, n = 11, confiance faible : n = 11, non significatif (p = 0,82)). +1 % de PIB ↔ +β % de lumière.
- `F39` Élasticité lumières–PIB réel en série longue DMSP–VIIRS : β = 1,55 (IC 95 % 1,14 à 1,97, R² = 0,87, n = 30, confiance élevée : n = 30, p < 0,01, IC étroit). +1 % de PIB ↔ +β % de lumière.

## ⚡ Cas d'usage 4 — Chocs et résilience

- **Question** — Quelle a été la profondeur d'un choc, et la vitesse de récupération ?
- **Données** — VIIRS (monthly), Black Marble VNP46A2 (daily), catalogue d'événements
- **Méthode** — Écart au niveau d'avant-choc sur la série désaisonnalisée ; ruptures structurelles ; indice quotidien Black Marble.
- **Validation** — Le creux dépasse-t-il la variabilité ordinaire ? (**creux (choc principal) = -14,2 % — non**)
- **Incertitude** — Variabilité mensuelle d'avant-choc (écart-type robuste) ; ruptures inexpliquées signalées.
- **Limites** — Les chocs touchant des activités peu éclairées (agriculture, services de jour) sont sous-estimés.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Román et al. (2018) ; Elvidge et al. (2020) lumières et confinements.
- **Page du tableau de bord** — [`#shocks`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#shocks)

**Résultats de cette exécution**

- `F06` Le choc le plus marqué dans la série désaisonnalisée est « COVID-19 » : creux de -14,2 % (12/2020), retour au niveau d'avant-choc après 12 mois. (confiance faible : creux comparé à la variabilité mensuelle d'avant-choc)
- `F41` COVID-19 (2020-03-01 → 2021-06-30) : creux de -14,2 % le 2020-12-01, retour au niveau d'avant-choc après 12 mois. Distinct du bruit : non.
- `F42` Ruptures structurelles : 2017-02-01 (28,8 %); 2018-12-01 (27,3 %); 2022-02-01 (-12,7 %). Sans événement connu à ±6 mois : 3.
- `F43` Régions les plus touchées (creux) : Quthing District -38,4 % (covid19), Berea District -37,8 % (covid19), Maseru District -20,0 % (covid19), Butha-Buthe District -16,2 % (covid19), Mokhotlong District -9,2 % (covid19).

## ⚖️ Cas d'usage 5 — Inégalités et électrification

- **Question** — Où vivent les populations privées d'électricité ?
- **Données** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, accès à l'électricité (WDI)
- **Méthode** — Gini et Theil pondérés par la population ; population des pixels habités sous le seuil de détection ; sensibilité à trois seuils ; IC bootstrap de la variation du Gini.
- **Validation** — Écart avec le taux d'accès à l'électricité de la Banque mondiale (**écart moyen (points) = 11,1**)
- **Incertitude** — Plage selon le seuil de radiance ; IC bootstrap du Gini.
- **Limites** — Proxy de l'éclairage extérieur, pas du raccordement : un foyer raccordé mais peu éclairé paraît « dans le noir ».
- **Statut** — `experimental` · Confiance: moyenne
- **Références** — Theil (1967) ; Falchetta et al. (2020) accès à l'électricité par les lumières.
- **Page du tableau de bord** — [`#inequality`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#inequality)

**Résultats de cette exécution**

- `F07` Le Gini de la lumière par habitant (ADM2) vaut 0,53 en 2025 (baisse significative depuis 2014). Environ 0,03 million(s) de personnes vivent dans des zones habitées sans lumière détectable (39 % de la population habitée). (confiance moyenne : sensible au seuil de radiance (de 0,03 à 0,04 M selon le seuil) ; proxy d'éclairage extérieur, pas de raccordement)
- `F44` Gini de la lumière par habitant (ADM2) : 0,640 en 2014 → 0,532 en 2025 (variation -0,108, IC bootstrap -0,163 à -0,053). Theil T 0,487 ; part entre régions 26 %.
- `F45` Habitants de zones habitées sans lumière détectable : 0,03 M (48 %) en 2014 → 0,03 M (39 %) en 2025. Rapport lumière/hab. urbain/rural 2,3. Proxy de l'accès à l'électricité, sensible au seuil.
- `F46` Écart moyen entre la part de la population en zone éclairée et le taux d'accès à l'électricité de la Banque mondiale : 11,1 points.

## 🏭 Cas d'usage 6 — Zones industrielles

- **Question** — Où est l'industrie, et son activité progresse-t-elle ?
- **Données** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Méthode** — Concordance de six signaux par pixel (≥ 3 dont la lumière), grappes 8-connexes, typologie et confiance.
- **Validation** — Comparaison avec la liste de référence (OpenStreetMap) (**précision / rappel / F1 = 92 % / 22 % / 0,35**)
- **Incertitude** — Confiance par grappe selon le nombre de signaux forts ; sites isolés à vérifier.
- **Limites** — Résolution de Sentinel-5P (≈ 5 km) et MODIS (1 km) : les signaux qualifient un voisinage.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Elvidge et al. (2016) torchères ; Pesaresi et al. (2023) GHSL.
- **Page du tableau de bord** — [`#industry`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#industry)

**Résultats de cette exécution**

- `F08` 12 grappes industrielles détectées par concordance de signaux satellitaires : 3 d'industrie lourde, 2 zones d'activités et de logistique, 2 sites d'hydrocarbures et 5 sites isolés à vérifier. Elles émettent 16,0 % de la lumière nationale (dernière année) ; leur lumière évolue de +1,0 % par an. Maseru District concentre la plus forte activité industrielle. (confiance faible : précision 92 % et rappel 22 % face à la liste de référence)
- `F47` 12 grappes industrielles (≥ 3 signaux sur 6) : Site isolé à vérifier 5, Industrie lourde 3, Hydrocarbures et torchères 2, Zone d'activités et logistique 2. Part de la lumière nationale : 16,0 % ; croissance annuelle +1,0 %. Validation (OpenStreetMap) : précision 92 %, rappel 22 %.
- `F48` IND-001 — Site isolé à vérifier à Maseru (Maseru District) (Maseru District) (20.855 km², 3 signaux, confiance faible); IND-002 — Site isolé à vérifier à Maputsoe (Leribe District) (9.46 km², 3 signaux, confiance faible); IND-004 — Hydrocarbures et torchères à Seate (Mokhotlong District) (4.515 km², 4 signaux, confiance moyenne); IND-003 — Industrie lourde à Mafeteng (Mafeteng District) (5.59 km², 3 signaux, confiance faible); IND-006 — Industrie lourde à Mphokojoana (Mokhotlong District) (2.795 km², 3 signaux, confiance faible); IND-005 — Site isolé à vérifier à Maseru (Maseru District) (Maseru District) (3.01 km², 3 signaux, confiance faible); IND-008 — Site isolé à vérifier à Senekane (Berea District) (1.29 km², 3 signaux, confiance faible); IND-011 — Zone d'activités et logistique à Nqoe (Butha-Buthe District) (0.645 km², 3 signaux, confiance faible); IND-007 — Hydrocarbures et torchères à Metsi-Maholo (Mafeteng District) (1.505 km², 3 signaux, confiance faible); IND-010 — Zone d'activités et logistique à Maseru (Maseru District) (Maseru District) (1.075 km², 3 signaux, confiance faible)
- `F49` Maseru District : 3 grappe(s) industrielle(s), 24,9 km², 25,8 % de la lumière de la région.

## 🏖️ Cas d'usage 7 — Tourisme saisonnier

- **Question** — Quelles zones vivent du tourisme, et comment évolue la saison ?
- **Données** — VIIRS (monthly), nuitées ou arrivées WDI
- **Méthode** — Surcroît estival net des unités comparables de même latitude ; test unilatéral ; indice de saison base 100 ; saisons recoupant le Ramadan signalées.
- **Validation** — Corrélation avec international tourist arrivals (WDI) (**r = 0,87**)
- **Incertitude** — p-valeur par unité ; années 2020–2021 exclues du classement.
- **Limites** — Toute activité estivale (diaspora, résidences secondaires, festivals) est captée, pas seulement le tourisme.
- **Statut** — `experimental` · Confiance: élevée
- **Références** — Analyses saisonnières des lumières et du tourisme, par ex. Hu et al. (2021).
- **Page du tableau de bord** — [`#tourism`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#tourism)

**Résultats de cette exécution**

- `F09` 11 unités sur 77 ont un surcroît de lumière estival net d'au moins 10 % : Ratau (Maseru District), Mafeteng (Mafeteng District), Tayateyaneng (Berea District), Mohale's Hoek (Mohale's Hoek District). Le surcroît net médian atteint +21 % dans la zone la plus touristique. L'indice de saison (base 100 = 2019) tombe à 224 en 2020 et vaut 87 en 2025. (confiance élevée : corrélation de 0,87 avec international tourist arrivals (WDI) (6 années))
- `F57` 11 zone(s) touristique(s) sur 77 unités ADM2 (surcroît estival net ≥ 10 %, mois de pointe [12, 1]) : Ratau (Maseru District) (+21 %, confiance élevée), Mafeteng (Mafeteng District) (+19 %, confiance élevée), Tayateyaneng (Berea District) (+19 %, confiance élevée), Mohale's Hoek (Mohale's Hoek District) (+19 %, confiance élevée), Maseru (Berea Distict) (Berea District) (+18 %, confiance moyenne), Maseru (Maseru District) (Maseru District) (+17 %, confiance élevée), Maputsoe (Leribe District) (+15 %, confiance élevée), Telle (Quthing District) (+14 %, confiance élevée), Leribe (Leribe District) (+11 %, confiance élevée), Mohlakeng (Maseru District) (+10 %, confiance élevée).
- `F58` Indice de saison (base 100 = 2019) : 2014 : -51, 2015 : -23, 2016 : 147, 2017 : 137, 2018 : 81, 2019 : 100, 2020 : 224, 2021 : 81, 2022 : 184, 2023 : 30, 2024 : 230, 2025 : 87. Années avec Ramadan chevauchant la saison : 2021, 2022, 2023, 2024, 2025.
- `F59` Corrélation entre l'indice de saison et international tourist arrivals (WDI) : 0,87 (6 années ; en croissance : 0,84).

## 🏙️ Cas d'usage 8 — Signaux d'urbanisation

- **Question** — Où les villes s'étendent-elles, où les villages s'électrifient-ils, et où la population croît-elle sans lumière ?
- **Données** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, population urbaine (WDI)
- **Méthode** — Surface éclairée (pixels au-dessus du seuil) et population par unité ; croissances de Theil–Sen ; pixels nouvellement éclairés (sombres deux années de suite au début, éclairés deux années de suite à la fin), séparés entre électrification de zones habitées et nouvelles implantations ; typologie lumière/population.
- **Validation** — Corrélation de rang avec la croissance de la surface bâtie GHSL (source indépendante) (**Spearman ρ = 0,25**)
- **Incertitude** — Persistance exigée sur deux années pour limiter le bruit ; marge de ± 1 point entre croissances avant de classer.
- **Limites** — La lumière mesure l'éclairage extérieur, pas l'urbanisation au sens administratif ; le débordement (blooming) élargit les villes ; la population GHSL est interpolée entre époques.
- **Statut** — `experimental` · Confiance: faible
- **Références** — Zhou et al. (2015) étendue urbaine par les lumières ; Pesaresi et al. (2023) GHSL ; Min et al. (2013) électrification des villages.
- **Page du tableau de bord** — [`#urban`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/fr/?country=LSO#urban)

**Résultats de cette exécution**

- `F60` Surface éclairée nationale : +10,9 % par an ; population : +1,2 % par an. Classes (ADM2) : Urbanisation électrifiée 65, Indéterminé 10, Croissance non éclairée 1, Stable ou en déclin 1, Croissance équilibrée 1.
- `F61` Entre 2014 et 2025 : 789 km² nouvellement éclairés, dont 130 km² de zones déjà habitées (électrification, ≈ 7 k habitants) et 659 km² de nouvelles implantations ; 7 km² ont perdu leur lumière.
- `F62` Plus forte extension de la surface éclairée : Ngoajane (Butha-Buthe District) (+234,2 %/an), Thaba-Mokhele (Mohale's Hoek District) (+97,9 %/an), Menoaneng (Mokhotlong District) (+83,5 %/an), Motanasela (Berea District) (+72,5 %/an), Phuthiatsana (Berea District) (+59,0 %/an), Ramapepe (Leribe District) (+53,6 %/an). Croissance non éclairée (population plus rapide que la lumière) : Semonkong (Maseru District).
- `F63` Corrélation de rang (Spearman) entre croissance de la surface éclairée et croissance du bâti GHSL : 0,25 (p = 0,039, 68 unités).

## Limites générales des lumières nocturnes

- **Ce que mesurent les lumières** — Radiance émise vers le haut vers 01 h 30 : l'agriculture, le commerce de jour, les services peu éclairés et l'économie informelle rurale sont mal captés.
- **Saturation et débordement** — DMSP sature au centre des villes (DN 63) et « déborde » (blooming) ; VIIRS est bien meilleur mais le débordement gonfle encore la surface éclairée des villes.
- **Torchères et sites isolés** — Le masque automatique peut retirer des mines, ports ou centrales isolés, et manquer de petites torchères ; les candidats sont exportés pour vérification.
- **Nuages, saisons, lune** — Les mois nuageux sont partiellement observés ; la STL retire la saisonnalité moyenne mais pas une saison anormale (neige, mousson tardive).
- **Ruptures de produit** — DMSP et VIIRS ne sont pas directement comparables : la série longue harmonisée (Li et al., 2020) est un produit modélisé, à lire en tendance seulement.
- **Élasticité NTL–PIB** — Estimée sur 10 à 30 points annuels : intervalles larges, instabilité possible, relation non causale et variable selon le niveau de développement.
- **Accès à l'électricité** — « Habité sans lumière » ≠ « non raccordé » : un foyer raccordé à faible consommation est invisible ; l'indicateur dépend fortement du seuil de radiance et de la population.
- **Limites administratives** — geoBoundaries/GAUL peuvent différer des limites officielles ; les petites unités ADM2 sont sensibles au débordement de la lumière des voisines.
- **Zones industrielles** — La détection repose sur des seuils : une centrale, un port ou un grand centre commercial peut cumuler les signaux ; une usine peu éclairée ou sans émissions visibles échappe à la détection. Sentinel-5P (≈ 5 km) et MODIS (1 km) sont plus grossiers que VIIRS : les signaux NO₂/SO₂/chaleur qualifient un voisinage, pas un bâtiment.
- **Tourisme estival** — Le surcroît estival mesure toute hausse de lumière en été (résidences secondaires, diaspora, fêtes, chantiers), pas seulement le tourisme ; aux hautes latitudes, les nuits d'été très courtes réduisent les observations VIIRS. Le Ramadan modifie l'activité nocturne : les étés concernés sont signalés.
- **Urbanisation** — La surface éclairée dépend du seuil de détection et du débordement de lumière (blooming) autour des villes ; un quartier raccordé mais peu éclairé reste invisible. La population (GHSL/WorldPop) est modélisée à partir des recensements : sa croissance n'est pas une observation indépendante, et les années entre deux millésimes sont interpolées.


---
<sub>Généré par le notebook le 2026-10-30 · version 2.1.0</sub>

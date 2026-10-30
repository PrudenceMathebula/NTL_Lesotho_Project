<p align="right"><a href="methodology.fr.md">Français</a></p>

# Methodology — Lesotho (2014–2025)

## Data and cleaning

VIIRS DNB monthly (VCMSLCFG) and annual VNL V2, harmonised DMSP–VIIRS, daily Black Marble, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, World Bank. Cleaning: pixels valid if cf_cvg ≥ 2, unit-month kept if ≥ 80% of pixels observed, spikes replaced, background and gas flares masked.

## 📈 Use case 1 — Time dynamics

- **Question** — Is activity accelerating or slowing down, net of seasonality?
- **Data** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Method** — Robust STL (period 12) on log(sum of lights); Theil–Sen slope and Mann–Kendall test on annual composites; anomaly and break detection.
- **Validation** — Trend significance (Mann–Kendall) and monthly/annual consistency (**p-value = 0.0010**)
- **Uncertainty** — 95% CI of annual growth: +3.3% to +8.1%
- **Limits** — Cloud cover and short summer nights; light is not value added.
- **Status** — `experimental` · Confidence: high
- **References** — Cleveland et al. (1990) STL; Sen (1968); Elvidge et al. (2017).
- **Dashboard page** — [`#time`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#time)

**Results of this run**

- `F02` Between 2014 and 2025, night-time light in Lesotho changed by +5.8% per year (95% CI: +3.3% to +8.1%). Over the last 12 months, the seasonally adjusted level is +10.2% relative to the previous 12 months. (confidence high: significant trend (p < 0.01; n = 12))
- `F65` Validation: Trend significance (Mann–Kendall) and monthly/annual consistency (p-value = 0.0010). Uncertainty: 95% CI of annual growth: +3.3% to +8.1% Limitations: Cloud cover and short summer nights; light is not value added. Status: experimental statistic; confidence high.

## 🗺️ Use case 2 — Regional growth and convergence

- **Question** — Which regions take off, which fall behind?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Method** — Robust growth per unit (Theil–Sen, Mann–Kendall), growth/stagnation/decline classes, β- and σ-convergence, Herfindahl index.
- **Validation** — Rank correlation with tropospheric NO₂ (independent source) (**Spearman ρ = 0.31**)
- **Uncertainty** — Class assigned only if |slope| ≥ threshold and p < α; CI of β (robust errors).
- **Limits** — Small units: noise and light blooming between neighbours.
- **Status** — `experimental` · Confidence: medium
- **References** — Barro & Sala-i-Martin (1992) convergence; Henderson, Storeygard & Weil (2012).
- **Dashboard page** — [`#regions`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#regions)

**Results of this run**

- `F03` Of 78 ADM2 units, 55 show significant growth, 19 are stagnating and 1 are declining. Light remains concentrated: Maseru District accounts for 41% of national light. (confidence medium: classification of 78 units, threshold ±1%/yr and p < 0.10)
- `F04` Across ADM2 units, light per capita converges: the least-lit units are catching up. (confidence medium: β = −0.046 [−0.056; −0.037], n = 65)
- `F24` Maseru District (ADM1, 2025): share of national light 40.7%, annual growth +4.0% (CI +1.8% to +5.5%, class Growth), light per capita 0.230, population 0.03 M, in the dark 22%, estimated GDP (experimental) 0.98 bn USD.
- `F25` Berea District (ADM1, 2025): share of national light 16.7%, annual growth +6.8% (CI +3.3% to +10.8%, class Growth), light per capita 0.152, population 0.02 M, in the dark 33%, estimated GDP (experimental) 0.40 bn USD.

## 💹 Use case 3 — Light–GDP relationship

- **Question** — Can growth be estimated before its release, and regional GDP?
- **Data** — VIIRS, Real GDP (World Bank, WDI)
- **Method** — log(light) ~ log(GDP) in levels and growth, OLS with HAC errors; out-of-sample nowcast; regional GDP = national GDP allocated pro rata of light.
- **Validation** — Out-of-sample tracking of official growth (**correlation / MAE (pp) = -0.96 / 3.6**)
- **Uncertainty** — 95% CI of the elasticity: -3.41 to 2.75; 80% and 95% prediction intervals.
- **Limits** — Short annual sample; regional GDP is an experimental statistic to be checked against regional accounts.
- **Status** — `experimental` · Confidence: low
- **References** — Henderson et al. (2012) AER; Chen & Nordhaus (2011) PNAS; Gibson et al. (2021) JDE.
- **Dashboard page** — [`#time`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#time)

**Results of this run**

- `F05` The elasticity of light with respect to real GDP is −0.33 in levels (95% CI: −3.41 to 2.75, R² = 0.00, 12 years) and −0.19 in growth rates (CI: −1.82 to 1.44). Out of sample, light growth tracks GDP growth with a correlation of −0.96 (mean absolute error: 3.6 percentage points of growth). (confidence low: n = 12, not significant (p = 0.83))
- `F37` Light–real GDP elasticity in levels: β = -0.33 (95% CI -3.41 to 2.75, R² = 0.00, n = 12, confidence low: n = 12, not significant (p = 0.83)). +1% GDP ↔ +β% light.
- `F38` Light–real GDP elasticity in growth rates: β = -0.19 (95% CI -1.82 to 1.44, R² = 0.00, n = 11, confidence low: n = 11, not significant (p = 0.82)). +1% GDP ↔ +β% light.
- `F39` Light–real GDP elasticity in long DMSP–VIIRS series: β = 1.55 (95% CI 1.14 to 1.97, R² = 0.87, n = 30, confidence high: n = 30, p < 0.01, narrow CI). +1% GDP ↔ +β% light.

## ⚡ Use case 4 — Shocks and resilience

- **Question** — How deep was a shock, and how fast the recovery?
- **Data** — VIIRS (monthly), Black Marble VNP46A2 (daily), event catalogue
- **Method** — Gap to the pre-shock level on the seasonally adjusted series; structural breaks; daily Black Marble index.
- **Validation** — Does the trough exceed ordinary variability? (**trough (main shock) = -14.2% — no**)
- **Uncertainty** — Pre-shock month-to-month variability (robust SD); unexplained breaks flagged.
- **Limits** — Shocks hitting poorly lit activities (agriculture, daytime services) are underestimated.
- **Status** — `experimental` · Confidence: low
- **References** — Román et al. (2018); Elvidge et al. (2020) COVID-19 lockdown lights.
- **Dashboard page** — [`#shocks`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#shocks)

**Results of this run**

- `F06` The most pronounced shock in the seasonally adjusted series is “COVID-19”: trough of -14.2% (12/2020), return to the pre-shock level after 12 months. (confidence low: trough compared with pre-shock month-to-month variability)
- `F41` COVID-19 (2020-03-01 → 2021-06-30): trough of -14.2% on 2020-12-01, back to the pre-shock level after 12 months. Distinguishable from noise: no.
- `F42` Structural breaks: 2017-02-01 (28.8 %); 2018-12-01 (27.3 %); 2022-02-01 (-12.7 %). Without a known event within ±6 months: 3.
- `F43` Hardest-hit regions (trough): Quthing District -38.4 % (covid19), Berea District -37.8 % (covid19), Maseru District -20.0 % (covid19), Butha-Buthe District -16.2 % (covid19), Mokhotlong District -9.2 % (covid19).

## ⚖️ Use case 5 — Inequality and electrification

- **Question** — Where do people without electricity live?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, electricity access (WDI)
- **Method** — Population-weighted Gini and Theil; population of inhabited pixels below the detection threshold; sensitivity to three thresholds; bootstrap CI of the Gini change.
- **Validation** — Gap with the World Bank electricity-access rate (**mean gap (pp) = 11.1**)
- **Uncertainty** — Range across radiance thresholds; bootstrap CI of the Gini.
- **Limits** — Proxy of outdoor lighting, not of connection: a connected but dimly lit household looks “in the dark”.
- **Status** — `experimental` · Confidence: medium
- **References** — Theil (1967); Falchetta et al. (2020) electricity access from lights.
- **Dashboard page** — [`#inequality`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#inequality)

**Results of this run**

- `F07` The Gini coefficient of light per capita (ADM2) is 0.53 in 2025 (significant decrease since 2014). About 0.03 million people live in inhabited areas with no detectable light (39% of the inhabited population). (confidence medium: sensitive to the radiance threshold (from 0.03 to 0.04 M depending on the threshold); a proxy for outdoor lighting, not for grid connection)
- `F44` Gini of light per capita (ADM2): 0.640 in 2014 → 0.532 in 2025 (change -0.108, bootstrap CI -0.163 to -0.053). Theil T 0.487; between-region share 26%.
- `F45` People in inhabited areas without detectable light: 0.03 M (48%) in 2014 → 0.03 M (39%) in 2025. Urban/rural light-per-capita ratio 2.3. Proxy of electricity access, sensitive to the threshold.
- `F46` Average gap between the share of people in lit areas and the World Bank electricity-access rate: 11.1 points.

## 🏭 Use case 6 — Industrial zones

- **Question** — Where is industry, and is its activity growing?
- **Data** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Method** — Concordance of six signals per pixel (≥ 3 including light), 8-connected clusters, typology and confidence.
- **Validation** — Comparison with the reference list (OpenStreetMap) (**precision / recall / F1 = 92% / 22% / 0.35**)
- **Uncertainty** — Per-cluster confidence from the number of strong signals; isolated sites to verify.
- **Limits** — Sentinel-5P (≈ 5 km) and MODIS (1 km) resolution: signals describe a neighbourhood.
- **Status** — `experimental` · Confidence: low
- **References** — Elvidge et al. (2016) gas flares; Pesaresi et al. (2023) GHSL.
- **Dashboard page** — [`#industry`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#industry)

**Results of this run**

- `F08` 12 industrial clusters detected from concordant satellite signals: 3 heavy industry, 2 business parks & logistics, 2 oil & gas sites and 5 isolated sites to verify. They emit 16.0% of national light (latest year); their light changes by +1.0% per year. Maseru District has the most industrial activity. (confidence low: precision 92% and recall 22% against the reference list)
- `F47` 12 industrial clusters (≥ 3 of 6 signals): Isolated site to verify 5, Heavy industry 3, Oil, gas & flares 2, Business park & logistics 2. Share of national light: 16.0%; annual growth +1.0%. Validation (OpenStreetMap): precision 92%, recall 22%.
- `F48` IND-001 — Isolated site to verify in Maseru (Maseru District) (Maseru District) (20.855 km², 3 signals, confidence low); IND-002 — Isolated site to verify in Maputsoe (Leribe District) (9.46 km², 3 signals, confidence low); IND-004 — Oil, gas & flares in Seate (Mokhotlong District) (4.515 km², 4 signals, confidence medium); IND-003 — Heavy industry in Mafeteng (Mafeteng District) (5.59 km², 3 signals, confidence low); IND-006 — Heavy industry in Mphokojoana (Mokhotlong District) (2.795 km², 3 signals, confidence low); IND-005 — Isolated site to verify in Maseru (Maseru District) (Maseru District) (3.01 km², 3 signals, confidence low); IND-008 — Isolated site to verify in Senekane (Berea District) (1.29 km², 3 signals, confidence low); IND-011 — Business park & logistics in Nqoe (Butha-Buthe District) (0.645 km², 3 signals, confidence low); IND-007 — Oil, gas & flares in Metsi-Maholo (Mafeteng District) (1.505 km², 3 signals, confidence low); IND-010 — Business park & logistics in Maseru (Maseru District) (Maseru District) (1.075 km², 3 signals, confidence low)
- `F49` Maseru District: 3 industrial cluster(s), 24.9 km², 25.8% of the region's light.

## 🏖️ Use case 7 — Seasonal tourism

- **Question** — Which areas live from tourism, and how does the season evolve?
- **Data** — VIIRS (monthly), hotel nights or WDI arrivals
- **Method** — Summer excess net of comparable units at the same latitude; one-sided test; season index base 100; seasons overlapping Ramadan flagged.
- **Validation** — Correlation with international tourist arrivals (WDI) (**r = 0.87**)
- **Uncertainty** — p-value per unit; 2020–2021 excluded from the classification.
- **Limits** — Any summer activity (diaspora, second homes, festivals) is captured, not only tourism.
- **Status** — `experimental` · Confidence: high
- **References** — Seasonal light analyses of tourism, e.g. Hu et al. (2021).
- **Dashboard page** — [`#tourism`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#tourism)

**Results of this run**

- `F09` 11 of 77 units show a net summer light excess of at least 10%: Ratau (Maseru District), Mafeteng (Mafeteng District), Tayateyaneng (Berea District), Mohale's Hoek (Mohale's Hoek District). The median net excess reaches +21% in the most touristic zone. The season index (base 100 = 2019) falls to 224 in 2020 and stands at 87 in 2025. (confidence high: correlation of 0.87 with international tourist arrivals (WDI) (6 years))
- `F57` 11 tourist zone(s) out of 77 ADM2 units (net summer excess ≥ 10%, peak months [12, 1]): Ratau (Maseru District) (+21%, confidence high), Mafeteng (Mafeteng District) (+19%, confidence high), Tayateyaneng (Berea District) (+19%, confidence high), Mohale's Hoek (Mohale's Hoek District) (+19%, confidence high), Maseru (Berea Distict) (Berea District) (+18%, confidence medium), Maseru (Maseru District) (Maseru District) (+17%, confidence high), Maputsoe (Leribe District) (+15%, confidence high), Telle (Quthing District) (+14%, confidence high), Leribe (Leribe District) (+11%, confidence high), Mohlakeng (Maseru District) (+10%, confidence high).
- `F58` Season index (base 100 = 2019): 2014: -51, 2015: -23, 2016: 147, 2017: 137, 2018: 81, 2019: 100, 2020: 224, 2021: 81, 2022: 184, 2023: 30, 2024: 230, 2025: 87. Years when Ramadan overlaps the season: 2021, 2022, 2023, 2024, 2025.
- `F59` Correlation between the season index and international tourist arrivals (WDI): 0.87 (6 years; in growth rates: 0.84).

## 🏙️ Use case 8 — Urbanisation signals

- **Question** — Where do cities spread, where do villages get electrified, and where does population grow without light?
- **Data** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, urban population (WDI)
- **Method** — Lit area (pixels above the threshold) and population per unit; Theil–Sen growth rates; newly lit pixels (dark two years in a row at the start, lit two years in a row at the end), split between electrification of inhabited areas and new settlements; light/population typology.
- **Validation** — Rank correlation with GHSL built-up area growth (independent source) (**Spearman ρ = 0.25**)
- **Uncertainty** — Persistence required over two years to limit noise; ± 1 pp margin between growth rates before classifying.
- **Limits** — Light measures outdoor lighting, not urbanisation in the administrative sense; blooming widens cities; GHSL population is interpolated between epochs.
- **Status** — `experimental` · Confidence: low
- **References** — Zhou et al. (2015) urban extent from lights; Pesaresi et al. (2023) GHSL; Min et al. (2013) village electrification.
- **Dashboard page** — [`#urban`](https://PrudenceMathebula.github.io/NTL_Lesotho_Project/?country=LSO#urban)

**Results of this run**

- `F60` National lit area: +10.9% per year; population: +1.2% per year. Classes (ADM2): Electrified urbanisation 65, Undetermined 10, Unlit growth 1, Stable or declining 1, Balanced growth 1.
- `F61` Between 2014 and 2025: 789 km² newly lit, of which 130 km² already inhabited (electrification, ≈ 7k people) and 659 km² of new settlements; 7 km² lost their light.
- `F62` Fastest lit-area expansion: Ngoajane (Butha-Buthe District) (+234.2%/yr), Thaba-Mokhele (Mohale's Hoek District) (+97.9%/yr), Menoaneng (Mokhotlong District) (+83.5%/yr), Motanasela (Berea District) (+72.5%/yr), Phuthiatsana (Berea District) (+59.0%/yr), Ramapepe (Leribe District) (+53.6%/yr). Unlit growth (population faster than light): Semonkong (Maseru District).
- `F63` Spearman rank correlation between lit-area growth and GHSL built-up growth: 0.25 (p = 0.039, 68 units).

## General limits of night-time lights

- **What lights measure** — Upward radiance emitted around 01:30: agriculture, daytime trade, poorly lit services and the rural informal economy are poorly captured.
- **Saturation and blooming** — DMSP saturates in city centres (DN 63) and “blooms” beyond lit areas; VIIRS is much better, but blooming still inflates the lit area of cities.
- **Gas flares and isolated sites** — The automatic mask may remove isolated mines, ports or power plants, and miss small flares; candidates are exported for verification.
- **Clouds, seasons, moon** — Cloudy months are only partially observed; STL removes average seasonality but not an abnormal season (snow, late monsoon).
- **Product breaks** — DMSP and VIIRS are not directly comparable: the harmonised long series (Li et al., 2020) is a modelled product, to be read for trends only.
- **NTL–GDP elasticity** — Estimated on 10 to 30 annual observations: wide intervals, possible instability, a non-causal relationship that varies with the level of development.
- **Access to electricity** — “Inhabited without light” ≠ “not connected”: a connected household with low consumption is invisible; the indicator depends strongly on the radiance threshold and the population data.
- **Administrative boundaries** — geoBoundaries/GAUL may differ from official boundaries; small ADM2 units are sensitive to light spilling over from neighbouring units.
- **Industrial zones** — Detection relies on thresholds: a power plant, a port or a large shopping centre can meet the signals; a dimly lit factory without visible emissions is missed. Sentinel-5P (≈ 5 km) and MODIS (1 km) are coarser than VIIRS: NO₂/SO₂/heat signals describe a neighbourhood, not a building.
- **Summer tourism** — The summer excess captures any rise in summer light (second homes, diaspora visits, festivals, construction), not only tourism; at high latitudes, very short summer nights reduce VIIRS observations. Ramadan changes night-time activity: the summers concerned are flagged.
- **Urbanisation** — The lit area depends on the detection threshold and on light blooming around cities; a connected but dimly lit neighbourhood stays invisible. Population (GHSL/WorldPop) is modelled from censuses: its growth is not an independent observation, and years between two epochs are interpolated.


---
<sub>Generated by the notebook on 2026-10-30 · version 2.1.0</sub>

# Input series

Daily temperature series for the 20 Spanish weather stations used in the paper,
covering **2008-01-01 to 2023-12-31** (5844 days per station, no missing dates).

These are the series **exactly as consumed by the experiment**, with the missing
values imputed as described in Section 4.2 of the paper. From them, the code derives
the 93 recent, 75 historical and 4 calendar variables of each of the 620 supervised
datasets.

## Columns

| Column | Description |
|---|---|
| `date` | Date (YYYY-MM-DD) |
| `tmin` | Daily minimum temperature (°C) |
| `tmax` | Daily maximum temperature (°C) |
| `output` | Daily mean temperature (°C) — **the target variable** |
| `month`, `day`, `year`, `yearday` | Calendar variables, derived from `date` |

`output` is AEMET's own `tmed` measurement, **not** the average of `tmin` and `tmax`
(they differ by 0.02 °C on average). The column keeps the name `output` for
consistency with the analysis code.

## Imputed cells

AEMET provides a record for every day, but for some days the temperature fields are
not reported. In these series those gaps have been **filled by linear interpolation
in time** between the nearest available observations, following Section 4.2 of the
paper. In total **465 cells in 162 rows across 8 of the 20 stations**
were imputed — 0.13 % of all temperature readings.

Because no value is missing, every instance survives the complete-case filter and all
620 supervised datasets have the same size, **4002 instances**. In the non-imputed
version the count ranged from 1889 to 4002, so each station carried a different weight
in the averaged results.

Stations with imputed values: PAMPLONA_AEROPUERTO (55 rows), SEVILLA_AEROPUERTO (27 rows), ALHAMA_DE_MURCIA (23 rows), ALMERIA_AEROPUERTO (22 rows), JAEN (21 rows), SALAMANCA_AEROPUERTO (6 rows), LUGO_AEROPUERTO (5 rows), A_CORUNA (3 rows).

> **Caveat.** Linear interpolation matches the paper's description for one-day gaps,
> but not for long runs. Four runs exceed 5 days — PAMPLONA_AEROPUERTO (28 days in May
> 2015), ALHAMA_DE_MURCIA (10), JAEN (9) and SEVILLA_AEROPUERTO (8) — and are filled
> as a straight ramp, which underestimates their natural variability.

## stations.csv

| File | Paper code | Province | AEMET id | Altitude (m) | Lat | Lon | Imputed rows |
|---|---|---|---|---|---|---|---|
| `ALBACETE.csv` | alb | Albacete | 8178D | 674 | 39.00583 | -1.86278 | 0 |
| `ALMERIA_AEROPUERTO.csv` | alm | Almería | 6325O | 21 | 36.84639 | -2.35694 | 22 |
| `OVIEDO.csv` | ast | Asturias | 1249I | 336 | 43.35333 | -5.87417 | 0 |
| `BADAJOZ.csv` | bad | Badajoz | 4478X | 174 | 38.88611 | -7.00944 | 0 |
| `ARANDA_DE_DUERO.csv` | bur | Burgos | 2117D | 790 | 41.66583 | -3.74278 | 0 |
| `CACERES.csv` | cac | Cáceres | 3469A | 394 | 39.47139 | -6.33889 | 0 |
| `MOLINA_DE_ARAGON.csv` | gua | Guadalajara | 3013 | 1062 | 40.84167 | -1.87889 | 0 |
| `HUELVA_RONDA_ESTE.csv` | hue | Huelva | 4642E | 18 | 37.27833 | -6.91167 | 0 |
| `JAEN.csv` | jae | Jaén | 5270B | 580 | 37.7775 | -3.80917 | 21 |
| `A_CORUNA.csv` | lac | A Coruña | 1387 | 57 | 43.36583 | -8.42139 | 3 |
| `LLEIDA.csv` | ler | Lleida | 9771C | 186 | 41.62611 | 0.59806 | 0 |
| `LUGO_AEROPUERTO.csv` | lug | Lugo | 1505 | 442 | 43.11139 | -7.4575 | 5 |
| `ALHAMA_DE_MURCIA.csv` | mur | Murcia | 7227X | 157 | 37.86167 | -1.33472 | 23 |
| `PAMPLONA_AEROPUERTO.csv` | nav | Navarra | 9263D | 459 | 42.77694 | -1.65 | 55 |
| `SALAMANCA_AEROPUERTO.csv` | sal | Salamanca | 2867 | 790 | 40.95944 | -5.49833 | 6 |
| `SEVILLA_AEROPUERTO.csv` | sev | Sevilla | 5783 | 34 | 37.41667 | -5.87917 | 27 |
| `CALAMOCHA.csv` | ter | Teruel | 9381I | 884 | 40.92611 | -1.29333 | 0 |
| `TOLEDO.csv` | tol | Toledo | 3260B | 513 | 39.88472 | -4.04528 | 0 |
| `VALENCIA.csv` | val | Valencia | 8416 | 11 | 39.48056 | -0.36639 | 0 |
| `ZARAGOZA_AEROPUERTO.csv` | zar | Zaragoza | 9434 | 249 | 41.66056 | -1.00417 | 0 |

Source: AEMET open data portal, <https://opendata.aemet.es/>

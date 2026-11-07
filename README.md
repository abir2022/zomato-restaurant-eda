# Zomato Restaurant EDA — 9,551 restaurants across 15 countries

Exploratory analysis of the Zomato restaurant dataset: where supply concentrates, how ratings behave, and why the rating column is the least trustworthy field in the file.

`Python` · `pandas` · `matplotlib` / `seaborn` · 9,551 rows × 21 columns · two notebooks

---

## The question

A delivery marketplace lives or dies on supply density and rating quality. This analysis asks:

> **Where is restaurant supply concentrated, how is quality distributed — and which parts of this dataset can a decision actually be built on?**

## Headline findings

| # | Finding | Evidence |
|---|---|---|
| 1 | **9,551 restaurants, 21 fields, 9 missing cuisines** | `Cuisines` is the only incomplete column (0.09% null); everything else is complete |
| 2 | **22.5% of listings have no rating at all** | 2,148 restaurants carry `Aggregate rating = 0.0` and `Rating text = Not rated` |
| 3 | **Those unrated listings are almost entirely one country** | 2,139 of the 2,148 sit in India — the missingness is structural, not random |
| 4 | **Ratings cluster in the middle** | Most rated restaurants sit in the 2.5–3.4 band; "Excellent" (4.5+) is rare |
| 5 | **Supply is heavily concentrated** | India dominates the listing count by a wide margin, followed by the US and UK |

Finding 3 is the one worth acting on. If a country's listings are ~22% unrated, an "average rating by country" comparison silently drops its newest or worst-served supply and flatters the result. That is how a dashboard ends up lying while every number in it is technically correct.

## Method

1. **Load and join** — merged `zomato.csv` with `Country-Code.xlsx` to resolve numeric country codes into country names.
2. **Profile** — shape, dtypes, null counts; isolated `Cuisines` as the only incomplete column.
3. **Categorical pass** — country, city and rating-text distributions.
4. **Numeric pass** — aggregate rating and rating-count distributions.
5. **Relationship pass** — rating against rating count, rating against country, and the "not rated" population broken out separately instead of averaged in.

## Charts

Missing-values heatmap, top countries by restaurant count, rating counts by aggregate rating, rating-colour distribution, top cities.

## Files

```
notebooks/01_eda_and_feature_engineering.ipynb   profiling, joins, EDA
notebooks/02_zomato_refined_dataset.ipynb        cleaned / refined dataset
```

The raw `zomato.csv` (~500 MB unzipped on Kaggle) is not committed; the notebooks document every join and derived column.

## Run it

```bash
pip install pandas numpy matplotlib seaborn openpyxl
jupyter notebook notebooks/01_eda_and_feature_engineering.ipynb
```

## Limitations

- Ratings are user-generated and vendor-influenced; nothing in this file can verify them.
- `Average Cost for two` is in each country's local currency, so it is **not** comparable across countries without an FX join — a mistake this dataset invites.
- These are listings, not transactions: nothing here says whether a restaurant is still trading.

## Next

Predict the rating band from city, cuisine and price features — and quantify how much a per-country "best restaurants" ranking changes once unrated listings are excluded.

---

**Md. Abir Ul Islam** · [GitHub](https://github.com/abir2022) · [LinkedIn](https://www.linkedin.com/in/md-abir-ul-islam/)

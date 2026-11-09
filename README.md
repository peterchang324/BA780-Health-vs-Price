# Health vs. Price: How to Be a Smart Grocery Shopper

**BA780 · Cohort B · Team 2 (B02)**

This project uses open product and price data to examine a practical grocery question: **Can shoppers choose healthier food without paying more?** We compare packaged foods by nutrition, processing level, environmental score, brand, and store price. The goal is to give budget-conscious shoppers useful comparisons—not to estimate grocery prices for all U.S. households.

## What we studied

The analysis is organized into five themes:

1. **Know your aisle:** How food group and brand relate to nutrition, and whether aisles with more ultra-processed products tend to have fewer Nutri-Score A/B products.
2. **The greener choice:** Whether lower-impact products are also more nutritious, and how their prices compare within food groups.
3. **Healthy doesn’t cost more:** Whether Nutri-Score A/B products cost more than D/E products per 100 g within the same food group.
4. **What shoppers pay for:** How processing level, nutrients, and organic labels relate to price.
5. **Shop the store, not just the shelf:** How store brands compare with national brands, how the same barcode varies across stores, and whether promotions differ by processing level.

## Main findings

- Within food groups, Nutri-Score A/B products cost about **17% less per 100 g** than D/E products in the observed price sample; no food group showed a statistically significant health premium.
- Store-brand products cost about **42% less per 100 g** than national brands in the same food group. They also had a higher share of Nutri-Score A/B products and a lower share of ultra-processed products in this sample.
- For products found at multiple stores, the median gap between the cheapest and most expensive observed price was about **14%**; for one quarter of products, the gap was **29% or more**.
- Food group matters: comparing products within an aisle is more informative than pooling unrelated foods together.

These are observed associations, not proof that a brand, label, or store causes a price or nutrition difference.

## Data sources

- [Open Food Facts product database](https://huggingface.co/datasets/openfoodfacts/product-database) — product details and nutrition information.
- [Open Prices](https://huggingface.co/datasets/openfoodfacts/open-prices) — crowd-sourced store-price observations.
- [Open Food Facts food-group taxonomy](https://github.com/openfoodfacts/openfoodfacts-server/tree/main/taxonomies) — used to assign consistent food groups.

The notebook’s data pull included about **988,000 product records** and **39,700 price observations**. After requiring a usable food group, package size, and price, the per-100-g food analysis included **5,752 products**. The source data are not stored in this repository; see “Run the notebook” below for the required input files.

## Cleaning and analysis

- Product and price records are matched using barcode, with barcodes kept as text and normalized to preserve leading zeros.
- Placeholder values such as `unknown` are treated as missing, implausible nutrient values are removed, and the official food-group taxonomy is applied.
- Package sizes outside the project’s 20 g–5 kg range are excluded from per-100-g comparisons.
- Price records are limited to USD grocery observations; duplicate price tags and non-grocery entries are removed. Regular prices are used for the main comparisons.
- Prices are expressed per 100 g when package size is available. Most comparisons are made within food groups to reduce differences caused by the mix of products in each aisle.

## Repository contents

- [`B02-Health-Vs-Price-US-Packaged-Groceries.ipynb`](B02-Health-Vs-Price-US-Packaged-Groceries.ipynb) — analysis notebook.
- [`B02-Health-Vs-Price-US-Packaged-Groceries.docx`](B02-Health-Vs-Price-US-Packaged-Groceries.docx) — project report and findings.

## Run the notebook

The notebook is designed for Google Colab and reads the input files from Google Drive. Put these files in:

```text
My Drive/BA780 Team 2/Codebase/input_data/
```

Required files:

```text
off_products_us.csv
off_prices_us.csv
food_groups.json
```

Open the notebook in Colab, connect the Google Drive account that contains the files, and run the cells from top to bottom. The notebook mounts Drive and expects the folder path above. The CSV files are not included in this repository.

## Important limitations

- Open Prices is crowd-sourced. About **85% of location-tagged price observations were from California**, and about **93% were submitted by one contributor**. Results describe this limited sample, not national grocery prices.
- Only about **0.6% of the product catalog** had the information needed for the per-100-g food-group price analysis.
- Package sizes and product categories are incomplete or imperfect; products in the same food group are not always exact substitutes.
- Nutrition and environmental scores are missing for many products, so results may reflect which products are better documented.
- The findings are descriptive comparisons. They do not establish why a product is priced differently or predict what an individual shopper will pay.

## References

- Open Food Facts, [Product database](https://huggingface.co/datasets/openfoodfacts/product-database).
- Open Food Facts, [Open Prices](https://huggingface.co/datasets/openfoodfacts/open-prices).
- Open Food Facts, [Food-group taxonomy](https://github.com/openfoodfacts/openfoodfacts-server/tree/main/taxonomies).

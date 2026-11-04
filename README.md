# goit-rdb-hw-04

Homework 3 (Topic 4): DML, DDL, JOINs, aggregates, set operations and window functions on the Olist Brazilian E-commerce dataset in PostgreSQL 16.

## Dataset

- **Source:** [Olist Brazilian E-commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle, `olistbr/brazilian-ecommerce`), orders from 2016–2018.
- **How it was obtained:** the CSV files were downloaded from Kaggle unchanged and placed in [data/olist/](data/olist/), so the notebook works without Kaggle credentials. If the folder is missing (for example in Colab without cloning the repository), the notebook downloads the same files from the raw copy of this repository on GitHub.
- **Size:** full tables, no sampling.

| Table | File | Rows |
|---|---|---|
| `olist_customers` | `olist_customers_dataset.csv` | 99,441 |
| `olist_orders` | `olist_orders_dataset.csv` | 99,441 |
| `olist_order_items` | `olist_order_items_dataset.csv` | 112,650 |
| `olist_products` | `olist_products_dataset.csv` | 32,951 |
| `olist_sellers` | `olist_sellers_dataset.csv` | 3,095 |
| `olist_order_reviews` | `olist_order_reviews_dataset.csv` | 99,224 |
| `olist_category_translation` | `product_category_name_translation.csv` | 71 |

## Running

[hw04_olist_dml_joins.ipynb](hw04_olist_dml_joins.ipynb) → Restart & Run All in Google Colab. PostgreSQL starts through `pgserver`. Locally: `uv sync`, then the same notebook on the `.venv` kernel.

## What is inside

1. **Raw and typed layers.** `COPY FROM STDIN` into raw tables with `TEXT` columns, then `INSERT ... SELECT` into the typed schema with PKs, FKs, `CHECK`s and `NOT NULL`. Reviews get a technical `review_row_id`.
2. **DML:**
   - `INSERT ... RETURNING` for `seller_alerts`;
   - an idempotent `INSERT ... ON CONFLICT` for `seller_score` at `seller_id × order_id` granularity;
   - `UPDATE ... FROM` for `is_late`;
   - `DELETE ... RETURNING`.
3. **Segments.** `olist_customer_dim` and `customer_segments` at the `customer_unique_id` level.
4. **JOINs.** Six queries covering `INNER`, `LEFT` + `COALESCE`, `FULL OUTER`, `SELF` and the `NOT EXISTS` anti-join.
5. **Aggregates.** Three queries with `GROUP BY`; all three have `HAVING`, one has `STRING_AGG`.
6. **Set operations and windows.** `EXCEPT`, `INTERSECT`, `RANK() OVER` and the reflection.

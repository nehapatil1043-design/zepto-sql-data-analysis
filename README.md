# Zepto Inventory SQL Analysis (PostgreSQL)

SQL analysis of a quick-commerce (Zepto) product inventory dataset. I cleaned the data and wrote 13 SQL queries on pricing, discounts, stock availability and revenue.

## About this project

I followed the guided tutorial by [Amlan Mohanty](https://github.com/amlanmohanty/zepto-SQL-data-analysis-project) (Q1–Q8), then extended it with my **own 5 additional queries (Q9–Q13)** to answer extra business questions about stock-outs, revenue risk and category share.

| Part | Queries | Source |
|------|---------|--------|
| Setup, exploration, cleaning | - | Tutorial |
| Business analysis | Q1–Q8 | Tutorial |
| Additional analysis | **Q9–Q13** | **My own work** |

## Dataset

- Source: [Zepto Inventory Dataset on Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset) (`zepto_v2.csv`)
- 3,732 rows, 9 columns, 14 product categories
- Each row is one SKU (a product in one pack size)

| Column | Meaning |
|--------|---------|
| category | Product category |
| name | Product name |
| mrp | Maximum retail price (in paise, converted to ₹) |
| discountPercent | Discount on MRP |
| discountedSellingPrice | Final price (in paise, converted to ₹) |
| availableQuantity | Units in inventory |
| weightInGms | Weight in grams |
| outOfStock | TRUE / FALSE |
| quantity | Units per package |

## Tools

- PostgreSQL
- pgAdmin (to import the CSV)

## Steps I followed

1. **Create table** with proper data types
2. **Import** `zepto_v2.csv` (saved as CSV UTF-8 to avoid encoding errors)
3. **Explore data**: row count, sample rows, nulls, categories, in-stock vs out-of-stock, duplicate product names
4. **Clean data**: deleted rows with MRP = 0, converted prices from paise to rupees
5. **Analyse** with SQL (below)

## Queries

### From the tutorial (Q1–Q8)

| # | Question |
|---|----------|
| Q1 | Top 10 best-value products by discount % |
| Q2 | High-MRP products (> ₹300) that are out of stock |
| Q3 | Estimated revenue per category |
| Q4 | Products with MRP > ₹500 and discount < 10% |
| Q5 | Top 5 categories by average discount |
| Q6 | Price per gram for products ≥ 100 g |
| Q7 | Group products by weight: Low / Medium / Bulk |
| Q8 | Total inventory weight per category |

### My additions (Q9–Q13)

| # | Question | SQL concepts used |
|---|----------|-------------------|
| Q9 | Out-of-stock rate (%) per category | `CASE WHEN`, `SUM`, `COUNT` |
| Q10 | Number of SKUs and average MRP / selling price per category | `GROUP BY`, `AVG` |
| Q11 | Average rupee saving per unit by category (MRP − selling price) | Calculated column, `AVG` |
| Q12 | Revenue at risk: value of out-of-stock items per category | `WHERE`, `SUM` |
| Q13 | Each category's share of total revenue | Window function `SUM() OVER ()` |

## Some findings (Q9–Q11)

- After cleaning, 3,731 SKUs remain and 453 of them are out of stock.
- **Biscuits** has the highest out-of-stock rate (about 28.6%), followed by Beverages and Dairy, Bread & Batter (about 21.7% each).
- **Meats, Fish & Eggs** gives the biggest average saving per unit (about ₹23), followed by Paan Corner and Personal Care (about ₹17 each).

## Things I noticed

- Prices are stored in paise, so the conversion (`UPDATE ... / 100.0`) must be run **only once**.
- Some out-of-stock rows may have `availableQuantity = 0`, so Q12 uses `quantity` as a proxy for stock value. This is an assumption, not exact revenue.
- Revenue here is *estimated* (price × available quantity). It is not real sales data.

## How to run

1. Install PostgreSQL and pgAdmin
2. Create a database
3. Open `Zepto_SQL_Data_analysis.sql` and run the table creation part
4. Import `zepto_v2.csv` into the `zepto` table (UTF-8 encoding)
5. Run the rest of the script step by step

## Files

```
├── Zepto_SQL_Data_analysis.sql   # all queries
├── zepto_v2.csv                  # dataset
├── README.md
└── LICENSE
```

## Credits and license

- Base project and Q1–Q8: [Amlan Mohanty](https://github.com/amlanmohanty/zepto-SQL-data-analysis-project) (MIT License)
- Q9–Q13 and this README: Neha Jaydip Patil
- Dataset: [Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset)
- Released under the MIT License (see `LICENSE`)

## Contact

Neha Jaydip Patil | Electrical Engineering graduate | Python and data analytics
- GitHub:    - GitHub: https://github.com/nehapatil1043-design
- LinkedIn:  LinkedIn: https://www.linkedin.com/in/your-name

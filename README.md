# Superstore SQL Business Analysis

I used SQL to answer a simple question about a retail business: **where does it make money, and where does it lose it?**

The dataset has about 10,000 order lines from a Superstore-style retail business. I loaded it into SQLite and wrote 7 queries, each answering one business question. The results match my earlier Pandas analysis of the same data ([superstore-sales-analysis](https://github.com/vedant11460/superstore-sales-analysis)), which gave me confidence both are right.

## What I found

- **Overall:** 2.30M in sales and 286K in profit, a 12.5% margin.
- **West and East earn the most.** Profit was West 108K, East 92K, South 47K, Central 40K.
- **Three sub-categories lose money:** Tables (-17.7K), Bookcases (-3.5K), and Supplies (-1.2K).
- **Discounts above 20% turn profit negative.** The average profit per order line was +67 with no discount, +26.5 at 1-20%, -78 at 21-40%, and -107 above 40%.
- **Furniture is the weak category.** It earns only a 2.5% margin and 6.4% of total profit, versus Technology at 17.4% margin and 50.8% of profit.
- **Inside Furniture, Chairs are #1 and Tables are last.** In Technology, Copiers lead.
- **Worst states per region:** Texas and Illinois (Central), Ohio and Pennsylvania (East), North Carolina and Tennessee (South), Colorado and Arizona (West). Texas alone lost about 25.8K.

## The 7 queries

| # | Business question | SQL used |
|---|---|---|
| 1 | What are total sales, profit, and margin? | Aggregates (SUM, COUNT, ROUND) |
| 2 | Which regions earn the most profit? | GROUP BY, ORDER BY |
| 3 | Which sub-categories lose money? | HAVING |
| 4 | How does profit change with discount level? | CASE WHEN |
| 5 | How much does each category contribute to profit? | CTE (WITH) |
| 6 | How do sub-categories rank within their category? | Window function (RANK, PARTITION BY) |
| 7 | Which are the 2 worst states in each region? | CTEs + ROW_NUMBER |

## What I'd recommend

1. Cap discounts at around 20% unless there's a strong reason to go higher.
2. Review pricing and discounts on Tables first.
3. Investigate why Furniture margins are so thin compared with other categories.
4. Look at loss-making states (Texas, Ohio, Pennsylvania) for discount or shipping problems.

## How I built it

1. Cleaned the data in Pandas: removed 17 duplicate rows, treated Postal Code as text, dropped the single-value Country column.
2. Loaded the clean data into a SQLite database (`orders` table).
3. Wrote and ran each query from a Jupyter notebook, with the business question above each one.

## Tools

SQL (SQLite), Python, Pandas, Jupyter Lab

## Files

- `superstore_sql_analysis.ipynb`: all queries with results
- `SampleSuperstore.csv`: the dataset (from Kaggle)

## Limitations

This version of the dataset has no order dates or order IDs, so I couldn't analyze trends over time, customer behavior, or use JOINs. A few rows I removed as duplicates could be genuine repeat purchases.

## Run it yourself

```bash
pip install pandas jupyterlab
jupyter lab
```
Open the notebook and run all cells.

## About me

I'm Vedant Deshmukh, an MCA student in Mumbai interested in data analysis and backend development.
vvedant987@gmail.com | [LinkedIn](https://www.linkedin.com/in/vedant-deshmukh-da/)

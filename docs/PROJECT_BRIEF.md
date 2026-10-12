# NorthHome Sales Analysis — Project Brief

## Business Context

NorthHome is a fictional online homeware retailer serving customers
in the Netherlands, Belgium, and Germany through its website
and a marketplace.

Management needs a one-page dashboard to review sales performance
and delivery reliability for orders placed in 2025.

## Business Questions

- How much did the store sell each month?
- How did monthly sales change compared with the previous month?
- How many valid orders were placed?
- What was the average sales amount per valid order?
- Which product categories generated the most sales?
- What percentage of delivered orders arrived late?

The dashboard should support filtering by country, sales channel,
and product category.

## Data Scope

- Order period: January 1 to December 31, 2025.
- Extraction date: January 15, 2026.
- Currency: EUR.
- Prices exclude VAT and shipping charges.
- Returns and refunds are outside the dataset's scope.
- Some December orders were delivered in January 2026.

All data is synthetic and represents a fictional business.
No real customer or company records are included.

## Source Tables

| File | Intended row level | Intended unique key |
| --- | --- | --- |
| orders.csv | One row per order | order_id |
| order_items.csv | One row per order line | order_id + line_number |
| products.csv | One row per product | product_id |

These are the intended structures. Key uniqueness and data quality
must be verified before modeling.

Column definitions are provided in `data_dictionary.csv`.

## Business Rules

### Sales

- Line sales equal quantity multiplied by unit price,
  adjusted for the line discount.
- Discounts are stored as percentage points:
  a value of 10 means a 10% discount.
- Sales and valid order counts include all statuses
  except Cancelled.
- Sales represent the value of orders placed, rather than
  recognized accounting revenue or cash received.
- Sales are attributed to the order date.

### Order Counts and Average Order Value

- Each valid order must be counted once, regardless
  of its number of order lines.
- Average order value equals sales divided by the
  corresponding valid order count.
- When filtering by product category, sales include only
  the selected category's order lines.
- The corresponding order count includes valid orders
  containing at least one line from the selected category.
- Under that filter, average order value represents selected
  category sales per matching order, rather than the value
  of the entire basket.

### Monthly Comparisons

- Monthly sales are compared with the preceding calendar month.
- Growth is unavailable when the previous month's sales
  are missing or zero.
- The first month in the dataset has no previous-month
  comparison available.

### Delivery Performance

- An order is late when its actual delivery date is later
  than its promised delivery date.
- Delivery on the promised date is considered on time.
- The late delivery rate includes only Delivered orders
  with valid promised and actual delivery dates.
- Delivered orders with missing or invalid delivery dates
  are excluded from this rate and recorded separately
  as data quality issues.
- Delivery is recorded at order level, not order-line level.
- Product category filters select matching orders for
  delivery analysis; each matching order is counted once.

### Optional Gross Profit Analysis

- Unit purchase costs are available for gross profit analysis.
- Gross profit equals sales minus the purchase cost
  of the corresponding units.
- Operating expenses are not included, so net profit
  cannot be calculated from this dataset.

## Data Quality and Validation

Preserve the original CSV files in `data/raw`.

Before modeling, assess:

- Duplicate records and key uniqueness.
- Missing values.
- Data types and date validity.
- Consistency of order status values.
- References between orders, order lines, and products.
- Validity of quantities, prices, discounts, and costs.

Document cleaning decisions and their impact on the data.

Use SQL checks where needed to validate data quality
and reconcile Power BI measures with source records.

## Deliverables

- A one-page Power BI dashboard.
- Documented data preparation and modeling decisions.
- DAX measure definitions.
- SQL validation queries.
- Key findings and analysis limitations.
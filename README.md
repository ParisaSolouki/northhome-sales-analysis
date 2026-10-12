# NorthHome Sales Analysis

An analysis of sales performance and delivery reliability using
Power BI and SQL, based on synthetic e-commerce data from a
fictional homeware retailer.

## Business Objective

Build a one-page dashboard to help management review:

- Monthly sales and month-over-month growth.
- Valid order counts and average order value.
- Sales performance by product category.
- The percentage of delivered orders that arrived late.

The dashboard will support filtering by country, sales channel,
and product category.

## Dataset

The dataset contains orders placed between January 1 and
December 31, 2025, with an extraction date of January 15, 2026.

Some December orders were delivered in January 2026.

All records are synthetic and contain no real customer
or company information.

| Table | Description |
| --- | --- |
| orders | Order dates, statuses, countries, sales channels, and delivery dates |
| order_items | Products ordered, quantities, unit prices, discounts, and unit costs |
| products | Product names and categories |

All monetary values are in EUR and exclude VAT and shipping charges.
Returns and refunds are outside the dataset's scope.

## Tools

- **Power BI:** Power Query, data modeling, DAX, and visualization.
- **MySQL:** Data quality checks and metric validation.
- **VS Code:** SQL files and project documentation.
- **Git and GitHub:** Version control.

## Repository Structure

```text
northhome-sales-analysis/
├── README.md
├── .gitignore
├── data/
│   └── raw/
│       ├── orders.csv
│       ├── order_items.csv
│       └── products.csv
├── docs/
│   ├── PROJECT_BRIEF.md
│   └── data_dictionary.csv
├── sql/
└── powerbi/
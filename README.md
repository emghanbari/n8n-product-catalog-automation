# Product Catalog Automation with n8n and PostgreSQL

This project compares a supplier’s price and stock updates with a product catalog stored in PostgreSQL. It generates an Excel file for review so a reviewer can decide which changes to apply.

## Setup

Import all three workflow JSON files into n8n. Select your PostgreSQL connection in each PostgreSQL node. Use the same database for all three workflows.

## How to run

1. Run `initialize-catalog-public.json` to create the `products` table.
2. Open the form in `supplier-catalog-update-public.json` and upload the current catalog and the supplier update as JSON files. The workflow matches products by ID and generates `catalog_review.xlsx` for price changes, stock changes, or missing stock.
3. Open the spreadsheet and enter `approved` in the `review_decision` column for each change you want to apply. Save the file and upload it through the form in `catalog-review-decisions-public.json`. Only rows marked `approved` update the database. If the supplier omitted the stock value, the workflow uses the old stock value from the review sheet.

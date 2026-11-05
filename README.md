# SQL Data Warehouse Project

A SQL Server-based data warehouse project designed to ingest, transform, and model data from multiple source systems into a modern analytics-ready warehouse. The project follows a medallion-style architecture with bronze, silver, and gold layers and creates a star schema for business reporting and analysis.

## Project Overview

This repository demonstrates a practical end-to-end data warehousing workflow using:

- SQL Server database engineering
- ETL/ELT processing for structured CSV sources
- Layered warehouse design
- Data quality validation
- Dimensional modeling for analytics

The solution loads customer, product, and sales data from CRM and ERP sources and prepares curated datasets for reporting.

## Architecture

The warehouse is built around a `DataWarehouse` database with the following schemas:

- `bronze`: raw landing tables for source data
- `silver`: cleaned and standardized business data
- `gold`: analytical views representing dimensions and facts

This pattern supports traceability, quality checks, and incremental data processing.

## Data Sources

The repository contains source datasets under `datasets/`:

- `datasets/source_crm/`
  - `cust_info.csv`
  - `prd_info.csv`
  - `sales_details.csv`
- `datasets/source_erp/`
  - `CUST_AZ12.csv`
  - `LOC_A101.csv`
  - `PX_CAT_G1V2.csv`

These sources represent customer, product, sales, and location/reference data used to build the warehouse.

## Repository Structure

```text
.
├── datasets/
│   ├── source_crm/
│   └── source_erp/
├── docs/
├── scripts/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   └── init_database.sql
├── tests/
│   ├── quality_checks_gold.sql
│   └── quality_checks_silver.sql
├── LICENSE
├── README.md
└── .gitignore
```

## Scripts

### Database Setup

- `scripts/init_database.sql`
  - Creates the `DataWarehouse` database
  - Creates the `bronze`, `silver`, and `gold` schemas
  - Drops and recreates the database if it already exists

### Bronze Layer

- `scripts/bronze/ddl_bronze.sql`
  - Creates raw landing tables
- `scripts/bronze/proc_load_bronze.sql`
  - Loads source files into the bronze schema

### Silver Layer

- `scripts/silver/ddl_silver.sql`
  - Creates cleaned and modeled silver tables
- `scripts/silver/proc_load_silver.sql`
  - Transforms bronze-layer data into standardized silver-layer records

### Gold Layer

- `scripts/gold/ddl_gold.sql`
  - Creates the analytical gold views for dimensions and fact tables

## Gold Analytics Model

The gold layer includes star-schema style views:

- `gold.dim_customers`
- `gold.dim_products`
- `gold.fact_sales`

This structure supports reporting and dashboarding with a simple and intuitive business model.

## Data Quality Checks

Quality validation scripts are provided to ensure the warehouse remains consistent:

- `tests/quality_checks_silver.sql`
- `tests/quality_checks_gold.sql`

These checks validate:

- duplicate detection
- referential integrity
- business key consistency
- analytical model connectivity

## Typical Workflow

1. Run `scripts/init_database.sql` to create the warehouse database and schemas.
2. Run the bronze scripts to load raw source data.
3. Run the silver scripts to clean and standardize the data.
4. Run the gold DDL script to expose final analytics views.
5. Execute the quality checks to validate the model.

## Prerequisites

- SQL Server instance
- Appropriate permissions to create databases and schemas
- Source CSV files available in the `datasets/` folders

## License

This project is licensed under the Apache License 2.0. See `LICENSE` for details.

## Notes

This project is structured for learning, experimentation, and demonstration of a real-world SQL data warehousing implementation. It is especially useful for understanding layered warehouse patterns, source-to-target transformations, and star schema modeling in SQL Server.

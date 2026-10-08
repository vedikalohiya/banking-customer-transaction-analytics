# Banking Customer Transaction Analytics & Insights

An Azure analytics solution that consolidates customer transaction data from four banking source systems into one platform, using parameterized Azure Data Factory pipelines, ADLS Gen2, Azure Synapse Analytics, and Power BI.

Built as an internship project (MVP) for a banking client.

## Overview

Banking transaction data is spread across multiple systems, which makes it hard to monitor activity or see customer behavior in one place. This project brings four sources into a single Azure platform, models the data for analysis, and exposes it through Power BI dashboards.

**Source systems**

| Source | Type of data |
|---|---|
| Core banking | Account and transaction records |
| Mobile app | Mobile transactions |
| UPI | UPI payments |
| ATM / POS | Card and cash-withdrawal transactions |

> [TODO: add one line on the data format of each source, e.g. CSV, JSON, relational table]

## Architecture

```
Core Banking | Mobile App | UPI | ATM / POS
                    |
                    v
   Azure Data Factory (parameterized pipelines,
        incremental batch ingestion)
                    |
                    v
          ADLS Gen2 (raw / landing zone)
                    |
                    v
   Azure SQL + Cosmos DB  -->  Azure Synapse Analytics
                                (star-schema model)
                    |
                    v
                Power BI dashboards
```

## Tech Stack

| Layer | Tools |
|---|---|
| Orchestration / ingestion | Azure Data Factory |
| Data lake | Azure Data Lake Storage Gen2 |
| Databases | Azure SQL Database (relational), Azure Cosmos DB (NoSQL, document store) |
| Warehouse / modeling | Azure Synapse Analytics, SQL |
| Reporting | Power BI |

## Key Features

- **Parameterized ADF pipelines:** one reusable pipeline design ingests from all four sources instead of one hard-coded pipeline per source.
- **Incremental batch ingestion:** loads new and changed records rather than reloading full datasets.
- **Multi-store integration:** combines relational data (Azure SQL) and document data (Cosmos DB) in Synapse.
- **Star-schema dimensional model:** fact and dimension tables designed for analytical queries.
- **Power BI reporting:** three dashboards covering three channels.



## Dashboards

| Dashboard | Purpose |
|---|---|
| Customer Insights | Spending patterns and customer-level analysis |
| Transaction Monitoring | Transaction volumes, trends, peak hours, and failed-transaction rates |
| Revenue & KPI | Revenue and high-value activity |

The dashboards cover three channels. They were validated on a 100-transaction sample.

## Pipeline Design

1. **Ingest:** parameterized ADF pipelines pull data from each source into ADLS Gen2 on an incremental batch schedule.
2. **Store:** raw data lands in the data lake; relational and document data sit in Azure SQL and Cosmos DB.
3. **Model:** Synapse Analytics combines both stores into a star schema.
4. **Report:** Power BI connects to the modeled data for the dashboards.


## Repository Structure

```
.
|-- README.md
|-- adf/          # exported pipeline, dataset, and linked-service JSON
|-- sql/          # table and star-schema scripts
|-- powerbi/      # report file or screenshots
|-- data/         # sample data only
`-- docs/         # architecture and schema diagrams
```


## Outcome

A unified banking transaction platform that gives the business one place to monitor transaction activity, spot failed transactions, and understand customer behavior across channels.

## Author

**Vedika Lohiya**
[LinkedIn](https://www.linkedin.com/in/vedika2203) | [GitHub](https://github.com/vedikalohiya)

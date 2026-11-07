# CMS Payments and Prescription Analysis

## Project Overview

This project explores the relationship between pharmaceutical industry payments to healthcare providers and their Medicare Part D prescribing patterns in the United States.

We will use Apache Spark (PySpark) to process, join, and analyze large datasets published by the Centers for Medicare & Medicaid Services (CMS).

## Datasets

### 1. CMS Open Payments
Source: https://openpaymentsdata.cms.gov/

Contains information about payments made by pharmaceutical and medical device companies to healthcare providers, including payment amounts, categories, and recipients.

### 2. Medicare Part D Prescribers by Provider and Drug
Source: https://data.cms.gov/provider-summary-by-type-of-service/medicare-part-d-prescribers/medicare-part-d-prescribers-by-provider-and-drug

Contains prescription counts, drug information, and Medicare Part D prescription costs associated with individual providers.

We plan to use 2024 data from both sources.

## Research Goals

- Investigate relationships between industry payments and prescription volumes.
- Explore differences in brand-name drug prescribing.
- Compare payment and prescribing patterns across medical specialties.
- Examine geographic differences in payments and prescriptions.

## Tools

- Python
- Apache Spark / PySpark
- Pandas
- Matplotlib
- GitHub

## Project Status

Initial setup and dataset validation.

The proposed join uses provider identifiers (NPI), subject to verification against the actual downloaded files.

## Team

Team members and responsibilities will be added once finalized.

## Project Timeline

November 2026 – December 16, 2026.
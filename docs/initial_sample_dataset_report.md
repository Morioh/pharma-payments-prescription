# Dataset Schema and Join Plan

**Project:** CMS Payments and Prescription Analysis  
**Status:** Preliminary — API Samples (2024)

## 1. Dataset Schemas and First Five Rows

### Dataset 1: CMS Open Payments

- **Source:** https://openpaymentsdata.cms.gov/
- **Sample size:** 500 payment records
- **Join key:** `covered_recipient_npi`

The complete list of column names, data types, and first five rows is displayed in `notebooks/02_open_payments_inspection.ipynb`.

### Dataset 2: Medicare Part D Prescribers by Provider and Drug

- **Source:** https://data.cms.gov/provider-summary-by-type-of-service/medicare-part-d-prescribers/medicare-part-d-prescribers-by-provider-and-drug
- **Initial sample:** 5 records
- **Targeted sample:** 233 drug records from 15 matching providers
- **Join key:** `Prscrbr_NPI`

The sample contains 22 columns, including:

| Column | Sample Data Type | Description |
|---|---|---|
| `Prscrbr_NPI` | string | Provider identifier |
| `Prscrbr_Last_Org_Name` | string | Provider surname or organization |
| `Prscrbr_First_Name` | string | Provider first name |
| `Prscrbr_City` | string | Provider city |
| `Prscrbr_State_Abrvtn` | string | State abbreviation |
| `Prscrbr_Type` | string | Medical specialty |
| `Brnd_Name` | string | Brand-name drug |
| `Gnrc_Name` | string | Generic drug |
| `Tot_Clms` | string (numeric values) | Total prescription claims |
| `Tot_Drug_Cst` | string (numeric values) | Total drug cost |

The complete 22-column sample schema and first five records are displayed in `notebooks/01_medicare_inspection.ipynb`.

*Note: The API initially returns numeric fields as strings. These are converted to numeric types before aggregation.*

## 2. Join Plan

### Join Keys

- Open Payments: `covered_recipient_npi`
- Medicare Part D: `Prscrbr_NPI`

Both columns identify providers using their National Provider Identifier (NPI).

### Join Relationship

**Before aggregation: Many-to-many**

A provider can have multiple payment records and multiple drug records.

For example, 5 payment records joined to 10 drug records for the same provider would produce 50 rows.

**After aggregation: One-to-one**

Both datasets are grouped by NPI before joining.

Open Payments aggregation:
- `Payment_Records` — Count of payment records
- `Total_Payments` — Sum of payment amounts

Medicare Part D aggregation:
- `Drug_Records` — Count of provider-drug records
- `Total_Claims` — Sum of prescription claims
- `Total_Drug_Cost` — Sum of drug costs

After aggregation, each dataset contains one row per NPI. We then perform an inner join on NPI.

### Initial Join Validation Results

| Metric | Result |
|---|---:|
| NPIs tested | 20 |
| Matching NPIs | 15 |
| Medicare drug records retrieved | 233 |
| Final aggregated joined rows | 15 |

The matching demonstrates that NPI can be used to join the datasets.

**Note:** These results use limited API samples. Final schemas, record counts, and join statistics will be updated using the complete datasets.
# Data-Engineering-Case-Study-Referral-System-ETL-Fraud-Logic
## Referral Program Data Pipeline

A complete end-to-end data processing pipeline that loads, profiles, cleans, enriches, validates, and reports on data from a Referral Program system.
This pipeline is production-ready and designed to run both locally and in Docker.

## Features:
This pipeline performs the following operations:

# 1. Data Loading

Loads CSV files:
- lead_log.csv
- paid_transactions.csv
- referral_rewards.csv
- user_logs.csv
- user_referral_logs.csv
- user_referral_statuses.csv
- user_referrals.csv

# 2. Data Profiling

Generates per-column statistics:
- Null counts
- Null percentage
- Distinct values count
- Data types

# Produces:
output/data_profiling_report.csv

# 3. Data Cleaning

Handles:
- Datatype conversions
- Timestamp conversion to local time
- String normalization
- Missing value handling
- Timezone merging

# 4. Feature Engineering & Enrichment

Adds:
- Source category
- Referrer details (name, phone, homeclub)
- Reward details
- Transaction details
- Local timestamps
- Standardized naming formats

# 5. Business Logic Validation

Detects valid vs invalid referral records based on:
- Membership status
- Referral status
- Reward eligibility
- Transaction timing
- Account deletions

# 6. Final Report Generation

Produces a complete, deduplicated referral table.

# Outputs:
output/final_referral_report.csv



Assignment/
│
├── your_script2.py              # Main pipeline script
├── lead_log.csv
├── paid_transactions.csv
├── referral_rewards.csv
├── user_logs.csv
├── user_referral_logs.csv
├── user_referral_statuses.csv
├── user_referrals.csv
│
├── Dockerfile
├── requirements.txt
├── README.md (this file)
│
└── output/
      ├── data_profiling_report.csv
      └── final_referral_report.csv


### To run in Docker

Run from inside your project folder:
type: docker build --no-cache -t referral-app .

Mount the current directory so the container can access CSVs and write outputs:
type: docker run --rm \
  -e BASE_PATH="/app" \
  -e OUTPUT_DIR="/app/output" \
  -v "$(pwd):/app" \
  referral-app

After a successful run, you should expect:

======================================================================
PIPELINE SUMMARY
======================================================================
Total records processed: 46
Valid referrals: 35
Invalid referrals: 11
======================================================================

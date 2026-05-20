# DPDP Governance Framework for Databricks

Automated discovery, classification, approval, and tagging of Personal Data (PD) and Sensitive Personal Data (SPD) in Databricks Unity Catalog to support compliance with the Digital Personal Data Protection (DPDP) Act.

---

## Overview

This solution scans Unity Catalog metadata, identifies potential Personal Data and Sensitive Personal Data columns using AI-assisted classification and rule-based detection, stores scan results in governance tables, and automatically applies Unity Catalog tags after approval.

### Key Capabilities

- Automated metadata discovery
- Personal Data identification
- Sensitive Personal Data identification
- AI-assisted classification
- Rule-based pattern matching
- Exclusion management
- Auto approval workflow
- Unity Catalog column tagging
- Incremental metadata scanning
- Audit trail and scan history
- Configurable governance repository

---

## Repository Structure

```text
dpdp-governance/
│
├── databricks.yml
├── README.md
│
└── dab/
    │
    ├── resources/
    │   └── scan_update_metadata.job.yml
    │
    └── src/
        │
        ├── create_datagov_objects.sql
        └── m1-sensitive_column_classification_and_tagging.sql
```

---

## Solution Flow

```text
Unity Catalog Metadata
          │
          ▼
Information Schema Scan
          │
          ▼
Classification Engine
(AI + Rules)
          │
          ▼
Governance Metadata Tables
          │
          ▼
Approval Workflow
          │
          ▼
Unity Catalog Tags
          │
          ▼
Compliance Reporting
```

---

## Incremental Scan Strategy

To avoid rescanning unchanged metadata, a column fingerprint is generated:

```sql
md5(
    concat(
        table_catalog,
        '_',
        table_schema,
        '_',
        table_name,
        '_',
        column_name,
        '_',
        data_type
    )
) AS column_hash
```

Columns are rescanned only when metadata changes.

## Future Enhancements

- Approval UI
- Lakebase-backed configuration management
- Automated compliance dashboards
- Data lineage integration
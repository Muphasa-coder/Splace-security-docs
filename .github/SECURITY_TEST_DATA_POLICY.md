
# Security Test Data Policy

- Production data shall never be copied into test or dev environments unless fully anonymized and approved.
- Acceptable test data sources:
  - Synthetic data generation
  - Anonymized export with irreversible masking
- Storage: test DBs must be encrypted; secrets (API keys, db passwords) stored in org secret manager.
- Access: least privilege; logs redacted for PII.
- Refresh: test data rotated every X days (org policy).
- Exceptions: must be approved by Security and documented in the PR.


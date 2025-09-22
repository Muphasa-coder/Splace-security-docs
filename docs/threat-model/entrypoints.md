# Entry Points

| Entry Point             | Method/Protocol | Authentication | Notes |
|-------------------------|-----------------|----------------|-------|
| `/login`                | HTTPS/POST      | Yes            | Main user login portal |
| `/api/v1/*`             | HTTPS/REST      | Token-based    | Public API endpoints   |
| `/admin`                | HTTPS/GET       | Yes (RBAC)     | Admin-only portal      |
| Database Connection     | TCP (3306)      | Password       | Restricted to backend  |


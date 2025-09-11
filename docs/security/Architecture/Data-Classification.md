
# Data Classification

> Scheme: Public / Internal / Confidential / Regulated (e.g., PCI, KYC).  
> Rule of thumb: choose the highest applicable level for each data item.

| Data Item               | Example                          | Classification       | Systems / Stores             | Retention       | Encryption (At Rest / In Transit) | Access Policy     | Notes (e.g., PCI scope)                  |
|-------------------------|----------------------------------|----------------------|------------------------------|------------------|------------------------------------|-------------------|------------------------------------------|
| User profile (name, email, phone) | "Adaeze, ada@example.com" | Confidential         | User DB, Core                | 7 years          | Yes / TLS                         | Need-to-know      | Used for onboarding, personalization     |
| Password hashes         | bcrypt hash                     | Confidential         | User DB, Auth                | While account active | Yes / TLS                     | Restricted         | Never log                                |
| Auth tokens / session IDs | JWT, session cookie           | Confidential         | Cache, Auth                  | Short TTL        | Yes / TLS                         | Restricted         | Rotate + revoke                          |
| Session metadata        | IP, device, browser             | Internal             | Logs, Cache                  | 30 days          | Yes / TLS                         | Need-to-know      | Used for fraud detection                 |
| Payment card data (PAN, expiry) | 4111 1111 1111 1111       | Regulated (PCI)      | (Ideally vendor only)        | Not stored       | N/A / TLS                         | N/A                | Avoid storing; use tokens                |
| Escrow transaction data | amount, status, timestamps      | Regulated            | PaymentDB, Core              | 7 years          | Yes / TLS                         | Finance/Admin      | PCI scope                                |
| Bank account numbers    | NUBAN/IBAN                      | Confidential         | Core, Vendor                 | 7 years          | Yes / TLS                         | Restricted         | Tokenize if possible                     |
| KYC IDs & documents     | NIN/BVN, passport scan          | Regulated            | Blob, Core, KYC Vendor       | Per policy       | Yes / TLS                         | Restricted         | Sensitive identity data                  |
| Verification results    | KYC status, match score         | Regulated            | KYC Vendor, Core             | Per policy       | Yes / TLS                         | Compliance Team    | Identity validation                      |
| Address                 | Street/city/state               | Confidential         | User DB                      | 7 years          | Yes / TLS                         | Need-to-know      | Used for shipping, KYC                   |
| File uploads            | profile photo, ID scan          | Confidential         | Object Storage               | Per policy       | Yes / TLS                         | Restricted         | Private buckets                          |
| Order data              | Items, amounts                  | Internal             | Order DB                     | 7 years          | Yes / TLS                         | Role-based         | Includes cart, delivery, payment status  |
| Reviews & ratings       | stars, comments                 | Public               | ReviewDB                     | Until deleted    | Optional / TLS                    | Public             | Visible to all users                     |
| Chat messages           | buyer-seller conversation       | Internal             | MessageDB                    | 1 year           | Yes / TLS                         | MessagingService   | May contain informal PII                 |
| Email events            | bounces, opens                  | Internal             | Logs, Email Vendor           | 2 years          | Yes / TLS                         | Need-to-know      | No PII in URLs                           |
| Logs & traces           | request IDs, metrics            | Internal             | Logs/SIEM                    | 30–90 days       | Yes / TLS                         | Need-to-know      | Scrub PII                                |
| API usage logs          | endpoint hits, latency          | Internal             | Logs/SIEM                    | 90 days          | Yes / TLS                         | DevOps             | No PII; used for performance monitoring  |
| Analytics events        | page_view                       | Internal             | Analytics Vendor             | 2 years          | Vendor / TLS                      | Need-to-know      | No PII                                   |
| Public content          | marketing pages                 | Public               | CDN                          | Indefinite       | N/A                               | Public             | Static assets                            |
| Secrets & keys          | API keys, KMS keys              | Confidential         | Secrets Manager              | Per policy       | Encrypted / TLS                   | Least privilege    | Never commit                             |

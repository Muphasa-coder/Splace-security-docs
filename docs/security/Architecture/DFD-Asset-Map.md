# 🔗 DFD ↔ Asset Inventory Mapping

This document links each node in the DFD diagram to its corresponding entry in the Asset Inventory. It ensures traceability across architecture, data flow, and system components.

| DFD Node         | Asset Name in Inventory             | Type         | Notes |
|------------------|--------------------------------------|--------------|-------|
| `U`              | —                                    | External     | End users initiating flows |
| `Browser`        | Frontend (SPA/SSR), FrontendClient   | Service      | Web interface |
| `Mobile`         | FrontendClient                       | Service      | Mobile app |
| `CDN`            | CDN/WAF                              | Service      | Edge delivery and protection |
| `APIGW`          | API Gateway                          | Service      | Routing, rate limiting, auth |
| `FE`             | Frontend (SPA/SSR), FrontendClient   | Service      | UI layer |
| `Auth`           | Auth Service, AuthService            | Service      | Login, session, token issuance |
| `Core`           | Core Service, CoreService            | Service      | Business logic, orchestration |
| `Order`          | Order Service, OrderService          | Service      | Cart, checkout, order tracking |
| `MQ`             | Message Queue, MessageQueue          | Queue        | Event-driven communication |
| `Cache`          | Cache (Redis)                        | Cache        | Session and token storage |
| `UserDB`         | User DB, UserDB                      | DB           | Stores PII and profiles |
| `OrderDB`        | Order DB, OrderDB                    | DB           | Order history and payments |
| `Logs`           | Logs / SIEM, AuditLogs, ErrorLogs    | Log          | Monitoring, compliance, debugging |
| `Blob`           | Object Storage                       | DB           | File uploads, KYC documents |
| `Secrets`        | Secrets Manager / KMS                | Secret       | API keys, encryption keys |
| `Pay`            | Payment Provider, StripeAPI, PaystackAPI | Vendor | PCI scope, webhook integration |
| `Email`          | Email Service                        | Vendor       | OTP, transactional emails |
| `KYC`            | KYC/Identity Provider                | Vendor       | Identity verification |
| `Analytics`      | Analytics                            | Vendor       | Event tracking, dashboards |
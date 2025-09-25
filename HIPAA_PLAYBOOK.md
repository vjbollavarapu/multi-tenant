# HEALS Multi-Tenant HIPAA Playbook

## Architecture: Row-Based Multi-Tenancy with HIPAA Alignment

### Database Strategy

* **Row-based tenancy**: All tenants share the same database and schema.
* **Tenant isolation**: Each row is tagged with a `tenant_id`. All queries enforce tenant scoping through middleware or ORM filters.
* **Encryption**: Data encrypted at rest (AES-256) and in transit (TLS 1.2+).
* **Audit trail**: Every read/write logged with user, tenant, and timestamp.

---

## Ongoing HIPAA Compliance Checklist

### Administrative Safeguards

* [ ] Security Management Process (risk analysis, mitigation)
* [ ] Workforce Training & Sanctions Policy
* [ ] Information Access Management
* [ ] Incident Response Plan

### Technical Safeguards

* [ ] Access Control (RBAC per tenant)
* [ ] Automatic Logoff for idle sessions
* [ ] Encryption (at rest + in transit)
* [ ] Audit Controls (logs, monitoring)
* [ ] Integrity Controls (hashing / checksums)

### Physical Safeguards

* [ ] Secure hosting (SOC 2, ISO 27001 datacenters)
* [ ] Disaster Recovery & Backups
* [ ] Device & Media Controls

### Monitoring & Auditing

* [ ] Log retention (minimum 6 years)
* [ ] Breach Notification policy
* [ ] Periodic Security Testing

---

## HIPAA Safeguard → Architecture Control Mapping Table

| HIPAA Requirement     | Architecture Control                  |
| --------------------- | ------------------------------------- |
| Access Control        | Row-level RBAC, JWT/OAuth2 auth       |
| Audit Controls        | Centralized logging, query monitoring |
| Integrity             | Checksums + ORM transaction handling  |
| Transmission Security | TLS 1.2+ enforced                     |
| Storage Security      | AES-256 at rest                       |
| Workforce Training    | Access provisioning + revocation logs |
| Contingency Plan      | Automated backups + DR site           |

---

## Sample Auditor Q&A Script

**Q1. How do you ensure tenant data is isolated in a shared database?**
*A1. Every record is tagged with a tenant_id. All queries pass through a middleware layer that enforces tenant scoping automatically. We also run automated tests to validate row-level isolation.*

**Q2. What encryption methods are you using?**
*A2. Data is encrypted in transit using TLS 1.2+ and at rest with AES-256. Keys are rotated regularly using our cloud KMS.*

**Q3. How do you detect unauthorized access?**
*A3. We maintain detailed audit logs of all access events, integrate with SIEM for anomaly detection, and enforce alerts for unusual access patterns.*

**Q4. How do you handle backups while ensuring compliance?**
*A4. Backups are encrypted, tenant data is scoped by `tenant_id`, and access to backups is strictly controlled. We regularly test restoration as part of disaster recovery drills.*

**Q5. How do you prove compliance with HIPAA’s minimum necessary standard?**
*A5. Role-based access control ensures users only access the data required for their role. Access is reviewed quarterly.*

**Q6. What is your incident response procedure?**
*A6. We have a documented incident response plan, including notification timelines, forensic analysis, and corrective action tracking.*

---

✅ With this playbook, your team has:

* Technical architecture documented.
* Ongoing compliance checklist.
* Mapping table for auditors.
* Prepared Q&A responses for audit readiness.

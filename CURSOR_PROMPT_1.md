# ⚡ Prompt Set for Cursor.AI – Multi-Tenant HEALS Development

## 1. **Architecture & Tenancy Layer**

* *Prompt:*

  ```
  Design a multi-tenant data access layer for Django/FastAPI that supports both row-based and schema-based tenancy. 
  Use PostgreSQL as the database. 
  Include middleware, query filters, and role-based access enforcement. 
  Show best practices for healthcare applications with compliance in mind.
  ```

* *Purpose:* Ensures generated code starts with the right **tenant-aware foundation**.

---

## 2. **Row-Based Tenant Filtering**

* *Prompt:*

  ```
  Modify the following model/query to ensure tenant_id filtering is always applied.
  Add a base model that enforces tenant_id automatically.
  Include Row-Level Security (RLS) policies in PostgreSQL for additional safety.
  ```

* *Purpose:* Cursor generates **consistent tenant filtering**, avoiding human error.

---

## 3. **Schema Migration Scripts**

* *Prompt:*

  ```
  Write a Django/FastAPI migration script that consolidates tenant data from multiple schemas 
  into a single shared schema with a tenant_id column. 
  Preserve foreign key relationships and indexes.
  ```

* *Purpose:* For when you switch from schema-based to row-based.

---

## 4. **Middleware & Request Context**

* *Prompt:*

  ```
  Implement middleware that extracts the tenant_id from request headers or JWT claims. 
  Pass tenant_id into the request context so all queries automatically filter by it. 
  Ensure this integrates with both Django ORM and SQLAlchemy.
  ```

* *Purpose:* Automates **tenant awareness per request**.

---

## 5. **Hybrid Model Support**

* *Prompt:*

  ```
  Implement a hybrid tenancy manager where small tenants use row-based storage, 
  and enterprise tenants use schema-based storage. 
  Write a configuration file that maps tenant IDs to tenancy mode, 
  and make the data access layer resolve dynamically.
  ```

* *Purpose:* Lets Cursor generate the **dual-mode flexibility** we discussed.

---

## 6. **Compliance & Security**

* *Prompt:*

  ```
  Add audit logging for all tenant-specific database operations. 
  Store tenant_id, user_id, operation, and timestamp. 
  Provide a query API to fetch audit trails per tenant for compliance.
  ```

* *Purpose:* Helps with **HIPAA/GDPR-like requirements**.

---

## 7. **Performance & Scaling**

* *Prompt:*

  ```
  Optimize queries for a large multi-tenant row-based system. 
  Add indexes on tenant_id and common lookup fields. 
  Suggest caching strategies for per-tenant dashboards. 
  Provide an example Redis caching layer integrated with FastAPI/Django.
  ```

* *Purpose:* Keeps HEALS scalable even as tenants grow.

---

## 8. **Testing & Validation**

* *Prompt:*

  ```
  Generate unit tests and integration tests to ensure tenant isolation. 
  Include tests where tenant A should never see tenant B’s data. 
  Add load tests simulating 10,000 tenants with 1,000 records each.
  ```

* *Purpose:* Ensures **safety + performance validation**.

---

## 9. **DevOps / Deployment**

* *Prompt:*

  ```
  Write a Kubernetes deployment strategy for a multi-tenant Django/FastAPI app. 
  Ensure database migrations, schema creation, and row-level policies 
  can run automatically during deployment. 
  Suggest monitoring tools for tenant-level performance tracking.
  ```

* *Purpose:* Guides Cursor to produce **production-ready infra code**.

---

## 10. **Refactoring Helper**

* *Prompt:*

  ```
  Refactor this code to remove schema-based logic and replace it with row-based logic. 
  Ensure all queries reference tenant_id. 
  Update models, serializers, and views accordingly.
  ```

* *Purpose:* Helps during **migration from django-tenants → row-based**.

---

✅ With these prompt sets, you can **systematically guide Cursor.AI** at every stage:

* Designing → Migrating → Securing → Scaling → Deploying.

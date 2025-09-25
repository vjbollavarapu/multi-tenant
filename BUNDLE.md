# 🧩 Cursor.AI Tenancy Prompt Library

*For HEALS ERP – Multi-Tenant Development (Django / FastAPI)*

This playbook contains ready-to-use prompts for **Cursor.AI** to help accelerate multi-tenant app development. Use them as building blocks while coding, refactoring, or scaling.

---

## 1. Architecture & Tenancy Layer

```
Design a multi-tenant data access layer for Django/FastAPI that supports both row-based and schema-based tenancy. 
Use PostgreSQL as the database. 
Include middleware, query filters, and role-based access enforcement. 
Show best practices for healthcare applications with compliance in mind.
```

---

## 2. Row-Based Tenant Filtering

```
Modify the following model/query to ensure tenant_id filtering is always applied.
Add a base model that enforces tenant_id automatically.
Include Row-Level Security (RLS) policies in PostgreSQL for additional safety.
```

---

## 3. Schema Migration Scripts

```
Write a Django/FastAPI migration script that consolidates tenant data from multiple schemas 
into a single shared schema with a tenant_id column. 
Preserve foreign key relationships and indexes.
```

---

## 4. Middleware & Request Context

```
Implement middleware that extracts the tenant_id from request headers or JWT claims. 
Pass tenant_id into the request context so all queries automatically filter by it. 
Ensure this integrates with both Django ORM and SQLAlchemy.
```

---

## 5. Hybrid Model Support

```
Implement a hybrid tenancy manager where small tenants use row-based storage, 
and enterprise tenants use schema-based storage. 
Write a configuration file that maps tenant IDs to tenancy mode, 
and make the data access layer resolve dynamically.
```

---

## 6. Compliance & Security

```
Add audit logging for all tenant-specific database operations. 
Store tenant_id, user_id, operation, and timestamp. 
Provide a query API to fetch audit trails per tenant for compliance.
```

---

## 7. Performance & Scaling

```
Optimize queries for a large multi-tenant row-based system. 
Add indexes on tenant_id and common lookup fields. 
Suggest caching strategies for per-tenant dashboards. 
Provide an example Redis caching layer integrated with FastAPI/Django.
```

---

## 8. Testing & Validation

```
Generate unit tests and integration tests to ensure tenant isolation. 
Include tests where tenant A should never see tenant B’s data. 
Add load tests simulating 10,000 tenants with 1,000 records each.
```

---

## 9. DevOps / Deployment

```
Write a Kubernetes deployment strategy for a multi-tenant Django/FastAPI app. 
Ensure database migrations, schema creation, and row-level policies 
can run automatically during deployment. 
Suggest monitoring tools for tenant-level performance tracking.
```

---

## 10. Refactoring Helper

```
Refactor this code to remove schema-based logic and replace it with row-based logic. 
Ensure all queries reference tenant_id. 
Update models, serializers, and views accordingly.
```

---

# 🚀 Pre-Launch Migration Checklist (Schema → Row-Based)

Use this section if you started with **django-tenants (schema-based)** and want to **switch to row-based** before going live.

### ✅ Step 1: Audit Models

* Ensure every tenant-specific table includes a `tenant_id` field.
* Convert schema-specific models into shared tables.
* Avoid per-tenant custom migrations (merge them into main schema).

### ✅ Step 2: Introduce Base Tenant Model

* Create `BaseTenantModel` with `tenant_id` field + auto filter.
* Update all tenant models to inherit from this.

### ✅ Step 3: Migration Script

* Write a migration that loops through existing schemas.
* Copy data into the new shared schema with correct `tenant_id`.
* Preserve foreign keys and constraints.

### ✅ Step 4: Update Middleware

* Remove schema-routing logic.
* Replace with tenant resolver from JWT/headers/domain → `tenant_id`.

### ✅ Step 5: Enforce Security

* Add **Postgres Row-Level Security (RLS)** per table.
* Create policies:

  ```sql
  CREATE POLICY tenant_isolation ON patients 
  FOR SELECT, INSERT, UPDATE, DELETE 
  USING (tenant_id = current_setting('app.tenant_id')::uuid);
  ```

### ✅ Step 6: Adjust Queries & Repositories

* Replace schema-switching with `tenant_id` filters.
* Cursor prompt to use:

  ```
  Refactor this query to filter by tenant_id automatically using the base model.
  ```

### ✅ Step 7: Testing

* Write **cross-tenant isolation tests**.
* Run **load tests** for 1,000+ tenants.
* Validate **migration rollback scripts**.

### ✅ Step 8: Documentation

* Update developer guide on tenancy approach.
* Include tenant onboarding process (provision new `tenant_id`).

### ✅ Step 9: Monitoring

* Add per-tenant usage metrics.
* Track queries, errors, and load per tenant.

### ✅ Step 10: Rollout Strategy

* Dry run migration in **staging**.
* Validate end-to-end flows.
* Roll out in production with **backups + rollback plan**.


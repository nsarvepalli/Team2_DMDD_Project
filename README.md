# Team 2 DMDD Project – Patient Care Management (PCM) Database

## Project Overview
This project delivers an **Oracle SQL/PLSQL-based Patient Care Management system** for a clinic/hospital workflow. We designed and implemented a complete database solution that supports:
- patient and doctor management,
- appointment scheduling and follow-ups,
- prescriptions and medication inventory,
- billing and payment tracking,
- analytical reporting for operations.

The solution is centered on the `PCM` schema and includes DDL, data loads, business logic, views, access-control scripts, and reports.

---

## What We Actually Built

### 1) Relational data model (core schema)
We created normalized tables with keys and integrity constraints for:
- `DOCTOR`
- `PATIENT`
- `APPOINTMENT`
- `PRESCRIPTION`
- `PRESCRIPTION_ORDER`
- `MEDICATION`
- `PHARMACY`
- `BILLING`

The DDL script is idempotent-friendly (drops existing objects before recreation) and adds:
- primary keys,
- unique constraints,
- check constraints (e.g., appointment status, medication type, payment status),
- foreign-key relationships across the full care workflow.

---

### 2) Seeded realistic demo data
We populated the schema with sample records for doctors, patients, pharmacies, medications, appointments, prescriptions, and billing to support testing and analytics use cases.

This allows end-to-end queries and reports to run on non-empty, relationally connected data.

---

### 3) Operational/business views
We implemented reusable SQL views for day-to-day analysis:
- **Medication_Stock_Status** – medication stock availability labeling.
- **Doctors_Patient_Load_View** – doctor-wise patient workload.
- **Patient_History_View** – appointment and prescription timeline by patient.
- **Prescription_Summary_View** – prescription lifecycle summary (start/end context).
- **Medical_History_View** – consolidated patient + doctor + treatment + medication history.

---

### 4) Data-quality and safety triggers
We added triggers to enforce key business rules automatically:
- prevent doctor/patient appointment conflicts,
- reduce stock after prescription order creation,
- validate billing totals against ordered prescription costs,
- block prescribing expired medication,
- validate primary doctor existence for each patient.

These constraints move critical validation into the database layer.

---

### 5) PL/SQL packages, procedures, and functions
We implemented modular PL/SQL APIs for core workflows:
- **Patient management** (`patient_pkg`) – add patient + existence checks.
- **Appointment management** (`appointment_pkg`) – schedule appointment + duplicate-on-date checks.
- **Billing management** (`billing_pkg`) – generate bill + payment-status retrieval.
- **Prescription management** (`prescription_mgmt_pkg`) – prescription-order workflow and stock checks.

This gives the project a service-like interface beyond raw SQL statements.

---

### 6) Reporting layer (analytics queries)
We authored reports focused on real operational questions, including:
- doctor availability vs patient coverage by city,
- medication inventory and dispensing activity,
- patient profile summary (appointments/prescriptions/billing/medications),
- appointment status and follow-up tracking,
- doctor performance overview.

These reports demonstrate practical decision-support output from the transactional model.

---

### 7) Role/access setup support
We included supporting scripts to create admins/users and grant access to base tables and views so different personas can query safely.

---

## Repository File Guide
- `DDL_Script.sql` – schema creation + constraints + FK relationships.
- `DML_Script.sql`, `DML 2.sql` – sample data loading.
- `Views.sql` – operational/analytical views.
- `Triggers.sql` – business-rule enforcement triggers.
- `Package,procedure,function.sql` – PL/SQL packages and logic units.
- `Reports.sql` – reporting queries.
- `Create_Clinic_Admin_and_User_script.sql` – user/role setup.
- `Create_Tables_As_App_Admin.sql` – app admin object creation helper.
- `Grant_Access_To_Other_Users.sql`, `Grant_Access_To_Views.sql` – permission grants.

---

## Suggested Execution Order
1. Create users/roles (if needed).
2. Run `DDL_Script.sql`.
3. Run `DML_Script.sql` and `DML 2.sql`.
4. Run `Views.sql`.
5. Run `Triggers.sql`.
6. Run `Package,procedure,function.sql`.
7. Run grant scripts for access.
8. Execute `Reports.sql` to validate outcomes.

---

## Key Outcome
The project is not just a set of tables—it is a complete **database-backed healthcare workflow prototype** with:
- transactional data model,
- embedded business rules,
- procedural APIs,
- secure access scaffolding,
- and decision-oriented reporting.


# Data Dictionary

This document describes the structure and contents of all CSV files in the `/data` directory.

## Table of Contents
- [patients.csv](#patientscsv)
- [appointments.csv](#appointmentscsv)
- [medical_records.csv](#medical_recordscsv)
- [billing_claims.csv](#billing_claimscsv)
- [staff.csv](#staffcsv)
- [inventory.csv](#inventorycsv)
- [insurance_providers.csv](#insurance_providerscsv)

---

## patients.csv

Patient demographics, contact information, and insurance details.

**Records:** ~100 patients  
**Primary Key:** patient_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| patient_id | String | Unique patient identifier | PT10001 |
| first_name | String | Patient first name | John |
| last_name | String | Patient last name | Smith |
| date_of_birth | Date | Birth date (YYYY-MM-DD) | 1985-03-15 |
| address | String | Street address | 1234 Main St |
| city | String | City | Springfield |
| state | String | State (2-letter code) | CA |
| zip_code | String | ZIP code | 94102 |
| phone | String | Phone number | 555-1234 |
| email | String | Email address | john.smith@email.com |
| insurance_provider | String | Insurance provider ID (FK to insurance_providers) or "Self-Pay" | INS001 |
| policy_number | String | Insurance policy number | POL123456 |
| group_number | String | Insurance group number | GRP1234 |
| registration_date | Date | Date patient registered | 2021-06-10 |
| last_visit_date | Date | Date of most recent visit | 2024-11-15 |
| status | String | Patient status | Active, Inactive |

**Data Quality Notes:**
- ~5% of patients are "Self-Pay" (no insurance)
- ~15% of patients haven't been seen in over 2 years (inactive but not marked)

---

## appointments.csv

Appointment scheduling data including past, current, and future appointments.

**Records:** ~4,300+ appointments (3 months historical + 2 months future)  
**Primary Key:** appointment_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| appointment_id | String | Unique appointment identifier | APT50001 |
| patient_id | String | Patient identifier (FK to patients) | PT10001 |
| provider_id | String | Provider identifier (FK to staff) | EMP1001 |
| appointment_date | Date | Date of appointment | 2024-12-15 |
| appointment_time | Time | Time of appointment | 09:30:00 |
| duration_minutes | Integer | Scheduled duration | 15, 30, 45 |
| appointment_type | String | Type of visit | Annual Physical, Follow-up Visit, Sick Visit |
| status | String | Appointment status | Scheduled, Completed, No-Show, Cancelled, Rescheduled |
| checkin_time | DateTime | When patient checked in (blank if not checked in) | 2024-12-15 09:25:00 |
| notes | String | Additional notes | Patient did not show, no call |

**Appointment Types:**
- Annual Physical (30 min)
- Follow-up Visit (15 min)
- Sick Visit (20 min)
- Well Child Check (30 min)
- Chronic Care Management (20 min)
- New Patient Visit (45 min)
- Vaccine Only (15 min)

**Data Quality Notes:**
- **15% no-show rate** for past appointments (key pain point)
- ~5% cancellation rate
- Future appointments may have pre-cancellations

---

## medical_records.csv

Clinical documentation from completed patient visits.

**Records:** ~2,000+ records (from completed appointments)  
**Primary Key:** record_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| record_id | String | Unique medical record identifier | MR60001 |
| appointment_id | String | Associated appointment (FK to appointments) | APT50001 |
| patient_id | String | Patient identifier (FK to patients) | PT10001 |
| provider_id | String | Provider who saw patient (FK to staff) | EMP1001 |
| visit_date | Date | Date of visit | 2024-12-15 |
| chief_complaint | String | Reason for visit | Cold symptoms for 3 days |
| blood_pressure | String | BP reading | 120/80 |
| heart_rate | Integer | Heart rate (bpm) | 72 |
| temperature_f | Float | Temperature in Fahrenheit | 98.6 |
| weight_lbs | Integer | Weight in pounds | 165 |
| height_inches | Integer | Height in inches | 70 |
| bmi | Float | Body Mass Index | 23.7 |
| diagnosis_codes | String | ICD-10 codes (semicolon-separated) | I10;E11.9 |
| diagnosis_descriptions | String | Diagnosis descriptions (semicolon-separated) | Essential hypertension;Type 2 diabetes |
| prescriptions | String | Medications prescribed (semicolon-separated) | Lisinopril 10mg;Metformin 500mg |
| clinical_notes | String | Provider's clinical notes | Patient presents with... |
| followup_needed | String | Follow-up timeframe | None, 2 weeks, 1 month, 3 months, 6 months, 1 year |

**Common ICD-10 Codes:**
- Z00.00 - Routine health examination
- I10 - Essential hypertension
- E11.9 - Type 2 diabetes
- J06.9 - Upper respiratory infection
- K21.9 - GERD
- M79.3 - Back pain

---

## billing_claims.csv

Insurance claims and billing information.

**Records:** ~2,000+ claims (one per completed visit)  
**Primary Key:** claim_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| claim_id | String | Unique claim identifier | CLM70001 |
| appointment_id | String | Associated appointment (FK to appointments) | APT50001 |
| patient_id | String | Patient identifier (FK to patients) | PT10001 |
| insurance_provider | String | Insurance provider ID (FK to insurance_providers) | INS001 |
| submission_date | Date | Date claim submitted | 2024-12-16 |
| procedure_codes | String | CPT codes (semicolon-separated) | 99213;85025 |
| diagnosis_codes | String | ICD-10 codes (semicolon-separated) | I10 |
| total_charge | Decimal | Total billed amount | 175.00 |
| insurance_payment | Decimal | Amount paid by insurance | 140.00 |
| patient_responsibility | Decimal | Patient portion (copay/deductible) | 35.00 |
| paid_amount | Decimal | Total amount received | 175.00 |
| claim_status | String | Current status | Paid, Denied, Pending, Patient Responsibility |
| payment_date | Date | Date payment received (blank if unpaid) | 2024-12-30 |
| notes | String | Claim notes/denial reasons | Missing authorization |

**CPT Procedure Codes:**
- 99213 - Office visit, established patient, 15 min ($150)
- 99214 - Office visit, established patient, 25 min ($200)
- 99203 - Office visit, new patient, 30 min ($250)
- 99385 - Annual wellness visit ($300)
- 85025 - Complete blood count ($25)
- 80053 - Comprehensive metabolic panel ($35)

**Claim Statuses:**
- **Paid** - Claim processed and paid (70%)
- **Denied** - Claim rejected (~18% - key pain point)
- **Pending** - Under review (~7%)
- **Patient Responsibility** - Self-pay patients

**Common Denial Reasons:**
- Missing authorization
- Invalid diagnosis code
- Services not covered
- Eligibility issue
- Duplicate claim
- Timely filing limit exceeded

---

## staff.csv

Employee directory with roles and contact information.

**Records:** 17 employees  
**Primary Key:** employee_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| employee_id | String | Unique employee identifier | EMP1001 |
| name | String | Full name | Dr. Emily Chen |
| role | String | Job title/role | Physician, Medical Assistant, Receptionist |
| department | String | Department | Clinical Services, Patient Services, Revenue Cycle |
| email | String | Work email | echen@healthbridge.com |
| phone | String | Work phone extension | 555-0201 |
| employment_status | String | Full-time or Part-time | Full-time, Part-time |
| status | String | Employment status | Active, Inactive |

**Roles by Department:**
- **Clinical Services:** Physicians (5), Nurse Practitioners (2), Medical Assistants (3)
- **Patient Services:** Receptionists (3)
- **Revenue Cycle:** Billing Specialists (2)
- **Administration:** Office Manager (1), IT Administrator (1)

---

## inventory.csv

Medical supplies, equipment, and medication inventory.

**Records:** 28 items  
**Primary Key:** item_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| item_id | String | Unique item identifier | INV001 |
| item_name | String | Item description | Examination gloves (box of 100) |
| category | String | Item category | Supplies, Lab, Vaccine, Medication, Office |
| vendor | String | Supplier/vendor name | McKesson |
| current_quantity | Integer | Current stock on hand | 150 |
| reorder_point | Integer | Quantity that triggers reorder | 40 |
| par_level | Integer | Target stock level | 150 |
| unit_cost | Decimal | Cost per unit | 12.99 |
| last_order_date | Date | Date of most recent order | 2024-11-15 |
| expiration_date | Date | Expiration date (blank if N/A) | 2025-06-30 |
| status | String | Stock status | In Stock, Low Stock, Out of Stock, Overstock |
| notes | String | Special notes/alerts | URGENT: Order needed immediately |

**Categories:**
- **Supplies** - Examination and clinical supplies
- **Lab** - Laboratory testing supplies
- **Vaccine** - Immunizations (refrigerated)
- **Medication** - Sample medications
- **Office** - Administrative supplies

**Data Quality Notes:**
- ~10% of items out of stock (pain point)
- ~20% of items at or below reorder point
- ~15% of expirable items expiring within 30 days (pain point)
- ~10% overstocked items

---

## insurance_providers.csv

Insurance companies and plan information.

**Records:** 10 providers  
**Primary Key:** provider_id

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| provider_id | String | Unique provider identifier | INS001 |
| provider_name | String | Insurance company name | BlueCross BlueShield |
| plan_type | String | Type of plan | PPO, HMO, EPO, Government |
| phone | String | Provider phone number | 800-555-0101 |
| claims_email | String | Email for claims submission | claims@bcbs.com |
| status | String | Provider status | Active, Inactive |

**Plan Types:**
- **PPO** - Preferred Provider Organization (most flexible)
- **HMO** - Health Maintenance Organization (requires referrals)
- **EPO** - Exclusive Provider Organization
- **Government** - Medicare, Medicaid

---

## Relationships

```
patients (patient_id)
  ├─→ appointments (patient_id)
  │    ├─→ medical_records (appointment_id)
  │    └─→ billing_claims (appointment_id)
  └─→ billing_claims (patient_id)

insurance_providers (provider_id)
  ├─→ patients (insurance_provider)
  └─→ billing_claims (insurance_provider)

staff (employee_id)
  ├─→ appointments (provider_id)
  └─→ medical_records (provider_id)
```

---

## Data Generation Notes

All data is **completely fictional** and generated for training purposes:
- Names, addresses, phone numbers, and emails are randomly generated
- No real patient information (PHI) is included
- Medical information is simplified for training scenarios
- Dates span approximately 5 months (3 months historical + 2 months future)

The data intentionally includes **pain points and inefficiencies** to enable Copilot Agent scenarios:
- High no-show rates (15%)
- Claim denial rates (18%)
- Inventory stockouts and expiring items
- Outstanding patient balances
- Insurance verification gaps

These issues provide opportunities for agents to demonstrate value and improvement.

# HealthBridge Medical Group - Copilot Agents Training Environment

## 🏥 Company Overview

**HealthBridge Medical Group** is a fictional primary care medical practice designed as a training environment for building GitHub Copilot Agents. This comprehensive simulation includes realistic data, personas, workflows, and operational challenges that sales teams can use to demonstrate how Copilot Agents improve business operations.

### Company Profile
- **Name:** HealthBridge Medical Group
- **Type:** Primary Care Medical Practice
- **Specialties:** Family Medicine, Internal Medicine, Pediatrics
- **Size:** 120 employees
- **Location:** Single facility in suburban area
- **Patient Base:** ~8,000 active patients
- **Annual Visits:** ~45,000 patient encounters

### Organizational Structure

#### Clinical Staff (75 employees)
- **Physicians:** 12 (8 Family Medicine, 3 Internal Medicine, 1 Pediatrics)
- **Nurse Practitioners:** 6
- **Physician Assistants:** 3
- **Registered Nurses:** 15
- **Medical Assistants:** 25
- **Lab Technicians:** 8
- **Radiology Technicians:** 6

#### Administrative Staff (45 employees)
- **Front Desk/Receptionists:** 12
- **Billing Specialists:** 10
- **Medical Records:** 6
- **Insurance Verification:** 5
- **Office Managers:** 3
- **IT/Systems Administrators:** 2
- **Facility/Maintenance:** 4
- **HR/Compliance:** 3

## 📊 Current Business Challenges

### Operational Inefficiencies
1. **Appointment Management** - 15% no-show rate costing ~$180K annually
2. **Insurance Verification** - Average 45-minute delay per patient due to manual verification
3. **Prescription Refills** - 150+ refill requests daily overwhelming nursing staff
4. **Patient Communication** - Manual reminder calls miss 40% of patients
5. **Billing/Claims** - 18% claim rejection rate requiring resubmission
6. **Supply Management** - Frequent stockouts and over-ordering issues
7. **Staff Coordination** - Scheduling conflicts and coverage gaps

### Key Performance Indicators (KPIs)
- **Patient Satisfaction:** 3.8/5.0 (target: 4.5/5.0)
- **First-Call Resolution:** 62% (target: 85%)
- **Claims Acceptance Rate:** 82% (target: 95%)
- **Appointment Utilization:** 78% (target: 92%)
- **Staff Overtime:** 18% above budget
- **Patient Wait Time:** Average 28 minutes (target: <15 minutes)

## 🎯 Copilot Agent Opportunities

This environment is designed for building Copilot Agents that address specific business challenges:

### 1. **Intelligent Appointment Scheduler**
- Reduce no-shows through predictive analytics
- Optimize provider schedules based on appointment types
- Automated waitlist management and patient notifications

### 2. **Insurance Verification Assistant**
- Real-time eligibility checks
- Pre-authorization automation
- Coverage summaries for front desk staff

### 3. **Patient Communication Hub**
- Automated appointment reminders (SMS, email, voice)
- Prescription refill request handling
- Follow-up care coordination

### 4. **Clinical Documentation Helper**
- Voice-to-text for provider notes
- ICD-10 code suggestions
- Treatment plan templates

### 5. **Billing & Claims Manager**
- Claim scrubbing before submission
- Rejection analysis and correction
- Payment posting automation

### 6. **Inventory Intelligence**
- Predictive ordering based on usage patterns
- Expiration date tracking
- Vendor price comparison

## 📁 Project Structure

```
CoPilotLearning/
├── README.md                 # This file
├── data/                     # CSV datasets
│   ├── patients.csv
│   ├── appointments.csv
│   ├── medical_records.csv
│   ├── billing_claims.csv
│   ├── staff.csv
│   ├── inventory.csv
│   └── insurance_providers.csv
├── personas/                 # Role-specific workflows and pain points
│   ├── front_desk.md
│   ├── medical_assistant.md
│   ├── physician.md
│   ├── billing_specialist.md
│   ├── office_manager.md
│   └── it_administrator.md
├── workflows/               # Detailed process documentation
│   ├── appointment_booking.md
│   ├── patient_checkin.md
│   ├── clinical_visit.md
│   ├── prescription_management.md
│   ├── insurance_billing.md
│   ├── claims_processing.md
│   └── inventory_management.md
└── docs/                    # Additional documentation
    ├── getting_started.md
    ├── agent_scenarios.md
    └── data_dictionary.md
```

## 🚀 Getting Started

1. **Explore the Data:** Review CSV files in `/data` to understand the business operations
2. **Choose a Persona:** Select a role from `/personas` to understand specific challenges
3. **Review Workflows:** Study process flows in `/workflows` to identify improvement areas
4. **Build an Agent:** Create a Copilot Agent to solve a specific business problem
5. **Measure Impact:** Use the KPIs to demonstrate value

## 📝 Data Overview

All data is **fictional** and generated for training purposes only. No real patient information is included.

### Available Datasets
- **Patients** (~8,000 records) - Demographics, contact info, insurance
- **Appointments** (~15,000 records) - 6 months of scheduling data
- **Medical Records** (~12,000 records) - Visit notes, diagnoses, prescriptions
- **Billing/Claims** (~13,500 records) - Invoices, payments, insurance claims
- **Staff** (120 records) - Employee directory, roles, schedules
- **Inventory** (~500 items) - Medical supplies, medications, equipment
- **Insurance Providers** (25 providers) - Plans, coverage details

## 🎓 Training Scenarios

See `/docs/agent_scenarios.md` for specific challenges and exercises designed for different skill levels:
- **Beginner:** Simple data lookup and reporting agents
- **Intermediate:** Workflow automation and notification systems
- **Advanced:** Predictive analytics and multi-system integrations

## 📄 License

This is a fictional training environment created for educational purposes.

---

**Questions?** See `/docs/getting_started.md` for detailed instructions on using this training environment.

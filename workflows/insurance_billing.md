# Insurance Verification and Billing Workflow

## Overview
Insurance verification and billing is a critical revenue cycle process that involves confirming coverage, submitting claims, and managing denials. Currently plagued by an 18% claim rejection rate costing significant time and revenue.

## Current State Workflow

### Phase 1: Pre-Visit Insurance Verification

#### Step 1: Insurance Information Collection
**Actors:** Front Desk, Patient  
**Duration:** 2-3 minutes  
**When:** Ideally at scheduling, often at check-in

1. Request insurance card (front and back)
2. Photocopy or scan card
3. Enter insurance information:
   - Provider name and ID
   - Policy number
   - Group number
   - Subscriber information
4. Verify patient is subscriber or dependent

**Pain Points:**
- **CRITICAL:** Only done at booking 35% of the time
- Rest verified at check-in (causes delays)
- Cards not updated when insurance changes
- Manual data entry errors

---

#### Step 2: Eligibility Verification
**Actors:** Front Desk or Billing Specialist  
**Duration:** 15-45 minutes  
**When:** Should be pre-visit, often skipped

**Manual Process:**
1. Call insurance company
2. Wait on hold (average 15-20 minutes)
3. Provide patient and practice information
4. Ask about:
   - Active coverage on date of service
   - Copay/coinsurance amounts
   - Deductible status
   - Prior authorization requirements
   - Covered services
5. Document in notes (often inconsistent format)

**Pain Points:**
- **CRITICAL:** Skipped 65% of the time due to time constraints
- Long hold times with insurers
- Information not documented properly
- Patients arrive with expired/inactive coverage
- Leads to claim denials and collection issues

---

#### Step 3: Prior Authorization (When Required)
**Actors:** Medical Assistant, Provider, Billing Specialist  
**Duration:** 20-45 minutes per authorization  
**When:** After provider orders service/medication

1. Determine if prior auth required (manual lookup)
2. Complete authorization form:
   - Patient demographics
   - Diagnosis codes (ICD-10)
   - Procedure codes (CPT)
   - Clinical justification
   - Provider signature
3. Submit via fax or phone
4. Wait for approval (1-7 days)
5. Follow up if no response
6. Document authorization number

**Pain Points:**
- **MAJOR:** Takes 3-5 hours weekly of provider/MA time
- Delays patient care (sometimes weeks)
- Requirements not always known upfront
- High rejection rate requiring appeals
- Tracking system is manual spreadsheet

---

### Phase 2: Post-Visit Claim Creation

#### Step 4: Charge Capture
**Actors:** Provider, Medical Assistant  
**Duration:** 5-10 minutes per visit  
**When:** During or immediately after visit

1. Provider documents visit in EMR
2. Selects diagnosis codes (ICD-10)
3. Selects procedure codes (CPT)
4. Reviews and signs note

**Pain Points:**
- Coding errors common (18% of claims rejected)
- Providers not trained coders
- Code combinations sometimes invalid
- Under-coding loses revenue
- Over-coding risks compliance issues

---

#### Step 5: Claim Preparation
**Actors:** Billing Specialist  
**Duration:** 10-15 minutes per claim  
**When:** 1-3 days after visit

1. Review provider's coding
2. Verify codes are complete and valid
3. Check diagnosis links to procedures
4. Query provider if clarification needed (3-5 day delay)
5. Add modifiers if needed
6. Enter charges in billing system

**Pain Points:**
- Manual review of 40-60 claims daily
- Provider queries delay submission
- No automated validation
- Inconsistent between billing staff

---

#### Step 6: Claim Submission
**Actors:** Billing Specialist  
**Duration:** 1-2 hours for daily batch  
**When:** Daily batch submission

1. Generate claims in billing system
2. Final review of batch
3. Submit electronically to clearinghouse
4. Print/mail paper claims for payers requiring them
5. Document submission date

**Pain Points:**
- Some claims held waiting for corrections
- Paper claims to some payers (slower payment)
- No pre-submission validation
- Submission delays cost money (time value)

---

### Phase 3: Claim Tracking and Resolution

#### Step 7: Payment Posting
**Actors:** Billing Specialist  
**Duration:** 2-3 hours daily  
**When:** As payments received

1. Receive EOB (Explanation of Benefits) from payer
2. Match EOB to claims in system
3. Post insurance payment amount
4. Post adjustments/contractual write-offs
5. Post patient responsibility
6. Generate patient statement if balance remains

**Pain Points:**
- Manual matching of EOBs to claims
- Payments may cover multiple claims
- Adjustment reasons not always clear
- Patient balances not communicated well

---

#### Step 8: Denial Management
**Actors:** Billing Specialist  
**Duration:** 15-20 minutes per denial  
**When:** Continuous (200+ backlog)

**When Claim Denied:**
1. Review denial reason code
2. Pull patient chart
3. Determine if correctable
4. Research payer requirements
5. Correct and resubmit, OR
6. Initiate appeal process:
   - Write appeal letter
   - Attach supporting documentation
   - Submit to payer
   - Track appeal status
7. Follow timely filing limits

**Pain Points:**
- **CRITICAL:** 18% denial rate (industry avg 10-12%)
- 200+ denied claims in backlog
- Takes 15-20 minutes per claim to resolve
- Some age past timely filing and must be written off
- **$8K-12K monthly write-offs**
- Common denial reasons could be prevented

**Top Denial Reasons:**
1. Missing/invalid authorization (22%)
2. Invalid diagnosis code combinations (18%)
3. Services not covered (15%)
4. Eligibility issues (12%)
5. Duplicate claim (10%)
6. Timely filing exceeded (8%)
7. Other (15%)

---

#### Step 9: Patient Collections
**Actors:** Billing Specialist, Collections  
**Duration:** Varies  
**When:** After insurance processes

1. Generate patient statements (monthly)
2. Mail statements
3. Wait 30 days
4. Make collection phone calls
5. Set up payment plans
6. Send to collections agency after 90+ days
7. Write off uncollectable amounts

**Pain Points:**
- Patient responsibility increasing (high deductible plans)
- **$180K outstanding patient balances**
- Collection calls unpleasant and time-consuming
- Many patients don't understand their bills
- 55% collection rate on patient responsibility

---

## Workflow Diagram

```
Pre-Visit:
Insurance Card → [Manual Verification - Often Skipped] → Prior Auth?
                                ↓
                          Patient Arrives
                                ↓
Post-Visit:
Provider Codes → Billing Review → Claim Creation → Submission
                     ↓                                  ↓
            [Query Provider]                    [Wait 14-30 days]
                                                       ↓
                     Payment Received ← OR → Denial (18%)
                            ↓                         ↓
                    Post Payment              Research & Fix
                            ↓                         ↓
                    Bill Patient              Resubmit/Appeal
                            ↓                         ↓
                    Collection            [Many Written Off]
```

---

## Metrics

**Current Performance:**
- Claims submitted daily: 40-60
- Clean claim rate (accepted first time): 82%
- Denial rate: 18%
- Average days in A/R: 42 days
- Denial backlog: 200+ claims
- Monthly write-offs: $8K-12K
- Patient collection rate: 55%
- Insurance verification at booking: 35%
- Prior auth average time: 30 minutes each

**Financial Impact:**
- **$95K monthly delayed revenue** (due to denials)
- **$120K annual write-offs** (aged denials)
- **$180K outstanding patient balances**

---

## Copilot Agent Opportunities

### 🤖 Intelligent Claim Scrubbing Agent

**Capabilities:**
1. **Pre-Submission Validation:**
   - Verify all required fields present
   - Check ICD-10 and CPT code validity
   - Validate code combinations
   - Confirm diagnosis links to procedures
   - Check for missing modifiers
2. **Payer-Specific Rules:**
   - Apply payer-specific requirements
   - Check authorization on file
   - Verify coverage for services
3. **Error Prevention:**
   - Flag potential issues before submission
   - Suggest corrections
   - Learn from past denials
4. **Automated Corrections:**
   - Fix common errors automatically
   - Route complex issues to specialists

**Expected Impact:**
- Reduce rejection rate from 18% to <5%
- Increase clean claim rate to 95%+
- **Accelerate cash flow by 15-20 days**
- **Recover $80K monthly in faster payments**
- Reduce rework by 70%

---

### 🤖 Real-Time Insurance Verification Agent

**Capabilities:**
1. **Instant Eligibility Checks:**
   - API integration with all major payers
   - Real-time coverage verification
   - Active status on date of service
2. **Coverage Summary:**
   - Copay/coinsurance amounts
   - Deductible status and remaining
   - Out-of-pocket max
   - Covered services
3. **Authorization Detection:**
   - Flag services requiring prior auth
   - Track authorization status
   - Alert when auth needed
4. **Proactive Updates:**
   - Monitor for coverage changes
   - Alert before appointments if coverage lapsed
   - Suggest patient contact

**Expected Impact:**
- 100% pre-visit verification (vs. 35%)
- Eliminate eligibility denials (12% of denials)
- Reduce check-in time from 10 to 3 minutes
- Better patient payment collection (upfront awareness)
- Fewer billing surprises for patients

---

### 🤖 Automated Denial Management Agent

**Capabilities:**
1. **Smart Categorization:**
   - Auto-categorize denials by reason code
   - Prioritize by revenue and resolution likelihood
   - Track timely filing deadlines
2. **Automated Resolution:**
   - Auto-correct simple errors (40% of denials)
   - Resubmit corrected claims immediately
   - No human intervention needed
3. **Appeal Assistance:**
   - Generate appeal letters with documentation
   - Compile clinical support automatically
   - Track appeal status
   - Follow up automatically
4. **Pattern Analysis:**
   - Identify denial trends
   - Recommend process improvements
   - Provider-specific feedback

**Expected Impact:**
- Reduce denial write-offs by 60% (**$5K-7K monthly savings**)
- Process denials 3x faster
- Auto-resolve 40% of denials
- Never miss timely filing deadlines
- Clear backlog from 200 to <50 claims

---

### 🤖 Coding Quality Assistant Agent

**Capabilities:**
1. **Real-Time Coding Support:**
   - Suggest ICD-10 codes from clinical notes
   - Recommend appropriate CPT codes
   - Validate code combinations
   - Check for missing specificity
2. **Learning from Documentation:**
   - Extract diagnoses from provider notes
   - Map symptoms to codes
   - Suggest additional codes for proper specificity
3. **Compliance Checking:**
   - Flag over-coding risks
   - Ensure proper documentation support
   - Medical necessity validation
4. **Provider Feedback:**
   - Coding quality scorecards
   - Education on common errors

**Expected Impact:**
- Reduce coding errors by 80%
- Eliminate 3-5 day provider query delays
- Capture additional revenue (**$15K+ monthly** from proper coding)
- Improve provider satisfaction
- Reduce compliance risk

---

## Training Exercises

### Beginner
Analyze the billing_claims.csv to identify the most common denial reasons and calculate the financial impact.

### Intermediate
Build an agent that validates diagnosis codes in medical_records.csv match the claims in billing_claims.csv and flags mismatches.

### Advanced
Create an agent that predicts which claims are likely to be denied based on historical patterns and recommends preventive actions before submission.

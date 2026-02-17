# Prescription Management Workflow

## Overview
Prescription refill requests are one of the highest-volume processes at HealthBridge Medical Group, with 150+ daily requests overwhelming medical assistants and disrupting clinical workflow.

## Current State Workflow

### Step 1: Refill Request Receipt
**Actors:** Various  
**Duration:** Variable  
**Volume:** 150+ daily

**Request Sources:**
1. **Phone Calls (40%)** - Patient calls office directly
2. **Pharmacy Calls/Faxes (35%)** - Pharmacy contacts on patient's behalf
3. **Patient Portal Messages (15%)** - Electronic requests
4. **Walk-in Requests (10%)** - Patient asks at visit

**Pain Points:**
- Multiple channels hard to track
- No prioritization system
- Interrupts workflow constantly
- Some requests lost or delayed

---

### Step 2: Request Documentation
**Actors:** Front Desk or Medical Assistant  
**Duration:** 2-3 minutes per request

**Phone Request Process:**
1. Answer call (or return voicemail)
2. Verify patient identity (name, DOB)
3. Ask for medication name and pharmacy
4. Write on paper slip or sticky note
5. Place in MA inbox

**Pharmacy Fax Process:**
1. Check fax machine periodically
2. Sort faxes by provider
3. Place in provider/MA mailbox
4. Hope they see it

**Pain Points:**
- **CRITICAL:** Paper-based system prone to loss
- Handwriting legibility issues
- No tracking mechanism
- Piles up quickly
- No urgency indication

---

### Step 3: Chart Review
**Actors:** Medical Assistant  
**Duration:** 3-5 minutes per request

1. Pull patient chart in EMR
2. Locate current medication list
3. Verify medication still prescribed
4. Check last refill date
5. Check number of refills remaining
6. Review when patient last seen
7. Look for any alerts or flags

**Pain Points:**
- Time-consuming chart navigation
- Medication lists often out of date
- Can't tell if patient has been picking up meds (compliance)
- Sometimes can't find original prescription

---

### Step 4: Eligibility Determination
**Actors:** Medical Assistant  
**Duration:** 1-2 minutes

**Decision Tree:**
- **Automatic Refill OK IF:**
  - Medication currently active
  - Patient seen within last 12 months (6 months for controlled substances)
  - Refills available on original prescription
  - No medication changes needed
  - No overdue labs or monitoring

- **Requires Provider Review IF:**
  - Patient overdue for follow-up
  - Chronic medication needing monitoring (BP meds, diabetes, thyroid)
  - Controlled substance (DEA schedule II-IV)
  - Patient requesting early refill
  - Medication needs adjustment
  - Labs overdue

- **Requires Office Visit IF:**
  - Not seen in >12 months
  - New medication needed
  - Significant dosage change needed
  - Controlled substance >3 months old

**Pain Points:**
- Decision criteria not always clear
- MAs make clinical judgments they're not trained for
- Inconsistent between MAs
- Patients frustrated when told they need appointment

---

### Step 5: Processing Simple Refills
**Actors:** Medical Assistant  
**Duration:** 2-3 minutes per refill

**For Automatic Refills:**
1. Enter refill in EMR prescription module
2. Select pharmacy from list
3. Confirm medication, dose, quantity
4. Send electronically (or print if pharmacy doesn't accept e-prescribe)
5. Document in patient chart
6. Mark request as completed

**Pain Points:**
- Still requires manual entry
- EMR prescription module slow
- Some pharmacies not in system (must call)
- Takes MA away from patient care

---

### Step 6: Provider Review Queue
**Actors:** Provider, Medical Assistant  
**Duration:** 2-5 minutes per request

**For Requests Needing Review:**
1. MA prepares request with patient context
2. Places in provider's refill queue
3. Provider reviews during breaks or after clinic
4. Provider makes decision:
   - Approve refill
   - Modify dose/medication
   - Request office visit
   - Deny and explain why
5. MA executes provider's decision
6. MA may need to call patient with explanation

**Pain Points:**
- **MAJOR:** Interrupts provider workflow
- Providers review 20-30 requests daily
- MA must wait for provider decision (delays patient)
- Providers annoyed by routine interruptions
- Creates after-hours work

---

### Step 7: Patient Notification
**Actors:** Medical Assistant, Pharmacy  
**Duration:** Variable

**Current Process:**
- Most of the time: No notification sent, patient assumes pharmacy notified
- If refill denied: MA calls patient (often phone tag)
- If appointment needed: MA calls to schedule (more phone tag)

**Pain Points:**
- **CRITICAL:** Patients don't know status
- Call pharmacy only to find out not refilled
- Multiple calls between patient, office, pharmacy
- Poor communication creates frustration

---

### Step 8: Exception Handling

**Scenario: Pharmacy Claims "Never Received"**
1. Patient calls saying pharmacy doesn't have prescription
2. MA must research what happened
3. Check if sent electronically (may have failed)
4. Resend or call pharmacy directly
5. Additional time and frustration

**Scenario: Insurance Doesn't Cover**
1. Pharmacy calls office about rejection
2. MA must research alternatives
3. Contact provider for different medication or prior auth
4. More delays and work

**Scenario: Early Refill Request**
1. Patient calls requesting refill earlier than due
2. MA must investigate (lost medication? taking more than prescribed?)
3. Usually requires provider review
4. Often denied, causing patient complaints

**Pain Points:**
- No good tracking of exceptions
- Each exception creates more work
- Patterns not identified (patient non-compliance, formulary issues)

---

## Workflow Diagram

```
150+ Daily Requests → Multiple Channels (phone, fax, portal, walk-in)
         ↓
   Paper Slips/Faxes → MA Inbox → Chart Review (3-5 min each)
         ↓
   Eligibility Check
         ↓
    /           \
Routine         Needs Provider Review
Refill          (20-30 daily)
   ↓                  ↓
Process in      Provider Queue
EMR (2-3 min)   (interrupts workflow)
   ↓                  ↓
Pharmacy        Provider Decides
   ↓                  ↓
[Patient         MA Executes &
 Wonders]        Calls Patient
```

---

## Metrics

**Current Performance:**
- Daily refill requests: 150+
- MA time per request: 5-10 minutes (simple) to 15-20 minutes (complex)
- **Total MA time on refills: 3-4 hours daily**
- Provider review queue: 20-30 daily
- **Total provider time: 30-45 minutes daily**
- Average processing time: 24-48 hours
- Patient satisfaction: Low (no status updates)
- Lost/delayed requests: 3-5 per week
- Same-day completion rate: 40%

**Staffing Impact:**
- 3 MAs spend 12+ hours combined daily on refills
- Takes them away from rooming patients and clinical care
- Contributes to provider running behind schedule
- Generates overtime on busy days

---

## Copilot Agent Opportunities

### 🤖 Automated Prescription Refill Agent

**Capabilities:**

**1. Multi-Channel Request Intake:**
- Accept requests via phone (voice), text, portal, pharmacy fax
- Natural language understanding
- Automated patient identification
- Capture all relevant details

**2. Intelligent Chart Analysis:**
- Auto-retrieve patient medication history
- Check last visit date
- Verify refill eligibility automatically
- Check for required monitoring (labs, visits)
- Review compliance history

**3. Smart Routing:**
- **Automatic Processing (60%):**
  - Routine refills meeting all criteria
  - No provider review needed
  - Send directly to pharmacy
  - Notify patient
- **Provider Review Queue (30%):**
  - Present with full context
  - Highlight key decision factors
  - One-click approve/modify/deny
  - Auto-execute decision
- **Office Visit Required (10%):**
  - Auto-schedule appointment
  - Notify patient why visit needed
  - Coordinate with scheduling

**4. Pharmacy Integration:**
- Electronic prescribing to any pharmacy
- Real-time status tracking
- Handle rejections automatically
- Prior authorization initiation

**5. Patient Communication:**
- Real-time status updates via SMS/portal
- "Your refill has been sent to CVS"
- "Dr. Chen is reviewing your request"
- "Please schedule a follow-up visit"
- Proactive refill reminders before patient runs out

**6. Compliance Monitoring:**
- Track actual pickup from pharmacy
- Identify non-adherence patterns
- Alert providers to compliance issues
- Suggest interventions

**Expected Impact:**
- **Reduce MA time by 80%** (from 3-4 hours to <1 hour daily)
- **Free up 12+ hours daily across MA team**
- **Reduce provider interruptions by 70%** (only complex cases)
- **Same-day completion rate: 90%** (vs. 40%)
- **Zero lost requests**
- Improved medication adherence monitoring
- Higher patient satisfaction
- MAs can focus on direct patient care

**Financial Impact:**
- **$85K annual savings** in MA time (12 hours daily at $35/hour)
- Better provider productivity (less interruption)
- Improved chronic disease management (better adherence)
- Fewer medication-related complications

---

### 🤖 Medication Management Intelligence Agent

**Capabilities:**

**1. Predictive Refill Management:**
- Predict when patients will need refills
- Proactive outreach before they run out
- Batch similar requests for efficiency

**2. Adherence Analytics:**
- Track pickup patterns from pharmacy data
- Identify non-adherent patients
- Calculate medication possession ratio (MPR)
- Alert care team for intervention

**3. Formulary Optimization:**
- Identify insurance rejection patterns
- Suggest formulary-preferred alternatives
- Auto-generate prior authorizations
- Track approval rates by medication/insurance

**4. Clinical Decision Support:**
- Drug interaction checking
- Alert for duplicate therapies
- Dosing guidance based on labs/vitals
- Evidence-based alternative suggestions

**5. Visit Optimization:**
- Identify patients overdue for monitoring
- Coordinate lab orders with refills
- Bundle multiple medication reviews in one visit
- Maximize care quality and efficiency

**Expected Impact:**
- Improve medication adherence by 25%
- Better chronic disease outcomes
- Reduce medication errors
- Fewer insurance rejections
- More efficient office visits

---

## Training Exercises

### Beginner
Analyze medical_records.csv to identify the most commonly prescribed medications and create a report of prescription volume by medication.

### Intermediate
Build an agent that identifies patients who haven't had a visit in over 12 months but have active prescriptions that should require monitoring.

### Advanced
Create an agent that simulates the refill approval process by analyzing patient data (last visit, medication history) and predicting which refill requests would require provider review vs. automatic approval.

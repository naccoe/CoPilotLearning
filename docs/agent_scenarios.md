# Copilot Agent Scenarios and Training Exercises

This document provides specific, hands-on exercises for building Copilot Agents using the HealthBridge Medical Group data. Exercises are organized by skill level and business impact.

## 📋 Table of Contents
- [Beginner Scenarios](#beginner-scenarios)
- [Intermediate Scenarios](#intermediate-scenarios)
- [Advanced Scenarios](#advanced-scenarios)
- [Challenge Scenarios](#challenge-scenarios)

---

## Beginner Scenarios

### 1. No-Show Analysis Agent
**Persona:** Office Manager, Front Desk  
**Skills:** Data analysis, CSV processing, basic reporting  
**Time:** 30-45 minutes

**Challenge:**
Build an agent that analyzes appointment no-shows to identify patterns and calculate financial impact.

**Requirements:**
- Read appointments.csv
- Calculate overall no-show rate
- Break down by:
  - Day of week
  - Time of day
  - Appointment type
  - Provider
- Calculate revenue lost (assume $150 average per appointment)
- Generate actionable recommendations

**Success Criteria:**
- Identifies 15% no-show rate
- Shows Thursday has highest no-show rate
- Calculates ~$180K annual impact
- Suggests specific improvement areas

**Sample Questions Agent Should Answer:**
- "What's our no-show rate by day of week?"
- "Which providers have the highest no-show rates?"
- "How much revenue are we losing to no-shows?"

---

### 2. Claim Denial Report Agent
**Persona:** Billing Specialist, Office Manager  
**Skills:** Data filtering, categorization, financial analysis  
**Time:** 30-45 minutes

**Challenge:**
Analyze denied insurance claims to identify root causes and prioritize fixes.

**Requirements:**
- Read billing_claims.csv
- Identify denied claims (status = "Denied")
- Categorize by denial reason (from notes field)
- Calculate total $ denied
- Prioritize by frequency and dollar amount
- Suggest preventive measures

**Success Criteria:**
- Identifies 18% denial rate
- Lists top denial reasons
- Calculates ~$95K in denied claim value
- Recommends top 3 preventive actions

**Sample Questions Agent Should Answer:**
- "What's our claim denial rate?"
- "What are the top 3 reasons for denials?"
- "How much money is tied up in denied claims?"

---

### 3. Patient Outreach List Agent
**Persona:** Medical Assistant, Office Manager  
**Skills:** Date calculations, data filtering, list generation  
**Time:** 30 minutes

**Challenge:**
Generate lists of patients who need outreach for preventive care or overdue visits.

**Requirements:**
- Read patients.csv
- Identify patients who haven't been seen in 12+ months
- Create outreach list with:
  - Patient name and contact info
  - Last visit date
  - Days since last visit
  - Priority level
- Export to CSV for calling campaign

**Success Criteria:**
- Identifies ~15 patients overdue for care
- Sorted by days since last visit
- Includes all needed contact information
- Actionable format for front desk staff

---

### 4. Inventory Stockout Alert Agent
**Persona:** Medical Assistant, Office Manager  
**Skills:** Threshold monitoring, alerts, basic reporting  
**Time:** 20-30 minutes

**Challenge:**
Monitor inventory levels and alert staff about items needing reorder.

**Requirements:**
- Read inventory.csv
- Identify items:
  - Out of stock (current_quantity = 0)
  - Below reorder point
  - Expiring within 30 days
- Generate prioritized alert list
- Calculate reorder quantities needed

**Success Criteria:**
- Identifies 6 out-of-stock items
- Lists items below reorder point
- Flags expiring vaccines/medications
- Calculates order quantities to reach par levels

---

## Intermediate Scenarios

### 5. Automated Appointment Reminder Agent
**Persona:** Front Desk  
**Skills:** Scheduling logic, templating, multi-step workflow  
**Time:** 1-2 hours

**Challenge:**
Build an agent that sends automated appointment reminders to reduce no-shows.

**Requirements:**
- Read appointments.csv
- Identify appointments scheduled for tomorrow
- For each appointment:
  - Get patient contact info from patients.csv
  - Generate personalized reminder message
  - Include appointment details (date, time, provider, type)
  - Add instructions (arrive 15 min early, bring insurance card)
- Track reminder sent status
- Handle confirmations and cancellations

**Success Criteria:**
- Generates reminders for all next-day appointments
- Personalized messages with accurate details
- Professional, friendly tone
- Clear call-to-action for confirmation
- Simulation shows 24-hour lead time

**Sample Message Output:**
```
Hi John Smith,

This is a reminder about your appointment tomorrow (December 16, 2024) at 9:30 AM with Dr. Emily Chen for a Follow-up Visit.

Please arrive 15 minutes early and bring your insurance card.

Reply 1 to confirm, 2 to reschedule, or call 555-0200.

HealthBridge Medical Group
```

---

### 6. Claim Validation Agent
**Persona:** Billing Specialist  
**Skills:** Data validation, rule-based logic, error detection  
**Time:** 1-2 hours

**Challenge:**
Validate insurance claims before submission to prevent denials.

**Requirements:**
- Read billing_claims.csv and medical_records.csv
- Check each claim for common errors:
  - Missing diagnosis codes
  - Invalid code combinations
  - Missing patient insurance info
  - Services requiring authorization
- Generate "clean" vs. "needs review" lists
- Provide specific fix recommendations

**Success Criteria:**
- Validates all fields present
- Checks code validity (basic)
- Identifies claims likely to be denied
- Provides actionable fix instructions
- Simulates catching 80% of denials before submission

**Validation Rules:**
1. Diagnosis code must be present
2. Procedure code must be present
3. Insurance provider must be active
4. Diagnosis must justify procedure
5. Patient must have been seen (appointment exists)

---

### 7. Prescription Refill Routing Agent
**Persona:** Medical Assistant  
**Skills:** Decision tree logic, data lookup, workflow automation  
**Time:** 1-2 hours

**Challenge:**
Automate prescription refill request routing based on eligibility rules.

**Requirements:**
- Read medical_records.csv and patients.csv
- Given a refill request, determine routing:
  - **Auto-approve** if routine maintenance med + patient seen <12 months
  - **Provider review** if chronic med needing monitoring or 6-12 months since visit
  - **Office visit required** if >12 months since last visit
- Provide context to help provider decide
- Estimate time saved vs. manual review

**Success Criteria:**
- Correctly routes 90%+ of requests
- Auto-approves ~60% (routine refills)
- Routes 30% to provider with context
- Requires visits for 10%
- Shows 70% time savings for MAs

**Sample Logic:**
```
Request: Lisinopril 10mg refill for patient PT10023
Analysis:
- Medication: Lisinopril (blood pressure)
- Last visit: 2024-08-15 (122 days ago)
- Medication type: Chronic, requires monitoring
- Routing: Provider review (due to monitoring needs)
- Context: Patient due for BP check, last reading 128/82
```

---

### 8. Revenue Cycle Dashboard Agent
**Persona:** Office Manager, Billing Manager  
**Skills:** Multi-source data aggregation, KPI calculation, visualization  
**Time:** 2-3 hours

**Challenge:**
Create a real-time revenue cycle health dashboard.

**Requirements:**
- Aggregate data from multiple CSVs
- Calculate key metrics:
  - Days in A/R
  - Clean claim rate
  - Denial rate by reason
  - Outstanding patient balances
  - Collection rate
- Identify trends and alerts
- Generate executive summary

**Success Criteria:**
- All key metrics calculated correctly
- Trends identified (improving/worsening)
- Red/yellow/green status indicators
- Actionable insights provided
- Executive-ready format

---

## Advanced Scenarios

### 9. No-Show Prediction Model Agent
**Persona:** Office Manager, Front Desk  
**Skills:** Machine learning concepts, pattern recognition, risk scoring  
**Time:** 3-4 hours

**Challenge:**
Build a predictive model to identify appointments at high risk of no-show.

**Requirements:**
- Analyze historical appointment data
- Identify no-show risk factors:
  - Patient demographics
  - Past no-show history
  - Appointment type
  - Day/time patterns
  - Lead time (how far in advance booked)
- Score future appointments by risk
- Recommend intervention strategies
- Simulate ROI from targeted interventions

**Success Criteria:**
- Identifies key risk factors
- Scores appointments from 0-100 risk
- Achieves 70%+ accuracy in identifying high-risk appointments
- Recommends specific interventions
- Calculates ROI ($50K+ from reducing high-risk no-shows)

**Risk Factors to Consider:**
- Previous no-shows (strongest predictor)
- Early morning appointments
- Mondays and Fridays
- Long lead times (>2 weeks)
- First-time patients
- Younger patients (18-25)

---

### 10. Intelligent Claim Optimization Agent
**Persona:** Billing Specialist  
**Skills:** Complex rules engine, optimization, learning from patterns  
**Time:** 4-5 hours

**Challenge:**
Optimize claims to maximize approval rate and revenue capture.

**Requirements:**
- Analyze denied vs. approved claims
- Learn patterns that predict denials
- For new claims:
  - Validate against learned patterns
  - Suggest code optimizations
  - Flag high-risk claims
  - Recommend supporting documentation
- Track improvements over time
- Calculate revenue impact

**Success Criteria:**
- Identifies patterns in 18% denials
- Predicts denial risk with 85%+ accuracy
- Suggests optimizations increasing approval rate
- Simulates reduction from 18% to 5% denial rate
- Calculates $80K+ annual impact

**Advanced Features:**
- Insurance-specific rules learned from data
- Provider-specific coaching
- Continuous learning from feedback

---

### 11. Smart Staff Scheduling Agent
**Persona:** Office Manager  
**Skills:** Constraint optimization, resource allocation, forecasting  
**Time:** 4-6 hours

**Challenge:**
Generate optimal staff schedules minimizing cost while meeting demand.

**Requirements:**
- Use appointments.csv to forecast demand by day/time
- Match staff availability from staff.csv
- Apply constraints:
  - Minimum coverage requirements
  - Maximum hours per employee
  - Skill matching (MAs to providers)
  - Break requirements
  - Overtime minimization
- Generate optimized schedule
- Calculate cost savings vs. current

**Success Criteria:**
- Meets all coverage requirements
- Minimizes overtime (target: on-budget)
- Fair distribution across staff
- Saves 5-10 hours weekly of manager time
- Reduces overtime by 18% ($40K+ annually)

---

### 12. End-to-End Patient Journey Agent
**Persona:** All roles  
**Skills:** Multi-system integration, process orchestration, complex workflows  
**Time:** 6-8 hours (team project)

**Challenge:**
Build an agent that manages the complete patient journey from booking to payment.

**Requirements:**
- **Pre-Visit:**
  - Schedule appointment (conflict-free)
  - Verify insurance eligibility
  - Send automated reminders
  - Process any authorizations needed
- **Visit:**
  - Check-in workflow
  - Clinical documentation support
  - Real-time coding assistance
- **Post-Visit:**
  - Claim creation and validation
  - Submission and tracking
  - Denial prevention/management
  - Patient billing and collections

**Success Criteria:**
- Seamless workflow across all phases
- 90% automation rate
- Reduced errors at each step
- Comprehensive analytics
- $200K+ annual impact across all improvements

---

## Challenge Scenarios

### 13. The Perfect Practice Challenge
**Difficulty:** 🔥🔥🔥🔥🔥  
**Time:** Multi-day project

**Challenge:**
Using all available data, build a comprehensive Copilot Agent ecosystem that:
- Reduces no-shows to <5%
- Achieves 95%+ claim acceptance rate
- Automates 70% of routine tasks
- Improves patient satisfaction to 4.8/5.0
- Generates $500K+ in annual value

**Requirements:**
Design and demonstrate the complete solution including:
- Multiple coordinated agents
- Integration points
- Change management approach
- ROI calculation
- Implementation roadmap

---

### 14. Custom Persona Challenge
**Difficulty:** 🔥🔥🔥  
**Time:** 2-3 hours

**Challenge:**
Choose a persona not covered (nurse, lab tech, etc.) and:
1. Create their profile with pain points
2. Identify their workflows
3. Build an agent solving their biggest problem
4. Calculate ROI
5. Present as a mini-case study

---

## 🎯 Demo Competition Ideas

### Speed Challenge
- 15-minute time limit
- Pick any beginner scenario
- Build functioning prototype
- Present ROI

### Impact Challenge
- Must show $100K+ annual value
- Any skill level
- Judged on ROI calculation quality

### Innovation Challenge
- Use the data in unexpected ways
- Most creative/novel agent wins
- Must still solve real business problem

---

## 📊 Evaluation Rubrics

### Technical Execution (40%)
- Agent works correctly
- Handles edge cases
- Code quality
- User experience

### Business Value (40%)
- Clear problem statement
- Realistic solution
- Quantified ROI
- Actionable insights

### Presentation (20%)
- Clear storytelling
- Persona-based narrative
- Professional delivery
- Handles questions well

---

## 💡 Tips for Success

1. **Start Simple** - Beginner exercises build foundation
2. **Use Real Data** - Work with the provided CSVs
3. **Calculate ROI** - Always quantify the impact
4. **Tell Stories** - Use personas to make it relatable
5. **Think Integration** - Consider how agents work together
6. **Measure Everything** - Before/after metrics are powerful
7. **Get Feedback** - Practice demos with colleagues

---

## 🚀 Next Steps

1. Pick a scenario matching your skill level
2. Review relevant persona and workflow docs
3. Explore the related data files
4. Build your agent
5. Calculate and present ROI
6. Level up to the next challenge!

**Remember:** The goal is demonstrating business value, not just technical capability. Every agent should answer: "How does this make HealthBridge Medical Group better?"

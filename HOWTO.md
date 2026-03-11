# HOWTO: Building Microsoft Copilot Agents with HealthBridge Data

> **Audience:** Sales Channel Managers  
> **Products:** Microsoft 365 Copilot + Microsoft Copilot Studio  
> **Goal:** Step-by-step guide to build working Copilot agents using the HealthBridge Medical Group training data, so you can demo real value to healthcare prospects.

---

## Table of Contents

1. [Before You Start — Prerequisites](#1-before-you-start--prerequisites)
2. [Understanding the Two Products](#2-understanding-the-two-products)
3. [Setting Up Your Demo Environment](#3-setting-up-your-demo-environment)
4. [Walkthrough 1 — Appointment No-Show Analysis Agent](#4-walkthrough-1--appointment-no-show-analysis-agent)
5. [Walkthrough 2 — Claim Denial Scrubbing Agent](#5-walkthrough-2--claim-denial-scrubbing-agent)
6. [Walkthrough 3 — Prescription Refill Routing Agent](#6-walkthrough-3--prescription-refill-routing-agent)
7. [Connecting Agents to Live Data Sources](#7-connecting-agents-to-live-data-sources)
8. [Publishing and Sharing Your Agent](#8-publishing-and-sharing-your-agent)
9. [Demo Day — Running the Presentation](#9-demo-day--running-the-presentation)
10. [Troubleshooting & FAQ](#10-troubleshooting--faq)

---

## 1. Before You Start — Prerequisites

### Licensing You Need

| Requirement | What It Is | How to Get It |
|---|---|---|
| **Microsoft 365 Copilot license** | Per-user license that enables Copilot in Word, Excel, Teams, etc. | Assigned by your org admin in the Microsoft 365 Admin Center → **Billing → Licenses** |
| **Copilot Studio license** | Enables building custom agents and declarative agents | Included with M365 Copilot, or available standalone via [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com) |
| **SharePoint Online site** | Where you'll host the HealthBridge CSV/data files as a knowledge source | Create one at [your-tenant.sharepoint.com](https://your-tenant.sharepoint.com) |

### Access Checklist

- [ ] You can sign in at [microsoft365.com/copilot](https://microsoft365.com/copilot) and see the Copilot chat
- [ ] You can open [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com) without an access error
- [ ] You have a SharePoint site where you can upload files (or permission to create one)
- [ ] Your admin has **not** blocked Copilot Studio agent creation for your account

> **💡 Tip:** If you hit a permissions wall, ask your M365 admin to check  
> **Admin Center → Settings → Copilot → Manage how users interact with Copilot**.

### What You Should Already Know

- How to navigate Microsoft 365 (Teams, SharePoint, Excel)
- The HealthBridge personas and pain points (read `personas/` and `README.md` first)
- Basic comfort with prompting AI — no coding required

---

## 2. Understanding the Two Products

Before building anything, you need to know what you're working with and when to use each tool.

### Microsoft 365 Copilot (The Day-to-Day Assistant)

**What it is:** An AI assistant embedded in the M365 apps your customers already use.

**Where it lives:**
- Microsoft Teams (chat sidebar)
- Word, Excel, PowerPoint, Outlook (ribbon bar)
- [microsoft365.com/copilot](https://microsoft365.com/copilot) (web chat)

**What it can do out of the box:**
- Analyze data in Excel ("What's our no-show rate by provider?")
- Draft documents in Word ("Write a memo about our claim denial problem")
- Summarize email threads in Outlook
- Answer questions over files stored in SharePoint/OneDrive

**Best for demos when:** You want to show *instant value* — a channel manager opens Excel with `billing_claims.csv` and asks Copilot to analyze denials. No setup required.

### Microsoft Copilot Studio (The Agent Builder)

**What it is:** A low-code platform for building custom AI agents that automate workflows.

**Where it lives:** [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)

**Two kinds of agents you can build:**

| Agent Type | Description | When to Use |
|---|---|---|
| **Declarative Agent** | A focused Copilot with specific instructions, knowledge, and capabilities. Runs inside M365 Copilot chat. | "I want Copilot to be an expert on HealthBridge billing data" |
| **Custom Engine Agent** | A standalone chatbot with topics, flows, triggers, and integrations. Runs in Teams, web, or other channels. | "I want a full appointment-booking bot for the front desk" |

**Best for demos when:** You want to show a *tailored, role-specific agent* — e.g., a billing assistant that only Patricia O'Brien's team uses, pre-loaded with claim rules and denial patterns.

### Which Should I Demo?

| Scenario | Use This |
|---|---|
| "Show me what Copilot does right now" | **M365 Copilot** — open Excel, ask questions |
| "Build me something for my billing team" | **Copilot Studio → Declarative Agent** |
| "I need an automated workflow" | **Copilot Studio → Custom Agent with Flows** |
| "Quick 15-minute demo" | **M365 Copilot** in Excel or Teams |
| "Deep 60-minute workshop" | **Copilot Studio** end-to-end build |

---

## 3. Setting Up Your Demo Environment

### Step 3.1 — Create a SharePoint Site for HealthBridge

1. Go to [your-tenant.sharepoint.com](https://your-tenant.sharepoint.com)
2. Click **+ Create site → Team site**
3. Name it: `HealthBridge Medical Group - Demo`
4. Set privacy to **Private** (you control who sees demo data)
5. Click **Create**

### Step 3.2 — Upload the HealthBridge Data

1. In your new SharePoint site, click **Documents**
2. Create a folder called `HealthBridge Data`
3. Upload all 7 CSV files from the `data/` folder:
   - `patients.csv`
   - `appointments.csv`
   - `medical_records.csv`
   - `billing_claims.csv`
   - `staff.csv`
   - `inventory.csv`
   - `insurance_providers.csv`
4. Also upload the persona files from `personas/` and the workflow files from `workflows/` — these give your agent background context

> **💡 Tip:** SharePoint is the primary knowledge source that M365 Copilot can access. If files aren't in SharePoint or OneDrive, Copilot can't see them.

### Step 3.3 — Open the CSVs in Excel Online (for M365 Copilot Demos)

1. In your SharePoint **Documents** library, click on `appointments.csv`
2. It will open in Excel Online
3. Click **Edit Workbook → Edit in Browser**
4. Excel will auto-detect the CSV columns and format them as a table
5. You should now see the **Copilot** button in the Excel ribbon

Repeat for `billing_claims.csv` and any other files you plan to demo.

### Step 3.4 — Verify Copilot Works

1. In Excel Online with `appointments.csv` open, click the **Copilot** button (right side of ribbon)
2. The Copilot panel opens on the right
3. Try a test prompt:
   ```
   What percentage of appointments have a status of "No-Show"?
   ```
4. Copilot should analyze the data and return approximately **15%**

If this works, your environment is ready. If not, see [Troubleshooting](#10-troubleshooting--faq).

---

## 4. Walkthrough 1 — Appointment No-Show Analysis Agent

> **Persona:** Sarah Martinez (Front Desk) / Rebecca Thompson (Office Manager)  
> **Pain Point:** 15% no-show rate costing $180K/year  
> **Time to Build:** 20–30 minutes  
> **Product Used:** Copilot Studio → Declarative Agent

### What You'll Build

A custom Copilot agent that the front desk team can chat with to:
- Get no-show rates by day, time, provider, and appointment type
- Identify tomorrow's high-risk appointments
- Generate patient reminder lists
- Calculate financial impact

### Step 4.1 — Create the Agent

1. Open [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. On the home page, click **+ Create** (top left) → **New agent**
3. You'll see the **"Describe your agent"** dialog. Enter:

   ```
   I want to create an agent that helps the front desk team at HealthBridge Medical 
   Group analyze appointment no-shows. It should be able to answer questions about 
   no-show rates, identify patterns, generate reminder lists, and calculate the 
   financial impact of missed appointments. It should be friendly, professional, 
   and always provide specific numbers from the data.
   ```

4. Click **Create**

Copilot Studio will generate a draft agent with a name, description, and instructions. You'll customize these next.

### Step 4.2 — Configure the Agent Identity

On the agent's **Overview** page, set the following:

| Field | Value |
|---|---|
| **Name** | HealthBridge Appointment Analyzer |
| **Description** | Helps the front desk and office manager analyze no-show patterns, generate reminder lists, and track financial impact of missed appointments. |
| **Icon** | Choose a calendar or medical icon |

### Step 4.3 — Write the Agent Instructions

Click on **Instructions** (or the edit pencil next to the instructions field). Replace the default with:

```
You are the HealthBridge Appointment Analyzer, an AI assistant for HealthBridge Medical Group's 
front desk and management team.

YOUR ROLE:
- Analyze appointment data to identify no-show patterns and trends
- Help the team proactively reduce no-shows
- Calculate the financial impact of missed appointments
- Generate actionable reminder and outreach lists

KEY FACTS ABOUT HEALTHBRIDGE:
- Primary care practice with ~8,000 active patients
- 5 physicians, 2 nurse practitioners, ~45,000 annual visits
- Current no-show rate is approximately 15% (target: 5%)
- Average appointment revenue: $150
- No-shows cost approximately $180K annually

WHEN ANSWERING QUESTIONS:
- Always reference specific data from the uploaded appointment and patient files
- Provide exact numbers and percentages, not vague estimates
- Break down analysis by: day of week, time of day, appointment type, and provider
- When asked about financial impact, use $150 per missed appointment
- When generating reminder lists, include patient name, phone number, appointment date/time, 
  and provider name
- Suggest specific interventions for high-risk appointments (e.g., confirmation calls, 
  overbooking slots)

PERSONA CONTEXT:
- Sarah Martinez (Front Desk) handles 80-120 calls/day and currently spends 2 hours daily 
  on manual reminder calls with only 60% patient reach
- Rebecca Thompson (Office Manager) needs operational visibility into no-show trends 
  for reporting and staffing decisions

TONE:
- Professional but approachable
- Data-driven — always lead with numbers
- Proactive — suggest next steps, don't just answer the question
```

### Step 4.4 — Add Knowledge Sources

This is where you connect the agent to the HealthBridge data.

1. In the left sidebar, click **Knowledge**
2. Click **+ Add knowledge**
3. Select **SharePoint** as the source type
4. Browse to your `HealthBridge Medical Group - Demo` SharePoint site
5. Select the `HealthBridge Data` folder (or select individual files):
   - ✅ `appointments.csv` (required)
   - ✅ `patients.csv` (required — for patient contact info)
   - ✅ `staff.csv` (helpful — maps provider IDs to names)
6. Click **Add**

> **💡 Tip:** You can also add the persona markdown files (`front_desk.md`, `office_manager.md`) as knowledge — this gives the agent rich context about the roles it's supporting.

### Step 4.5 — Add Starter Prompts

Starter prompts appear as clickable suggestions when a user opens the agent. They guide your demo audience to the best questions.

1. Go to the agent's **Overview** page
2. In the **Starter prompts** section, add:

| Starter Prompt |
|---|
| What is our current no-show rate, and how does it break down by day of week? |
| Show me tomorrow's appointments that are at high risk of no-show |
| How much revenue have we lost to no-shows this quarter? |
| Generate a reminder call list for tomorrow's appointments |

### Step 4.6 — Test the Agent

1. Click the **Test** button (bottom-right chat panel)
2. Try each of these prompts and verify the responses:

**Test 1 — Basic analysis:**
```
What is our no-show rate?
```
✅ Expected: ~15% with breakdown

**Test 2 — Pattern recognition:**
```
Which day of the week has the most no-shows?
```
✅ Expected: Identifies the highest no-show day with a percentage

**Test 3 — Financial impact:**
```
Calculate the total revenue lost to no-shows in the last 3 months
```
✅ Expected: A dollar amount based on count × $150

**Test 4 — Actionable list:**
```
Give me a list of patients with appointments tomorrow, sorted by no-show risk
```
✅ Expected: A table with patient names, times, and risk indicators

### Step 4.7 — Refine the Instructions (If Needed)

If the agent's responses are too vague or miss the data:
- Add more explicit instructions (e.g., "When asked about risk, consider patients who have previously no-showed as high-risk")
- Ensure the knowledge sources are indexed (this can take a few minutes after adding)
- Try being more specific in the instructions about the CSV column names (e.g., "The appointment status column contains values: Completed, No-Show, Cancelled, Scheduled, Checked-in")

---

## 5. Walkthrough 2 — Claim Denial Scrubbing Agent

> **Persona:** Patricia O'Brien (Billing Specialist)  
> **Pain Point:** 18% claim denial rate → $95K/month delayed revenue  
> **Time to Build:** 30–40 minutes  
> **Product Used:** Copilot Studio → Declarative Agent

### What You'll Build

A billing-team agent that:
- Analyzes denied claims to find root causes
- Validates new claims before submission
- Recommends fixes for common denial reasons
- Tracks denial rate trends

### Step 5.1 — Create the Agent

1. In Copilot Studio, click **+ Create → New agent**
2. Describe the agent:

   ```
   I want to create an agent for the billing team at a medical practice called 
   HealthBridge Medical Group. It should help billing specialists analyze claim 
   denials, identify patterns, validate claims before submission, and reduce 
   the denial rate from 18% to under 5%. It needs to understand CPT codes, 
   ICD-10 codes, and common insurance denial reasons.
   ```

3. Click **Create**

### Step 5.2 — Configure Identity

| Field | Value |
|---|---|
| **Name** | HealthBridge Claim Analyzer |
| **Description** | Helps the billing team reduce claim denials by analyzing patterns, validating claims before submission, and recommending corrections. |

### Step 5.3 — Write the Instructions

```
You are the HealthBridge Claim Analyzer, an AI assistant for the billing team at 
HealthBridge Medical Group.

YOUR ROLE:
- Analyze claim denials to identify root causes and patterns
- Validate claims before submission to catch errors
- Recommend fixes for denied claims to speed resubmission
- Track denial rates and trends over time

KEY FACTS ABOUT HEALTHBRIDGE BILLING:
- Current claim denial rate: 18% (industry average: 10-12%, target: <5%)
- Top denial reasons: Missing authorization (22%), Invalid codes (18%), 
  Not covered (15%), Eligibility issues (12%)
- 200+ denied claims in backlog
- $95K/month in delayed revenue from denials
- $120K/year in write-offs from unrecovered denials
- $8-12K monthly lost permanently to uncollectable denied claims

CLAIM VALIDATION RULES (check these before approving a claim):
1. Diagnosis code (ICD-10) must be present and valid
2. Procedure code (CPT) must be present and valid
3. Diagnosis must clinically justify the procedure
4. Patient insurance must be active and verified
5. Prior authorization must be obtained for applicable procedures
6. Patient must have a matching appointment record
7. Provider NPI must match the rendering provider
8. Timely filing — claim must be submitted within payer's deadline

WHEN ANSWERING QUESTIONS:
- Reference specific claim data from billing_claims.csv
- Group denials by reason, payer, provider, and procedure type
- Always calculate the dollar impact of findings
- When validating a claim, check ALL 8 rules and report pass/fail for each
- Suggest specific corrective actions, not generic advice
- Compare current denial rate to industry benchmarks

PERSONA CONTEXT:
- Patricia O'Brien processes 50+ claims daily
- She spends 60% of her time on denial follow-up instead of clean submissions
- Top frustration: providers submit incomplete documentation, causing preventable denials

TONE:
- Precise and detail-oriented (billing requires accuracy)
- Action-oriented — always end with "here's what to do next"
- Use billing terminology the team understands (EOB, ERA, CPT, ICD-10, A/R)
```

### Step 5.4 — Add Knowledge Sources

1. Go to **Knowledge → + Add knowledge → SharePoint**
2. Select from your HealthBridge SharePoint site:
   - ✅ `billing_claims.csv` (required)
   - ✅ `medical_records.csv` (for cross-referencing diagnoses and procedures)
   - ✅ `insurance_providers.csv` (for payer-specific rules)
   - ✅ `appointments.csv` (to verify appointments exist for claims)
   - ✅ `patients.csv` (for insurance eligibility info)
3. Optionally add `billing_specialist.md` for persona context

### Step 5.5 — Add Starter Prompts

| Starter Prompt |
|---|
| What are the top 5 reasons our claims are being denied? |
| Show me all denied claims over $500 and recommend next steps |
| What's our denial rate by insurance provider? |
| Validate this claim: CPT 99213, ICD-10 J06.9, patient PT10045, provider DR001 |

### Step 5.6 — Test the Agent

**Test 1 — Denial analysis:**
```
What's our overall claim denial rate, and how does it compare to industry average?
```
✅ Expected: 18% vs 10-12% industry average, with dollar impact

**Test 2 — Root cause:**
```
Break down our denied claims by reason. Which reason should we fix first?
```
✅ Expected: Ranked list with percentages and dollar amounts, plus a recommendation

**Test 3 — Payer analysis:**
```
Which insurance company denies the most claims? What can we do about it?
```
✅ Expected: Identifies the worst payer with specific patterns and action items

**Test 4 — Validation simulation:**
```
If I'm about to submit a claim for a follow-up visit (CPT 99213) with diagnosis 
code J06.9 (upper respiratory infection), what should I check before submitting?
```
✅ Expected: Walks through the validation rules with specific guidance

---

## 6. Walkthrough 3 — Prescription Refill Routing Agent

> **Persona:** Marcus Johnson (Medical Assistant)  
> **Pain Point:** 150+ daily refill requests consuming 3-4 hours of MA time  
> **Time to Build:** 30–40 minutes  
> **Product Used:** Copilot Studio → Declarative Agent

### What You'll Build

An agent that Medical Assistants can consult to:
- Triage refill requests into auto-approve, provider-review, or office-visit-required
- Pull patient context (last visit, current meds, diagnosis history)
- Generate provider summaries for requests needing review
- Track refill volumes and turnaround times

### Step 6.1 — Create the Agent

1. In Copilot Studio, click **+ Create → New agent**
2. Describe:

   ```
   Create an agent for medical assistants at HealthBridge Medical Group that helps 
   triage prescription refill requests. It should classify each request as 
   auto-approve, provider-review, or office-visit-required based on the patient's 
   history, last visit date, and medication type. It should pull relevant patient 
   context to help the MA or provider make quick decisions.
   ```

3. Click **Create**

### Step 6.2 — Configure Identity

| Field | Value |
|---|---|
| **Name** | HealthBridge Refill Assistant |
| **Description** | Helps MAs triage prescription refill requests by pulling patient history, classifying request urgency, and routing to the right workflow. |

### Step 6.3 — Write the Instructions

```
You are the HealthBridge Refill Assistant, an AI assistant for the medical assistant 
team at HealthBridge Medical Group.

YOUR ROLE:
- Help MAs quickly triage prescription refill requests
- Pull patient context to support decision-making
- Route requests to the correct workflow
- Reduce the 3-4 hours/day MAs spend on manual refill processing

ROUTING RULES:

Route 1 — AUTO-APPROVE (target: ~60% of requests):
  Criteria (ALL must be true):
  - Patient seen within the last 12 months
  - Medication is a routine maintenance drug (e.g., statins, blood pressure, thyroid)
  - No dosage change needed
  - Refill count has not been exhausted
  - No clinical alerts or contraindications
  Action: Approve and send to pharmacy. Notify MA for confirmation.

Route 2 — PROVIDER REVIEW (target: ~30% of requests):
  Criteria (ANY triggers this route):
  - Patient last seen 6-12 months ago AND medication requires monitoring
  - Controlled substance requiring provider sign-off
  - Dosage change requested
  - New interaction risk with other current medications
  Action: Generate a provider summary with patient context, medication history, 
  and last lab results. Route to the prescribing provider.

Route 3 — OFFICE VISIT REQUIRED (target: ~10% of requests):
  Criteria (ANY triggers this route):
  - Patient not seen in over 12 months
  - Medication requires periodic lab work that is overdue
  - New symptoms reported alongside refill request
  - Controlled substance with compliance concerns
  Action: Notify patient that a visit is needed. Offer scheduling assistance.

WHEN TRIAGING A REQUEST:
1. Look up the patient in patients.csv (by name or patient ID)
2. Check their last visit date in appointments.csv
3. Review their current medications and diagnoses in medical_records.csv
4. Apply the routing rules above
5. Present: routing decision, reasoning, patient summary, and recommended next step

PATIENT SUMMARY FORMAT:
  Patient: [Name] (ID: [ID])
  Last Visit: [Date] ([X] days ago)
  Provider: [Provider Name]
  Current Medications: [List from most recent record]
  Relevant Diagnoses: [ICD-10 codes and descriptions]
  Routing Decision: [AUTO-APPROVE / PROVIDER REVIEW / OFFICE VISIT REQUIRED]
  Reason: [Brief explanation]
  Next Step: [Specific action]

PERSONA CONTEXT:
- Marcus Johnson handles 150+ refill requests daily across phone, fax, portal, and walk-ins
- The team of 3 MAs collectively spends 9-12 hours/day on refills
- 3-5 requests per week are lost or delayed in the current paper-based system
- Only 40% of requests are completed same-day currently

TONE:
- Clinical and precise — MAs need accurate, structured information
- Efficient — minimize reading, maximize clarity
- Use the patient summary format consistently
```

### Step 6.4 — Add Knowledge Sources

1. Go to **Knowledge → + Add knowledge → SharePoint**
2. Select:
   - ✅ `medical_records.csv` (required — medication and diagnosis history)
   - ✅ `patients.csv` (required — patient lookup and demographics)
   - ✅ `appointments.csv` (required — last visit dates)
   - ✅ `staff.csv` (maps provider IDs to names for routing)
3. Optionally add `medical_assistant.md` and `prescription_management.md` for context

### Step 6.5 — Add Starter Prompts

| Starter Prompt |
|---|
| Triage a refill request for Lisinopril 10mg for patient PT10023 |
| Show me all patients who are overdue for a visit but have active prescriptions |
| How many refill requests would be auto-approvable based on current patient data? |
| Generate a provider review summary for patient PT10045's medication list |

### Step 6.6 — Test the Agent

**Test 1 — Auto-approve scenario:**
```
Patient PT10015 is requesting a refill on their blood pressure medication. 
Triage this request.
```
✅ Expected: Looks up the patient, checks last visit, and routes appropriately with the structured summary format

**Test 2 — Provider review scenario:**
```
A patient who was last seen 8 months ago is requesting a refill on a medication 
that requires monitoring. How should we handle this?
```
✅ Expected: Routes to provider review, generates context summary

**Test 3 — Office visit required:**
```
Which patients requesting refills haven't been seen in over 12 months?
```
✅ Expected: List of patients needing an office visit before refills can continue

**Test 4 — Volume analysis:**
```
Based on our patient data, estimate what percentage of refill requests could 
be auto-approved vs. needing provider review vs. requiring an office visit.
```
✅ Expected: Approximate breakdown near the 60/30/10 targets

---

## 7. Connecting Agents to Live Data Sources

The walkthroughs above use SharePoint-hosted CSVs, which is great for demos. In a real deployment, you'll connect to live systems. Here's how.

### Available Connectors in Copilot Studio

| Data Source | Connector | Use Case |
|---|---|---|
| **SharePoint** | Built-in | Documents, CSVs, knowledge bases (what we used above) |
| **Dataverse** | Built-in | Structured data (patients, appointments, claims as tables) |
| **Power Automate Flows** | Built-in | Trigger workflows (send reminders, create tasks, update records) |
| **Custom API / HTTP** | Premium | Connect to EMR systems (Epic, Cerner, Athenahealth) |
| **Azure AI Search** | Premium | Large-scale document search (thousands of records) |
| **SQL Server** | Premium | Direct database queries for practice management systems |

### Upgrading from CSV to Dataverse (Recommended for Production Demos)

For a more realistic demo that supports read/write operations:

1. **Open** [make.powerapps.com](https://make.powerapps.com)
2. **Go to** Tables → **Import → Import data**
3. **Upload** each HealthBridge CSV as a Dataverse table:
   - `patients.csv` → **HealthBridge Patients**
   - `appointments.csv` → **HealthBridge Appointments**
   - `billing_claims.csv` → **HealthBridge Claims**
   - etc.
4. **In Copilot Studio**, add a Dataverse knowledge source instead of (or in addition to) SharePoint
5. **Benefit:** Agents can now *write back* to the data (update appointment status, flag claims, etc.)

### Adding Power Automate Actions (Make the Agent Do Things)

To go beyond Q&A and make the agent take action:

1. In your agent, go to **Actions → + Add an action**
2. Select **Power Automate flow**
3. Build a flow for the action you want:

**Example Flow — Send Appointment Reminder:**
- **Trigger:** Called from Copilot Studio
- **Input:** Patient name, phone number, appointment date/time
- **Actions:**
  1. Format a reminder message
  2. Send via Outlook email (or Teams message for demo)
  3. Log the reminder in a SharePoint list
- **Output:** Confirmation message back to the agent

**Example Flow — Flag Claim for Review:**
- **Trigger:** Called from Copilot Studio
- **Input:** Claim ID, denial reason, recommended action
- **Actions:**
  1. Update claim status in Dataverse to "Under Review"
  2. Create a Planner task for the billing team
  3. Send Teams notification to Patricia O'Brien
- **Output:** Task URL and confirmation

4. Back in Copilot Studio, the agent can now call these flows during conversation

---

## 8. Publishing and Sharing Your Agent

### Publishing to Microsoft Teams (Recommended for Demos)

1. In Copilot Studio, click **Publish** (top right)
2. Click **Publish** to push the latest version
3. Go to **Channels → Microsoft Teams**
4. Click **Turn on Teams**
5. Click **Open in Teams** to test
6. To share with others: Click **Availability options → Share with specific users** and add demo attendees

### Making the Agent Available in M365 Copilot Chat

Declarative agents appear in the M365 Copilot chat as selectable personas:

1. After publishing, go to **Channels → Microsoft 365 Copilot**
2. Toggle it **On**
3. Users will see your agent listed when they click the **agent selector** (the `@` icon) in M365 Copilot chat
4. They can then chat with "HealthBridge Claim Analyzer" directly within their normal Copilot experience

### Pre-Demo Checklist

- [ ] Agent is published (no draft warning)
- [ ] All knowledge sources show "Ready" status (not "Indexing")
- [ ] Tested all starter prompts and they return good answers
- [ ] Teams channel is enabled and you've opened the agent in Teams at least once
- [ ] Demo attendees have been added to the SharePoint site (so the agent has data access)
- [ ] You have the HealthBridge persona profiles open for storytelling (Sarah, Patricia, Marcus)

---

## 9. Demo Day — Running the Presentation

### Recommended Demo Flow (45 minutes)

#### Opening — Set the Scene (5 min)

> *"Meet HealthBridge Medical Group — a primary care practice with 120 employees and 8,000 patients. They're facing the same challenges as most practices: 15% no-shows costing $180K/year, an 18% claim denial rate, and MAs drowning in 150+ prescription refills daily. Let me show you how Microsoft Copilot changes their day."*

Have `README.md` or a summary slide visible.

#### Act 1 — Instant Value with M365 Copilot (10 min)

**Show that Copilot works with data they already have:**

1. Open `billing_claims.csv` in Excel Online
2. Click the Copilot button
3. Ask: *"What's our claim denial rate, and which insurance company has the highest denial rate?"*
4. Copilot analyzes the data and shows results
5. Ask: *"Create a chart showing denials by reason"*
6. Copilot generates a chart

**Key message:** *"No setup, no coding, no IT project. The billing team opens Excel tomorrow and starts getting answers."*

#### Act 2 — Custom Agent in Copilot Studio (20 min)

**Show a purpose-built agent for Patricia's billing team:**

1. Open the HealthBridge Claim Analyzer in Teams (or M365 Copilot chat)
2. Click the first starter prompt: *"What are the top 5 reasons our claims are being denied?"*
3. Agent responds with analysis from the data
4. Ask: *"Show me all denied claims over $500 and recommend next steps for each"*
5. Agent provides actionable recommendations
6. Ask: *"If we fixed just the top 2 denial reasons, how much revenue would we recover?"*
7. Agent calculates the dollar impact

**Key message:** *"This agent is tailored for Patricia's billing team. It knows HealthBridge's data, speaks billing terminology, and always recommends next steps. This took 30 minutes to build — no code, no developers."*

#### Act 3 — The ROI Story (5 min)

Pull up the numbers:

| Improvement | Current | With Copilot | Annual Value |
|---|---|---|---|
| Claim denial rate | 18% | <5% | $80–120K |
| No-show rate | 15% | 5% | $120K |
| MA refill processing | 3-4 hrs/day | <1 hr/day | $85K |
| **Total** | | | **$285–325K** |

> *"And this is just three of the six roles we looked at. The full opportunity across HealthBridge is $500K+."*

#### Closing — Next Steps (5 min)

> *"Everything I showed you today runs on the Microsoft 365 licenses your customers likely already have. The agents took 30 minutes each to build. The question isn't whether this creates value — the data proves it does. The question is which team do we start with."*

### Demo Tips

| Do | Don't |
|---|---|
| Use the persona names — "Patricia spends 60% of her day chasing denials" | Use generic language — "the billing department has inefficiencies" |
| Show real data responses from the agent | Show slides about what the agent *could* do |
| Let the audience suggest follow-up questions to ask the agent | Script every interaction — live Q&A builds trust |
| Acknowledge when the agent gives an imperfect answer and refine the prompt | Panic if the agent hallucinates — say "let me refine that" |
| Have a backup plan (pre-captured screenshots) in case of connectivity issues | Rely 100% on live demos without a safety net |

---

## 10. Troubleshooting & FAQ

### "Copilot button doesn't appear in Excel"

- **Check licensing:** Admin Center → Users → select your user → Licenses → confirm M365 Copilot is assigned
- **Check rollout:** Your tenant may need the Copilot feature enabled in Admin Center → Settings → Copilot
- **Check file location:** The file must be in SharePoint or OneDrive, not local desktop
- **Wait:** License assignment can take up to 24 hours to propagate

### "Copilot Studio says I don't have access"

- Your admin needs to enable Copilot Studio in the Power Platform Admin Center
- Navigate to: [admin.powerplatform.microsoft.com](https://admin.powerplatform.microsoft.com) → Environments → Settings → Features → **Copilot Studio** → On
- You may need a Power Apps/Power Automate license in addition to M365 Copilot

### "The agent doesn't seem to know about my data"

- SharePoint knowledge sources take **5–15 minutes** to index after being added
- Check the **Knowledge** page — each source should show a green "Ready" status
- CSVs with more than ~5,000 rows may need to be split or loaded into Dataverse instead
- Ensure the file names and column headers are clear and descriptive

### "The agent gives vague or wrong answers"

- **Add more specific instructions** — tell the agent exactly which columns to look at and what values to expect
- **Add example Q&A pairs** — in the instructions, include: *"When asked about denial rate, look at the claim_status column in billing_claims.csv and count rows where status = 'Denied'"*
- **Simplify the question** — instead of "analyze everything," ask "what percentage of rows in billing_claims.csv have a claim_status of Denied?"
- **Check the data** — open the CSV and verify the column names match what your instructions reference

### "How is this different from ChatGPT?"

This is the #1 question you'll get. Here's your answer:

> *"Three things: First, it runs inside the tools they already use — Excel, Teams, Outlook — not a separate browser tab. Second, it has access to their organizational data in SharePoint and Dataverse with enterprise security — ChatGPT doesn't. Third, Copilot Studio agents can take action — send reminders, update records, flag claims — ChatGPT can only chat."*

### "Can I use this with real patient data?"

For demos: **No.** Use only the fictional HealthBridge data. Real patient data is protected by HIPAA and must never be uploaded to a demo tenant.

For production: **Yes**, but the customer's IT team must ensure:
- Data stays within their M365 tenant (it does by default)
- Copilot's data residency and compliance certifications meet their requirements
- A BAA (Business Associate Agreement) is in place with Microsoft
- Access controls and DLP policies are configured

### "What does this cost?"

| Component | Price (as of early 2025) | Notes |
|---|---|---|
| **Microsoft 365 Copilot** | $30/user/month | Required for each user who interacts with Copilot |
| **Copilot Studio** | Included with M365 Copilot (basic), or $200/month standalone for 25K messages | Included usage covers most small-practice needs |
| **Power Automate** | Included with M365, or $15/user/month for premium connectors | Needed only if building action flows with premium connectors |

> **💡 Note:** Always verify current pricing at [microsoft.com/copilot](https://www.microsoft.com/microsoft-365/copilot) — pricing may have changed since this guide was written.

---

## Quick Reference Card

Copy this for your demo notebook:

```
HEALTHBRIDGE QUICK STATS:
• 120 employees, 8,000 patients, $180K lost to no-shows
• 18% claim denial rate (industry avg: 10-12%)
• 150+ daily Rx refill requests consuming 3-4 MA hours
• Total opportunity: $500K+ annually

DEMO URLS:
• M365 Copilot:    microsoft365.com/copilot
• Copilot Studio:  copilotstudio.microsoft.com
• SharePoint:      [your-tenant].sharepoint.com

THREE AGENTS TO DEMO:
1. Appointment Analyzer  → Front Desk / Office Manager → $120K value
2. Claim Analyzer        → Billing Team              → $80-120K value
3. Refill Assistant      → Medical Assistants         → $85K value

KILLER DEMO PROMPTS:
• Excel:  "What's our claim denial rate by insurance provider?"
• Agent:  "Show me tomorrow's high-risk no-show appointments"
• Agent:  "Triage a Lisinopril refill for patient PT10023"
• Agent:  "If we fixed the top 2 denial reasons, how much would we recover?"

DIFFERENTIATION VS CHATGPT:
✓ Runs inside M365 tools they already own
✓ Accesses org data with enterprise security
✓ Agents take actions (not just chat)
```

---

*Built with the HealthBridge Medical Group training environment. See `README.md` for the full practice profile, `personas/` for role-based scenarios, and `docs/agent_scenarios.md` for hands-on exercises.*

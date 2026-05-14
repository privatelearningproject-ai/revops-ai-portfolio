# AI Lead Scoring Engine — Times Internet

## Overview
Built and deployed a production AI pipeline that automatically scores inbound leads, 
predicts conversion likelihood, and triggers personalised WhatsApp reactivation messages — 
processing 1,000+ leads with results still running in production.

---

## The Problem
The sales team at Times Internet was receiving high volumes of inbound leads daily with no 
consistent way to prioritise them. Reps were spending equal time on cold and hot leads, 
missing high-intent prospects, and manually deciding who to follow up with on WhatsApp.

---

## The Solution
An end-to-end AI pipeline that:
1. Pulls lead data from Salesforce via BigQuery
2. Sends it to Gemini 1.5 Flash (Vertex AI) for scoring and analysis
3. Returns a structured lead intelligence report per lead
4. Automatically decides which WhatsApp reactivation template to send (or not)
5. Pushes results back to Salesforce custom fields

---

## How it works

```
Salesforce Leads
      ↓
BigQuery (SQL query — pulls 15+ fields per lead)
      ↓
Gemini 1.5 Flash (Vertex AI)
      ↓
  ┌─────────────────────┬──────────────────────────┐
  │  Prompt 1           │  Prompt 2                │
  │  Lead Scoring       │  WhatsApp Decision       │
  │  - Score 1-10       │  - Send yes/no           │
  │  - Hot/Warm/Cold    │  - Which template        │
  │  - Conversion prob  │  - Disqualification type │
  │  - Revenue opp      │  - Suggested action      │
  └─────────────────────┴──────────────────────────┘
      ↓
Salesforce fields updated (Lead_Score__c, WhatsApp_Template_Name__c, etc.)
      ↓
WhatsApp message sent via template
```

---

## Fields analysed per lead
`Message__c` · `monthly_budgets__c` · `Industry` · `Lead_Age__c` · `LeadSource` · 
`Latest_Source__c` · `Email_Open__c` · `Reconversion_Lead__c` · `Other_Details__c` · 
`Number_of_form_submissions__c` · `Linkedin_GA_job_titles__c` · `Status` · `Company`

---

## Scoring logic (Gemini prompt)
- Base score on: message intent, budget info, email, phone, lead age, data completeness
- **+2-3 points** if message contains strong intent: *"interested in pricing", "ready to advertise", "send rate card"*
- **Deduct points** if marked "Not Interested" or lead age > 7 days
- Output: Score 1-10 + Hot/Warm/Cold + Conversion Likelihood + Revenue Opportunity 
**its was  big prompt , added  a sample above **

## WhatsApp template logic (Gemini prompt)
| Condition | Template |
|---|---|
| No response but email opened / form submitted | `no_response_checkin` |
| Budget / pricing objection | `budget_friendly_checkin` |
| Wrong role / filled by mistake | `rebootable_followup` |
| Vague or blank fields | `generic_checkin` |
| Said "not interested" / no phone | `none` — Do not contact |
| Lead Score > 6 | `generic_checkin` |

---

## Results (Production — April 2025 onwards)

| Lead Score | % of Leads | Qualification Probability |
|---|---|---|
| 8 | 1.7% | **90.9%** |
| 7 | 19.1% | **77.6%** |
| 6 | 23.4% | 33.3% |
| 5 | 22.3% | 12.3% |
| 4 | 22.6% | 3.4% |
| 3 | 10.9% | 2.8% |

**Key insight:** Leads scoring 7+ have 77-91% qualification probability vs 2-3% for scores below 4.
Sales team now prioritises score 7+ leads first — reducing wasted outreach by ~55%.

> Pipeline still running in production. 1,000+ leads processed to date.

---

## Tech stack
- **Gemini 1.5 Flash** via Vertex AI (LangChain + Google Cloud)
- **BigQuery** — data layer, SQL queries on Salesforce objects
- **Salesforce** — source and destination via API
- **Python** — LangChain, BigQueryLoader, VertexAI
- **WhatsApp Business API** — template-based messaging

---

## Impact
- Replaced manual lead prioritisation with AI scoring
- Sales reps now focus only on high-score leads
- WhatsApp reactivation automated for 1,000+ unqualified leads
- Conversion trend data used to build a Lead Scoring Dashboard shared with leadership

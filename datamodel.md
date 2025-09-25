# DealSource AI — Data Model

---

## 1. Entity Relationship Overview
The core entities are:

- **Company** → represents the startup or venture opportunity.  
- **Founder** → key individuals tied to a company.  
- **FundingRound** → captures financing events.  
- **Source** → origin of deal (Crunchbase, AngelList, Accelerator, Conference, etc.).  
- **DealRecord** → internal tracking of a deal sourced by the system.  
- **DueDiligence** → AI-enriched profile checks & scores.  
- **Recommendation** → preliminary investment outcome (Invest/Track/Pass).  
- **User** → VC analysts, partners, or syndicate members consuming reports.  

---

## 2. Tables & Attributes

### 2.1 Company
Represents each potential investment target.

| Field | Type | Description |
|-------|------|-------------|
| company_id (PK) | UUID | Unique identifier |
| name | String | Company name |
| website | String | Official website |
| description | Text | Company overview |
| hq_location | String | HQ city, state, country |
| sector | Enum (AI, SaaS, Biotech, Fintech, etc.) | Industry classification |
| sub_sector | String | More granular vertical |
| founded_year | Int | Year founded |
| stage | Enum (Idea, Pre-Seed, Seed, Series A, etc.) | Company stage |
| employees | Int | Approx. # of employees |
| linkedin_url | String | Public LinkedIn link |
| twitter_url | String | Twitter/X handle |
| crunchbase_url | String | Crunchbase profile link |
| angelist_url | String | AngelList profile link |
| last_updated | Timestamp | Last profile enrichment |

---

### 2.2 Founder
Captures information on company leadership.

| Field | Type | Description |
|-------|------|-------------|
| founder_id (PK) | UUID | Unique identifier |
| company_id (FK) | UUID | Link to company |
| name | String | Full name |
| title | String | Role (CEO, CTO, etc.) |
| linkedin_url | String | LinkedIn profile |
| background | Text | Education, past companies |
| repeat_founder | Boolean | Whether they’ve founded before |
| notable_exits | Text | Summary of past exits (if any) |

---

### 2.3 FundingRound
Tracks fundraising history.

| Field | Type | Description |
|-------|------|-------------|
| round_id (PK) | UUID | Unique identifier |
| company_id (FK) | UUID | Link to company |
| round_type | Enum (Seed, Series A, etc.) | Type of financing |
| amount_raised | Decimal | Amount raised (USD) |
| date | Date | Closing date of round |
| investors | JSON | List of investors (firms, angels) |
| lead_investor | String | Identified lead investor |
| source_id (FK) | UUID | Where this info came from |

---

### 2.4 Source
Origin of the deal or dataset.

| Field | Type | Description |
|-------|------|-------------|
| source_id (PK) | UUID | Unique identifier |
| name | String | Source name (Crunchbase, YC, etc.) |
| type | Enum (Database, Accelerator, Conference, Syndicate) | Source type |
| url | String | Source URL |
| ingestion_date | Timestamp | When data was imported |

---

### 2.5 DealRecord
Tracks when Musa Capital encounters a company.

| Field | Type | Description |
|-------|------|-------------|
| deal_id (PK) | UUID | Unique identifier |
| company_id (FK) | UUID | Link to company |
| source_id (FK) | UUID | Link to source |
| date_sourced | Timestamp | When discovered |
| analyst_assigned | String | User/analyst tracking the deal |
| status | Enum (New, In Review, Contacted, Dropped) | Deal pipeline stage |
| notes | Text | Internal analyst notes |

---

### 2.6 DueDiligence
Stores structured AI-generated and human-curated diligence.

| Field | Type | Description |
|-------|------|-------------|
| diligence_id (PK) | UUID | Unique identifier |
| company_id (FK) | UUID | Link to company |
| team_score | Int (0-100) | Quality of founding team |
| traction_score | Int (0-100) | Market traction indicators |
| market_size | Decimal | TAM estimate (USD) |
| product_maturity | Enum (Prototype, Beta, In-market) | Product readiness |
| competitive_landscape | Text | Key competitors snapshot |
| risks | Text | Identified risks |
| aligned_with_thesis | Boolean | Fit with Musa Capital investment thesis |
| diligence_summary | Text | Narrative summary |
| created_at | Timestamp | Generated on |

---

### 2.7 Recommendation
AI + analyst recommendation tied to a deal.

| Field | Type | Description |
|-------|------|-------------|
| recommendation_id (PK) | UUID | Unique identifier |
| deal_id (FK) | UUID | Link to deal record |
| recommendation | Enum (Invest, Track, Pass) | Suggested next step |
| confidence_score | Int (0-100) | AI confidence in recommendation |
| rationale | Text | Explanation of decision |
| created_by | Enum (AI, Analyst) | Who made recommendation |
| created_at | Timestamp | Date generated |

---

### 2.8 User
Represents Musa team members using the system.

| Field | Type | Description |
|-------|------|-------------|
| user_id (PK) | UUID | Unique identifier |
| name | String | Full name |
| role | Enum (Analyst, Partner, LP, Admin) | User role |
| email | String | Contact email |
| preferences | JSON | Notification/reporting preferences |

---

## 3. Relationships
- **Company → Founder**: One-to-many (a company has many founders).  
- **Company → FundingRound**: One-to-many (a company can raise multiple rounds).  
- **Company → DealRecord**: One-to-many (a company can be sourced multiple times).  
- **DealRecord → Source**: Many-to-one (deal comes from one source).  
- **DealRecord → DueDiligence**: One-to-one (each deal has one diligence record).  
- **DealRecord → Recommendation**: One-to-many (AI + analyst may both provide recommendations).  
- **User → DealRecord**: Analysts assigned to deals.  

---

## 4. Example Workflow
1. **Source Integration**: Import YC S24 cohort → creates `Company` and `Source` records.  
2. **Deal Capture**: Each new company enters as a `DealRecord`.  
3. **Diligence Engine**: AI generates a `DueDiligence` record (team, traction, market, risks).  
4. **Recommendation**: AI issues a `Recommendation` (Invest/Track/Pass). Analyst may override.  
5. **Pipeline Tracking**: `DealRecord.status` updated as the company moves forward.  

---

## 5. Extensions (Future)
- **Signals Table** → Hiring data, web traffic, social engagement.  
- **Events Table** → Conference/demo day participation.  
- **CRM Integration Table** → Links to Affinity/Salesforce records.  

# DealSource AI — Backlog

---

## Epic 1: Data Ingestion & Integration
**Goal:** Aggregate startup/company data from multiple public sources.

### User Stories
- As an **analyst**, I want to pull data from Crunchbase (free tier/API) so that I can source startups automatically.  
- As an **analyst**, I want to ingest accelerator cohort lists (YC, Techstars, 500 Startups, etc.) so that I can see emerging startups early.  
- As a **partner**, I want to include AngelList syndicate data so that I can spot co-investment opportunities.  
- As a **scout**, I want to pull conference attendee and speaker data (CES, AfroTech, Collision) so that I can track companies presenting at events.  

### Tasks
- [ ] Implement Crunchbase API connector (free tier).  
- [ ] Build scraper for YC/Techstars/other demo day cohorts.  
- [ ] Parse AngelList syndicate & rolling fund listings.  
- [ ] Scrape/export conference attendee & speaker lists (CSV, PDF parsing).  
- [ ] Normalize and clean ingested company data into unified schema.  
- [ ] Store raw + cleaned data in Postgres/Elastic DB.  

---

## Epic 2: Company Profile Builder
**Goal:** Generate structured, enriched company profiles.

### User Stories
- As an **analyst**, I want to see all relevant company data in one profile view so that I can avoid manual research.  
- As a **partner**, I want to track company sectors, stage, and funding history so that I can quickly filter by thesis fit.  
- As a **scout**, I want to check founders’ backgrounds so that I can evaluate credibility.  

### Tasks
- [ ] Define schema for `Company` entity (core details).  
- [ ] Link `Founder` data via LinkedIn enrichment.  
- [ ] Integrate funding round history from Crunchbase & press releases.  
- [ ] Add sector/industry classification (AI, SaaS, Fintech, etc.).  
- [ ] Include company website & social handles (LinkedIn, Twitter/X).  
- [ ] Auto-refresh profiles weekly.  

---

## Epic 3: Due Diligence Engine
**Goal:** Automate preliminary due diligence scoring.

### User Stories
- As an **analyst**, I want to see a quick scoring of the team, traction, and market so that I can prioritize high-potential deals.  
- As a **partner**, I want a narrative summary so that I can skim through deals efficiently.  
- As a **LP**, I want Musa’s sourcing process to be data-driven and transparent.  

### Tasks
- [ ] Implement diligence scoring dimensions: team, traction, market, product maturity.  
- [ ] Add competitor landscape snapshot (via web scraping + LLM).  
- [ ] Auto-detect risks from public data.  
- [ ] Align scoring rubric with Musa Capital’s thesis (weighting rules).  
- [ ] Generate diligence summary (LLM narrative).  
- [ ] Store diligence data in `DueDiligence` table.  

---

## Epic 4: Recommendation Engine
**Goal:** Provide AI + analyst recommendations on investment action.

### User Stories
- As an **analyst**, I want to see an “Invest / Track / Pass” label so that I know the system’s recommendation.  
- As a **partner**, I want to see a confidence score so that I can judge AI reliability.  
- As a **team**, I want AI + analyst recommendations side-by-side so that I can compare outcomes.  

### Tasks
- [ ] Implement recommendation model using diligence scores + rules.  
- [ ] Add confidence score (0–100).  
- [ ] Generate rationale text explaining recommendation.  
- [ ] Store in `Recommendation` table.  
- [ ] Enable analyst override + notes.  

---

## Epic 5: Reporting & Outputs
**Goal:** Deliver deal flow insights to Musa Capital team.

### User Stories
- As an **analyst**, I want weekly deal reports so that I can review new startups.  
- As a **partner**, I want “Top 10 weekly deals” pushed to Slack/email so that I don’t miss hot companies.  
- As an **LP**, I want evidence of proactive deal sourcing so that I see value in the fund’s process.  

### Tasks
- [ ] Generate Weekly Deal Sourcing Report (PDF/Notion).  
- [ ] Auto-publish profiles to Notion/CRM.  
- [ ] Send Slack/email alerts for high-potential companies.  
- [ ] Add filtering by sector, stage, geography in dashboard.  

---

## Epic 6: User & Access Management
**Goal:** Support collaboration within Musa Capital.

### User Stories
- As a **partner**, I want to assign deals to analysts so that sourcing is distributed.  
- As an **analyst**, I want to add internal notes to deals so that knowledge is shared.  
- As a **team**, I want role-based access so that LPs see reports but not raw data.  

### Tasks
- [ ] Define `User` schema with roles (Analyst, Partner, LP, Admin).  
- [ ] Implement user authentication (SSO/Google login).  
- [ ] Role-based access to deals & reports.  
- [ ] Add analyst assignment field in `DealRecord`.  
- [ ] Enable note-taking per deal.  

---

## Epic 7: Roadmap Expansion
**Goal:** Enhance product with predictive insights & integrations.

### User Stories
- As an **analyst**, I want LinkedIn hiring trends so that I can gauge traction.  
- As a **partner**, I want predictive deal heat scores so that I know which companies will raise soon.  
- As a **team**, I want CRM integration so that deal flow syncs with Affinity/Salesforce.  

### Tasks
- [ ] Integrate LinkedIn hiring/job postings data.  
- [ ] Track Twitter/X engagement trends.  
- [ ] Build predictive scoring model (likelihood to raise).  
- [ ] Sync with Affinity/Salesforce CRM.  
- [ ] Add founder contact/outreach module (future v2).  

---

## Epic 8: Non-Functional Requirements
**Goal:** Ensure system is robust, scalable, and compliant.

### User Stories
- As an **engineer**, I want to respect source ToS so that Musa Capital avoids compliance risks.  
- As a **partner**, I want reliable reports so that I trust the system.  
- As an **analyst**, I want fast search/filtering so that I don’t waste time.  

### Tasks
- [ ] Respect API & scraping terms of service.  
- [ ] Set refresh cycles (weekly for profiles, daily for new deals).  
- [ ] Ensure scalability (can handle 50k+ company records).  
- [ ] Implement data validation & deduplication.  
- [ ] Log ingestion errors + recovery workflows.  

---

# Milestones

### Phase 1 (0–8 weeks)
- Data ingestion (Crunchbase, AngelList, Accelerators).  
- Company profile builder (MVP).  
- Basic diligence scoring.  
- Weekly PDF report generation.  

### Phase 2 (3–6 months)
- Add conference + LinkedIn data.  
- Recommendation engine with confidence scores.  
- Slack/email alerts.  
- Analyst override + notes.  

### Phase 3 (6–12 months)
- Predictive scoring (deal heat).  
- CRM integration.  
- Outreach automation.  
- Full dashboard with filters + collaboration tools.  

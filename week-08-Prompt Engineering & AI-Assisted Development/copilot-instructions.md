# Capstone Project Context

## Project

- **Name:** Threat Intelligence Feed Dashboard
- **Team:**  
  - Jesus Alvarez — Component 1: Feed Collector  
  - Harry Yachimba — Component 2: AI Summarizer & IOC Extractor  
  - Julian Silva-Erazo — Component 3: Relevance Scorer  
  - Safayet Safin — Component 4: Integration, Testing & Presentation  

- **What it does:**  
This project aggregates cybersecurity threat information from multiple public sources and uses AI to summarize threats, extract indicators of compromise (IOCs), assess relevance to an organization’s technology stack, and present everything in a centralized dashboard. The system automates threat analysis workflows that would normally require hours of manual review by cybersecurity analysts.

- **Project type:** Threat Intelligence Feed Dashboard (Cybersecurity)

---

# Architecture

## Ingestion
Component 1 uses scheduled n8n workflows to collect cybersecurity threat data from RSS feeds, CVE databases, and public threat intelligence feeds. Data is normalized and stored inside Airtable.

### Current Sources
- The Hacker News
- BleepingComputer

### Stored Threat Fields
- title
- source
- url
- published_date
- raw_summary
- created_time

---

## AI Core

Flowise chains and Groq/Hugging Face APIs process threat entries to:

- Summarize threats
- Extract IOCs
- Classify severity
- Identify attack types
- Analyze threats
- Generate response recommendations
- Score relevance based on a technology stack

### AI Models Used
- Groq llama-3.1-8b-instant
- Groq llama-3.3-70b-versatile
- Hugging Face Inference API models

### AI-Enriched Outputs
- severity
- affected_software
- attack_type
- iocs
- enriched_at
- enriched_by
- scored

---

## Specialist

The workflows generate structured cybersecurity outputs including:

- Severity scores
- Attack classifications
- Threat summaries
- MITRE ATT&CK mappings
- Containment recommendations
- Investigation steps
- Relevance scoring

### Example Threat Types Detected
- Ransomware
- Credential Stealing
- Supply-Chain Attacks
- Vulnerability Exploitation
- Remote Code Execution (RCE)
- Phishing
- Privilege Escalation
- Malware Deployment
- Backdoor Deployment
- Zero-Day Vulnerabilities

### Example Affected Technologies
- Microsoft 365
- Windows Server
- VSCode
- Ubuntu Linux Servers
- Python
- GitHub Actions
- PAN-OS
- Enterprise IoT Devices

---

## Integration

n8n orchestrates the workflow execution between all components. Airtable stores shared records and dashboard data for monitoring and prioritization.

### Workflow Logic
1. Threat intelligence articles are collected automatically.
2. Threat records are stored inside Airtable.
3. AI workflows enrich the threats with structured intelligence.
4. Relevance scoring compares threats against the monitored technology stack.
5. The dashboard assigns:
   - relevance scores
   - response recommendations
   - monitoring priority
6. Analysts review prioritized threats through centralized dashboard views.

---

# Tech Stack

- n8n Cloud (workflow automation)
- Airtable (centralized database)
- Flowise Cloud
- Groq API
- Hugging Face Inference API
- Python
- GitHub
- VSCode
- Splunk
- Suricata
- Apache HTTP Server
- MySQL
- Google Cloud Platform
- Microsoft 365

---

# Airtable Schema

## Threats Table

| Field | Type | Written By | Status Values |
|-------|------|-----------|---------------|
| title | text | ingestion workflow | |
| source | text | ingestion workflow | |
| url | url | ingestion workflow | |
| published_date | date | ingestion workflow | |
| raw_summary | long text | ingestion workflow | |
| created_time | timestamp | Airtable | |

### Purpose
Stores raw cybersecurity threat intelligence articles collected from public sources before enrichment and scoring.

---

## Threat Enrichment Table

| Field | Type | Written By | Status Values |
|-------|------|-----------|---------------|
| enriched | checkbox | enrichment workflow | true / false |
| severity | select | Groq enrichment model | low / medium / high / critical |
| affected_software | text | enrichment workflow | |
| attack_type | text | enrichment workflow | |
| iocs | text | enrichment workflow | |
| enriched_at | timestamp | enrichment workflow | |
| enriched_by | text | Groq model | |
| scored | checkbox | scoring workflow | true / false |

### Purpose
Transforms raw cybersecurity articles into structured threat intelligence that analysts can review quickly.

---

## Relevance Scoring Table

| Field | Type | Written By | Status Values |
|-------|------|-----------|---------------|
| relevance_score | number | relevance workflow | |
| relevance_level | select | Groq scoring model | low / medium / high |
| matched_tech | text | relevance workflow | |
| relevance_reason | long text | Groq scoring model | |
| scored_at | timestamp | scoring workflow | |
| scored_by | text | Groq model | |
| current_status | select | workflow automation | scored |
| calculation | formula/text | Airtable automation | monitor / review promptly / immediate action |

### Current Scoring Logic
- Low relevance → Monitor
- Medium relevance → Review Promptly
- High relevance → Immediate Action

### Purpose
Prioritizes cybersecurity threats based on whether they directly affect technologies currently used by the organization.

---

## Tech Stack Table

| Field | Type | Written By | Status Values |
|-------|------|-----------|---------------|
| tech_name | text | analyst input | |
| category | select | analyst input | operating system / tool / cloud / database / language |
| priority | select | analyst input | high / medium |
| active | checkbox | analyst input | true / false |
| notes | long text | analyst input | |

### Current Technologies
- Windows Server
- Apache HTTP Server
- Python
- MySQL
- Microsoft 365
- Splunk
- Suricata
- iOS
- VSCode
- Windows
- Google Cloud Platform
- Ubuntu Linux Servers
- Enterprise IoT Devices
- PAN-OS
- AI Security Tools

### Purpose
Provides the monitored technology environment used for threat relevance comparison and prioritization.

---

# Airtable Base

- Shared Base: [Insert Airtable Shared Link]
- Purpose: Centralized storage for cybersecurity threats, AI enrichment outputs, relevance scoring, and analyst monitoring workflows.

---

# Conventions

- Field names use snake_case
- Status values use lowercase
- Date fields end in `_at`
- Boolean fields use checkboxes or `is_` prefixes
- Severity levels standardized as:
  - low
  - medium
  - high
  - critical
- AI-generated records include model attribution fields

---

# Current State

## What's Working
- Automated threat ingestion pipeline
- RSS feed collection
- Airtable integration
- AI-powered threat enrichment
- IOC extraction
- Severity classification
- Attack type identification
- Relevance scoring system
- Technology stack matching
- Dashboard prioritization logic
- Multi-source threat intelligence aggregation

---

## What's In Progress
- Improving relevance scoring consistency
- Expanding IOC extraction accuracy
- Enhancing dashboard visualizations
- Improving software normalization and matching
- Additional workflow automation

---

## Known Issues
- Some threat summaries lack detailed context
- Relevance scoring can occasionally create false positives
- IOC extraction consistency varies between threat sources
- Certain technologies require stronger normalization for matching

---

# Current Dataset Status

- Current Records Processed: 24+
- Total Threat Records: 40+
- AI Enrichment Status: Operational
- Relevance Scoring Status: Operational
- Dashboard Integration: Active

---

# Next Milestone

Checkpoint 2 (Week 9)

### Goals
- Complete end-to-end workflow across all threat records
- Improve scoring accuracy and prioritization
- Finalize analyst dashboard views
- Enhance automation reliability
- Improve AI-generated response recommendations
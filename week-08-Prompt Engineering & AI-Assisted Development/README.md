# Component 3: Relevance Scorer

## What it does
The Relevance Scorer evaluates enriched threat records against the organization’s monitored technology stack and assigns a relevance score and priority level. It transforms raw and AI-enriched threat intelligence into actionable risk signals by matching affected technologies and generating a concise relevance rationale.

## How it connects to other components
- Inputs:
  - Enriched threat records from Component 2 (AI Summarizer & IOC Extractor), including fields like `severity`, `affected_software`, `attack_type`, and `iocs`.
  - Monitored technology inventory from the `Tech Stack` table, including active software, platforms, and services.
  - Raw threat metadata from Component 1 ingestion, such as `title`, `source`, `url`, `published_date`, and `raw_summary`.
- Outputs:
  - Relevance scoring fields written back to Airtable:
    - `relevance_score`
    - `relevance_level`
    - `matched_tech`
    - `relevance_reason`
    - `scored_at`
    - `scored_by`
    - `current_status`
    - `calculation`
  - Status updates that allow the dashboard and analysts to prioritize threats as `monitor`, `review promptly`, or `immediate action`.

## Setup instructions

### Required accounts and keys
- **n8n Cloud**: to orchestrate the automation workflows.
- **Airtable**: to store threat records, enrichment outputs, scoring results, and the technology stack.
- **Flowise Cloud**: to run the relevance scoring model chain and scoring prompt.
- **Groq API key**: if Flowise is configured to use Groq inference for scoring.
- **Hugging Face Inference API key**: if the scoring flow uses Hugging Face model endpoints.
- **Airtable API key**: to allow n8n to read from and write to the Airtable base.

### n8n configuration
1. Create or update the workflow that runs after AI enrichment completes.
2. Add an Airtable node to read threat records that have `enriched = true` and `scored = false`.
3. Add another Airtable node to fetch the current active entries from the `Tech Stack` table.
4. Pass enriched threat data and active tech stack data into the Flowise scoring node.
5. Configure the Flowise node to call the relevance scoring model and return structured fields.
6. Add an Airtable update node to write the returned scoring fields back into the `Relevance Scoring` table and set `scored = true`.
7. Optionally add notification or dashboard update nodes for high-relevance results.

### flowise configuration
1. Create a scoring pipeline that accepts:
   - threat title
   - raw summary
   - severity
   - affected software
   - attack type
   - extracted IOCs
   - monitored tech stack list
2. Configure the prompt to compare incoming threat metadata against the monitored technology inventory and produce:
   - `relevance_score` (numeric)
   - `relevance_level` (`low`, `medium`, `high`)
   - `matched_tech`
   - `relevance_reason`
3. Map the model outputs to Airtable fields using structured output formatting.
4. Set the model attribution field `scored_by` to identify the Flowise/Groq or Hugging Face scoring model used.

### Airtable schema requirements
- `Threats Table` must contain raw threat fields.
- `Threat Enrichment Table` must contain enrichment fields such as `severity`, `affected_software`, `attack_type`, and `iocs`.
- `Relevance Scoring Table` must contain:
  - `relevance_score`
  - `relevance_level`
  - `matched_tech`
  - `relevance_reason`
  - `scored_at`
  - `scored_by`
  - `current_status`
  - `calculation`
- `Tech Stack Table` must include active monitored technologies and categories.

## Notes
- Keep the technology inventory up to date so relevance scoring remains accurate.
- Use consistent naming in Airtable fields and status values to ensure workflow mappings remain stable.
- Configure the `calculation` formula or automation in Airtable to translate `relevance_level` into analyst actions like `monitor`, `review promptly`, or `immediate action`.

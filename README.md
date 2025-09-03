# cti-pipeline

Toolkit for building a practical CTI ingestion and normalization pipeline. 
- collect open CTI feeds
- map raw feed records to a compact canonical schema (STIX-lite) that requires an event-level Diamond Model object
- enrich and score indicators to prioritize analyst work
- export sanitized context for detection engineering and threat hunting

This repository contains no malware samples, no production credentials, and no customer-identifying data.

## What's included
- `specs/canonical_cti.json` — canonical STIX-lite schema with a Diamond Model object. The schema requires `diamond_id`, `observed_time`, `confidence`, and `provenance` for every record. The normalizer will auto-create a minimal diamond when possible; enrichment fills the rest.
- `indicators/` — sanitized indicator fixtures (canonical JSON files).
- `feed-registry.csv` — curated list of free feeds and short vetting notes.
- `docs/` — operational notes: schema annotation, repository map and diamond policy.
- `tooling/` — placeholder for collectors, normalizer and enrichment code to be implemented.

## Quickstart — validate fixtures
1. Setup:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r tooling/requirements.txt

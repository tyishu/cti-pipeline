# Schema annotation

This document explains `specs/canonical_cti.json` and the role of the required `diamond model` object.

Key points:
- The canonical schema is compact (STIX-lite). Core fields: `id`, `type`, `observable_type`, `value`, `normalized_on`, `sources`, and `diamond`.
- `diamond` is required and must include:
  - `diamond_id` — canonical event identifier (deterministic),
  - `observed_time` — the observation timestamp,
  - `confidence` — integer 0 to 100,
  - `provenance` — array of source references (feed ids, parser version).

Operational notes:
- The normalizer should auto-generate a minimal diamond with deterministic `diamond_id` and minimal provenance even when only a single observable is present.
- Enrichment should populate `infrastructure` (ips/domains/asn), `capability` (malware/tool + ATT&CK techniques), and `victim` (asset tags) over time.
- Attribution labels from vendors would be stored under `adversary` with an associated `confidence` and `references`.

Example mapping guidance (short):
- If feed contains `ip` → set `diamond.infrastructure.ips`.
- If feed contains `campaign` → set `diamond.adversary.name` and `diamond.adversary.confidence` according to feed trust.
- If feed contains `sample_hash` → set `diamond.capability.name` and attach `evidence`.

Use the diamond to:
- boost scoring when infra is reused in high-confidence diamonds,
- filter hunts by ATT&CK technique or victim asset tag,
- export relationships to OpenCTI or MISP stubs.

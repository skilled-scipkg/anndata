---
name: anndata-index
description: This skill should be used when users ask how to use anndata and the correct generated documentation skill must be selected before going deeper into source code.
---

# anndata Skills Index

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Quick routing bootstrap:
```bash
find skills -maxdepth 2 -name SKILL.md | sort
```
Validation checkpoint: confirm target topic skill exists before opening docs/source maps.

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer docs-first routing; escalate to source only after the selected skill’s references are exhausted.
- Prioritize core skills for common simulation flows; use advanced topics for narrow one-doc themes.

## Generated topic skills
- `anndata-api-and-scripting`: Public API surfaces, IO entry points, accessors, and extension namespaces.
- `anndata-parallel-hpc`: zarr-v3 workflows, lazy/remote IO, sharding/chunking, and performance-oriented storage tuning.
- `anndata-release-notes`: Version deltas, upgrade impact, and change-driven risk triage.
- `anndata-tests`: Backward-compat fixture strategy, warning assertions, and regression-oriented IO testing.
- `anndata-troubleshooting`: Runtime failure diagnosis across IO compatibility, warnings, and legacy formats.
- `anndata-typing`: Public typing aliases and annotation boundaries across API/IO paths.
- `anndata-advanced-topics`: Consolidated narrow topics (benchmarks, concatenation, tutorials index, fileformat prose, interoperability, references, contributors, docs index).

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `docs/tutorials`

## Test roots for behavior checks
- `tests`
- `src/anndata/tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search the topic skill `references/doc_map.md`.
- If documentation still leaves ambiguity, open `references/source_map.md` inside the same topic skill and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" src/anndata tests`).

## Source directories for deeper inspection
- `src/anndata`
- `src/testing/anndata`

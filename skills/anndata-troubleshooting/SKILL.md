---
name: anndata-troubleshooting
description: This skill should be used when users ask about troubleshooting in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: Troubleshooting

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (legacy-warning reproduction):
```bash
python - <<'PY'
from pathlib import Path
import warnings
import anndata as ad

pth = Path("tests/data/archives/v0.5.0/adata.h5ad")
with warnings.catch_warnings(record=True) as seen:
    warnings.simplefilter("always")
    ad.read_h5ad(pth)
print("warnings:", len(seen))
PY
```
Validation checkpoint: confirm warning/emission profile before modifying compatibility code or settings.

## High-Signal Playbook

### Route conditions
- Route to `anndata-release-notes` when the main need is upgrade/change impact analysis.
- Route to `anndata-api-and-scripting` when the issue is primarily API usage, not failure diagnosis.
- Route to `anndata-parallel-hpc` for zarr-v3 performance/sharding/consolidation tuning.

### Triage questions
- What exact exception/warning text appears, and on which operation?
- Was the file written by an older or newer anndata version?
- Is the failing path `h5ad`, `zarr`, `read_elem`, or `write_elem`?
- Is the data store consolidated, legacy, or partially migrated?
- Are old-format warnings expected for this fixture?
- Can the issue be reproduced with a minimal archive fixture?

### Canonical workflow
1. Start with IO compatibility warning context in `docs/release-notes/0.8.0.md`.
2. Reproduce with smallest possible input (often `tests/data/archives/v0.5.0/adata.h5ad`).
3. Distinguish expected legacy warnings from true regressions.
4. Trace read/write path through `src/anndata/_io/h5ad.py` and `src/anndata/_io/zarr.py`.
5. Inspect legacy helpers and warning categories in `_io/utils.py`, `compat/__init__.py`, and `_warnings.py`.
6. Apply fix (rewrite file, adjust settings, update caller assumptions), then retest.

### Minimal working example
```python
from pathlib import Path
import warnings

import anndata as ad

pth = Path("tests/data/archives/v0.5.0/adata.h5ad")
with warnings.catch_warnings(record=True) as seen:
    warnings.simplefilter("always")
    adata = ad.read_h5ad(pth)

adata.write_h5ad("rewritten.h5ad")
```

### Pitfalls and fixes
- 0.8.0 changed on-disk format tags; older anndata versions cannot read all newer files (`docs/release-notes/0.8.0.md`).
- Legacy files can legitimately emit `OldFormatWarning`/`FutureWarning`; assert expected warnings instead of suppressing blindly (`tests/test_io_warnings.py`).
- Legacy and current raw encodings can conflict; inspect `_read_legacy_raw` handling (`src/anndata/_io/utils.py`).
- Fixed-length string decoding differences across ecosystems can surface in compat paths (`src/anndata/compat/__init__.py`).
- Forward slashes in keys can warn/error depending on settings and backend (`tests/test_readwrite.py`, `src/anndata/_settings.py`).
- Experimental APIs may change; avoid depending on undocumented stability (`docs/api.md`, experimental warning).

### Convergence/validation checks
- Confirm warning profile: old fixtures warn, newly written fixtures do not.
- Verify both `read_h5ad` and `read_zarr` paths for the same fixture when available.
- Run targeted backward-compat tests after applying fixes.
- Ensure rewritten files are readable without compatibility-only code paths.

## Scope
- Handle questions about known issues, diagnostics, and debugging patterns.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/release-notes/0.8.0.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`
- `src/anndata/tests`

## Optional deeper inspection
- `src/anndata`
- `src/testing/anndata`

## Source entry points for unresolved issues
- `src/anndata/_io/h5ad.py` (`read_h5ad`, `read_h5ad_backed`, `write_h5ad`)
- `src/anndata/_io/zarr.py` (`read_zarr`, `write_zarr`, `is_group_consolidated`)
- `src/anndata/_io/utils.py` (`_read_legacy_raw`, `report_read_key_on_error`, `report_write_key_on_error`)
- `src/anndata/compat/__init__.py` (`_read_attr`, `_from_fixed_length_strings`, `_decode_structured_array`)
- `src/anndata/_warnings.py` (`OldFormatWarning`, `warn`)
- `src/anndata/_settings.py` (format and forward-slash setting validation paths)
- `tests/test_io_warnings.py` (`test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`)
- `tests/test_io_backwards_compat.py` (`test_backwards_compat_files`)
- `tests/test_readwrite.py` (`test_read_full_io_error`, `test_readwrite_roundtrip`)
- Prefer targeted source search (for example: `rg -n "OldFormatWarning|legacy|backwards compat|read_h5ad|read_zarr" src/anndata tests`).

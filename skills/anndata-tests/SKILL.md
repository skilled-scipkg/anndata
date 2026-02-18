---
name: anndata-tests
description: This skill should be used when users ask about tests in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: Tests

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (focused compatibility test):
```bash
python -m pytest -q tests/test_io_warnings.py -k old_format_warning
```
Validation checkpoint: ensure warning tests pass before expanding to full IO/backward-compat suite.

## High-Signal Playbook

### Route conditions
- Route to `anndata-release-notes` when the question is "what changed" instead of "how is it tested".
- Route to `anndata-troubleshooting` when there is a failing runtime path that needs diagnosis.
- Route to `anndata-api-and-scripting` for API design usage outside regression strategy.

### Triage questions
- Are you validating backward compatibility, round-trip fidelity, or warning behavior?
- Is the target format `h5ad`, `zarr`, or both?
- Which archive version is relevant (for example `tests/data/archives/v0.11.4` or `tests/data/archives/v0.7.8`)?
- Should old-format warnings be expected or treated as failures?
- Do you need external tools (`h5diff`) or optional deps (`scanpy`)?

### Canonical workflow
1. Start from archive docs in `tests/data/archives/readme.md`.
2. Pick archive fixtures and expected support level.
3. Load both `h5ad` and `zarr` variants when available.
4. Compare with strict equality helpers.
5. Validate warning behavior for old vs current format files.
6. Add targeted regression tests before broad test runs.
7. Escalate to IO implementation files only when test intent is unclear.

### Minimal working example
```python
from pathlib import Path

import anndata as ad
import zarr

archive = Path("tests/data/archives/v0.11.4")
from_h5ad = ad.read_h5ad(archive / "adata.h5ad")
with zarr.storage.ZipStore(archive / "adata.zarr.zip") as store:
    from_zarr = ad.read_zarr(store)
```

```bash
uvx '--with=anndata==0.11.4' '--with=zarr<3' python -c '
import zarr
from anndata import AnnData
adata = AnnData(shape=(10, 20))
adata.write_zarr(zarr.ZipStore("tests/data/archives/v0.11.4/adata.zarr.zip"))
adata.write_h5ad("tests/data/archives/v0.11.4/adata.h5ad")'
```

### Pitfalls and fixes
- `v0.5.0` fixtures are structurally different and intentionally xfailed for some checks (`tests/test_io_backwards_compat.py`).
- Archive fixtures are for backward compatibility, not performance or modern-feature coverage (`tests/data/archives/readme.md`).
- Old files should emit old-format warnings; do not blanket-ignore without intent (`tests/test_io_warnings.py`).
- `h5diff` checks can be skipped outside CI unless tool is installed (`tests/test_io_backwards_compat.py`).
- Optional `scanpy` dependency gates legacy zarr tests (`tests/test_readwrite.py`).
- Zarr fixture creation for 0.11.4 requires `zarr<3` in its generation recipe (`tests/data/archives/v0.11.4/readme.md`).

### Convergence/validation checks
- Compare `h5ad` vs `zarr` loaded objects for archive fixtures.
- Assert no `OldFormatWarning` on freshly written current-format files.
- Validate warning categories/messages for known legacy fixtures.
- Run IO/backward-compat tests after any serialization-path change.

## Scope
- Handle questions about documentation grouped under the 'tests' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `tests/data/archives/readme.md`
- `tests/data/archives/v0.11.4/readme.md`
- `tests/data/archives/v0.5.0/readme.md`

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
- `tests/test_io_backwards_compat.py` (`read_archive`, `test_backwards_compat_files`, `test_no_diff`)
- `tests/test_io_warnings.py` (`test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`)
- `tests/test_readwrite.py` (`test_readwrite_roundtrip`, `test_readwrite_equivalent_h5ad_zarr`, `test_zarr_compression`)
- `src/anndata/_io/h5ad.py` (`read_h5ad`, `write_h5ad`)
- `src/anndata/_io/zarr.py` (`read_zarr`, `write_zarr`)
- `src/anndata/_io/utils.py` (`report_read_key_on_error`, `_read_legacy_raw`)
- `src/anndata/_warnings.py` (`OldFormatWarning`, `warn`)
- `tests/data/archives/readme.md` (archive-fixture policy and constraints)
- Prefer targeted source search (for example: `rg -n "backwards_compat|OldFormatWarning|read_h5ad|read_zarr" tests src/anndata`).

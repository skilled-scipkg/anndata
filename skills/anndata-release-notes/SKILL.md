---
name: anndata-release-notes
description: This skill should be used when users ask about release notes in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: Release Notes

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (upgrade triage input set):
```bash
python - <<'PY'
from importlib.metadata import version
print("installed anndata:", version("anndata"))
PY
rg -n '^## 0\\.' docs/release-notes/*.md | sed -n '1,20p'
```
Validation checkpoint: collect current version plus release-note files in upgrade span before mapping behavior changes.

## High-Signal Playbook

### Route conditions
- Route to `anndata-troubleshooting` for active runtime failures needing diagnosis.
- Route to `anndata-api-and-scripting` for API usage questions not tied to version deltas.
- Route to `anndata-parallel-hpc` when the change is specifically zarr-v3/lazy IO performance behavior.

### Triage questions
- What is the current installed version and the target version?
- Is the concern a bug fix, behavior change, performance, or deprecation?
- Does it involve IO compatibility (`h5ad`/`zarr`) or type/settings semantics?
- Which release-note files between current and target versions are in scope?
- Is there an existing failing test/warning tied to the upgrade?

### Canonical workflow
1. Start with `docs/release-notes/index.md` and enumerate all version files in the upgrade span.
2. Extract relevant bullet points by surface area (IO, lazy IO, warnings, settings, typing).
3. Map each change to concrete code paths via `references/source_map.md`.
4. Prioritize breaking/warning changes before performance-only changes.
5. Build an upgrade checklist and expected behavioral diffs.
6. Validate with targeted tests on changed surfaces.

### Minimal working example
```bash
python - <<'PY'
from importlib.metadata import version
print(version("anndata"))
PY

rg -n "^### 0\\." docs/release-notes
```

```bash
rg -n "copy_on_write_X|read_elem_lazy|floating point indices|OldFormatWarning" docs/release-notes
```

### Pitfalls and fixes
- Skipping intermediate release files misses cumulative behavior changes; scan every version in range (`docs/release-notes/index.md`).
- `anndata.__version__` is deprecated; use `importlib.metadata.version("anndata")` (`src/anndata/__init__.py`).
- 0.8.0 changed on-disk format semantics; older anndata versions cannot read all new files (`docs/release-notes/0.8.0.md`).
- 0.11.2 errors on non-integer float indices; update caller code accordingly (`docs/release-notes/0.11.2.md`).
- 0.12.1 lazy chunk behavior changed; revalidate chunk assumptions (`docs/release-notes/0.12.1.md`).
- 0.12.10 introduces `settings.copy_on_write_X` for forward compatibility; verify view-write expectations (`docs/release-notes/0.12.10.md`).

### Convergence/validation checks
- Confirm upgrade notes are mapped to corresponding code files and tests.
- Run targeted IO/backward-compat tests before and after version bump.
- Capture warning deltas (`OldFormatWarning`, `FutureWarning`) for regression review.
- Verify settings and defaults changed by release notes are explicitly pinned when needed.

## Scope
- Handle questions about documentation grouped under the 'release-notes' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/release-notes/index.md`
- `docs/release-notes/0.12.10.md`
- `docs/release-notes/0.12.9.md`
- `docs/release-notes/0.12.8.md`
- `docs/release-notes/0.12.2.md`
- `docs/release-notes/0.12.1.md`
- `docs/release-notes/0.11.2.md`
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
- `src/anndata/__init__.py` (`__getattr__` for deprecated `__version__`)
- `src/anndata/_settings.py` (`validate_zarr_write_format`, `validate_zarr_sharding`, `copy_on_write_X` registration)
- `src/anndata/_io/specs/registry.py` (`read_elem_lazy`, `read_elem_partial`)
- `src/anndata/_io/zarr.py` (`read_zarr`, `write_zarr`, old-format warning paths)
- `src/anndata/_io/h5ad.py` (`read_h5ad`, `write_h5ad`, legacy dataframe readers)
- `src/anndata/_warnings.py` (`OldFormatWarning`, `ExperimentalFeatureWarning`, `warn`)
- `tests/test_io_backwards_compat.py` (`test_backwards_compat_files`, `test_no_diff`)
- `tests/test_io_warnings.py` (`test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`)
- `tests/lazy/test_read.py` (lazy-read regressions tied to 0.12.x changes)
- Prefer targeted source search (for example: `rg -n "copy_on_write_X|read_elem_lazy|OldFormatWarning|backwards compat" src/anndata tests`).

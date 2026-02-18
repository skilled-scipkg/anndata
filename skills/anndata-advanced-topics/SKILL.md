---
name: anndata-advanced-topics
description: This skill should be used for narrowly scoped one-doc topics (benchmarks, concatenation, fileformat prose, interoperability, references, contributors, and docs index navigation) that were consolidated to reduce routing noise.
---

# anndata: Advanced Topics

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (concat behavior check):
```bash
python - <<'PY'
import numpy as np
import anndata as ad

a = ad.AnnData(np.ones((2, 3)))
b = ad.AnnData(np.zeros((1, 3)))
c = ad.concat([a, b], axis=0, join="inner")
print(c.shape)
PY
```
Validation checkpoint: concatenation smoke test should return `(3, 3)` before investigating edge-case merge behavior.

## Scope
- Consolidated router for narrow topics that were previously one-doc standalone skills.
- Use this skill when the request is specific but not frequent enough for a dedicated core playbook.

## Route the request (subtopic map)
- Benchmarks: `docs/benchmarks.md`
- Concatenation behavior/docs: `docs/concatenation.rst`
- Tutorials index navigation: `docs/tutorials/index.md`
- File format prose/spec overview: `docs/fileformat-prose.md`
- Package docs index/general orientation: `docs/index.md`
- Cross-language interoperability notes (R/Julia): `docs/interoperability.md`
- Maintainer/contributor references: `docs/_key_contributors.rst`
- External/citation references: `docs/references.rst`

## Primary documentation references
- `docs/benchmarks.md`
- `docs/concatenation.rst`
- `docs/tutorials/index.md`
- `docs/fileformat-prose.md`
- `docs/index.md`
- `docs/interoperability.md`
- `docs/_key_contributors.rst`
- `docs/references.rst`

## Workflow
- Start with the exact subtopic doc above.
- If the question spans multiple subtopics, answer with a short cross-doc synthesis and cite each doc path.
- If behavior details are unclear, inspect `references/source_map.md` entry points for the relevant subtopic.
- Keep this skill concise; route broad API/HPC/troubleshooting/release work to dedicated core skills.

## Source entry points for unresolved issues
- `src/anndata/_core/merge.py` (`concat`, `merge_nested`, `check_combinable_cols`)
- `src/anndata/experimental/merge.py` (`concat_on_disk`, `_concat_on_disk_inner`)
- `src/anndata/_io/specs/registry.py` (`IOSpec`, `read_elem`, `read_elem_lazy`, `write_elem`)
- `src/anndata/_io/specs/methods.py` (`write_anndata`, `read_anndata`, `read_partial`)
- `src/anndata/_io/h5ad.py` (`read_h5ad`, `write_h5ad`)
- `src/anndata/_io/zarr.py` (`read_zarr`, `write_zarr`)
- `src/anndata/compat/__init__.py` (`_read_attr`, `_from_fixed_length_strings`, `_decode_structured_array`)
- `src/anndata/_core/anndata.py` (`AnnData.concatenate`, `AnnData.write_h5ad`, `AnnData.write_zarr`)
- `benchmarks/benchmarks/readwrite.py` (`H5ADReadSuite`, `H5ADWriteSuite`, `H5ADBackedWriteSuite`)
- Prefer targeted source search (for example: `rg -n "concat|encoding|interop|reference|benchmark" src/anndata`).

# Evidence: anndata-parallel-hpc

## Primary docs
- `docs/tutorials/zarr-v3.md`
- `docs/contributing.md`
- `docs/release-notes/0.12.1.md`
- `docs/release-notes/0.11.2.md`

## Primary source entry points
- `skills/anndata-parallel-hpc/references/doc_map.md`
- `src/anndata/_io/zarr.py`
- `src/anndata/__init__.py`
- `src/anndata/experimental/__init__.py`
- `src/anndata/compat/__init__.py`
- `src/anndata/acc/__init__.py`
- `src/anndata/_io/__init__.py`
- `src/anndata/_core/__init__.py`
- `src/anndata/experimental/pytorch/__init__.py`
- `src/anndata/experimental/multi_files/__init__.py`
- `src/anndata/experimental/backed/__init__.py`
- `src/anndata/_io/specs/__init__.py`
- `src/anndata/_core/anndata.py`
- `src/testing/anndata/__init__.py`
- `src/anndata/utils.py`
- `src/anndata/typing.py`
- `src/anndata/types.py`
- `src/anndata/logging.py`
- `src/anndata/io.py`
- `src/anndata/abc.py`

## Extracted headings
- zarr-v3 Guide/Roadmap
- Consolidated Metadata
- Remote data
- Local data
- Codecs
- Dask
- GPU i/o
- Asynchronous i/o
- Contributing
- CI
- GPU CI
- 0.12.1 {small}`2025-07-23`

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- In this example, the store was opened unconsolidated (trying to open it as a consolidated store would error out), edited, and then reconsolidated.
- - Error out on floating point indices that are not actually integers {user}`ilan-gold` ({pr}`1746`)

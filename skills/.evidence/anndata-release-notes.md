# Evidence: anndata-release-notes

## Primary docs
- `docs/release-notes/index.md`
- `docs/release-notes/0.7.0.md`
- `docs/release-notes/0.12.2.md`
- `docs/release-notes/0.9.2.md`
- `docs/release-notes/0.9.1.md`
- `docs/release-notes/0.9.0.md`
- `docs/release-notes/0.7.8.md`
- `docs/release-notes/0.7.7.md`
- `docs/release-notes/0.7.6.md`
- `docs/release-notes/0.7.5.md`
- `docs/release-notes/0.7.4.md`
- `docs/release-notes/0.7.3.md`

## Primary source entry points
- `skills/anndata-release-notes/references/doc_map.md`
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
- `src/anndata/_warnings.py`

## Extracted headings
- Release notes
- 0.7.0 {small}`22 January, 2020`
- 0.12.2 {small}`2025-08-11`
- Bug fixes
- 0.9.2 {small}`2023-07-25`
- 0.9.1 {small}`2023-04-11`
- 0.9.0 {small}`2023-04-11`
- 0.7.8 {small}`9 November, 2021`
- 0.7.7 {small}`9 November, 2021`

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- ```{warning}
- - Better error messages during IO {pr}`734` {user}`flying-sheep`, {user}`ivirshup`
- - Fix warning from `rename_categories` {pr}`790` {smaller}`I Virshup`
- - Fixed propagation of import error when importing `write_zarr` but not all dependencies are installed {pr}`579` {smaller}`R Hillje`

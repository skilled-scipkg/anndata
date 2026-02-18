# anndata documentation map: Parallel and HPC

Generated from documentation roots:
- `docs`
- `docs/tutorials`
- `tests`
- `src/anndata/tests`

Total docs grouped in this topic: 4

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

## Verify mapped docs exist
```bash
for p in docs/tutorials/zarr-v3.md docs/contributing.md docs/release-notes/0.12.1.md docs/release-notes/0.11.2.md; do
  test -f "$p" || echo "missing: $p"
done
```

## File inventory
- `docs/tutorials/zarr-v3.md` | title: zarr-v3 Guide/Roadmap | headings: zarr-v3 Guide/Roadmap; Consolidated Metadata; Remote data
- `docs/contributing.md` | title: Contributing | headings: Contributing; CI; GPU CI
- `docs/release-notes/0.12.1.md` | title: 0.12.1 {small}`2025-07-23` | headings: 0.12.1 {small}`2025-07-23`; Bug fixes; Performance
- `docs/release-notes/0.11.2.md` | title: 0.11.2 {small}`2025-01-07` | headings: 0.11.2 {small}`2025-01-07`; Performance

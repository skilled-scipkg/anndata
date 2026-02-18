# anndata documentation map: API and Scripting

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
for p in docs/api.md docs/accessors.rst docs/_templates/autosummary/class.rst docs/_templates/autosummary/class-minimal.rst; do
  test -f "$p" || echo "missing: $p"
done
```

## File inventory
- `docs/api.md` | title: API | headings: API; Combining; Reading
- `docs/accessors.rst` | title: Accessors and paths | headings: Accessors and paths; API & Glossary; Extending accessors
- `docs/_templates/autosummary/class.rst` | title: Class | headings: (no heading extracted)
- `docs/_templates/autosummary/class-minimal.rst` | title: Class Minimal | headings: (no heading extracted)

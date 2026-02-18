# anndata documentation map: Release Notes

Generated from documentation roots:
- `docs`
- `docs/tutorials`
- `tests`
- `src/anndata/tests`

Total docs grouped in this topic: 47

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

## Verify mapped docs exist
```bash
test -f docs/release-notes/index.md || echo "missing: docs/release-notes/index.md"
find docs/release-notes -maxdepth 1 -name '*.md' | sort | sed -n '1,20p'
```

## File inventory
- `docs/release-notes/index.md` | title: Release notes | headings: Release notes; ```{release-notes} .
- `docs/release-notes/0.7.0.md` | title: 0.7.0 {small}`22 January, 2020` | headings: 0.7.0 {small}`22 January, 2020`; - The old deprecated attributes `.smp*`. `.add` and `.data` have been removed.
- `docs/release-notes/0.12.2.md` | title: 0.12.2 {small}`2025-08-11` | headings: 0.12.2 {small}`2025-08-11`; Bug fixes
- `docs/release-notes/0.9.2.md` | title: 0.9.2 {small}`2023-07-25` | headings: 0.9.2 {small}`2023-07-25`
- `docs/release-notes/0.9.1.md` | title: 0.9.1 {small}`2023-04-11` | headings: 0.9.1 {small}`2023-04-11`
- `docs/release-notes/0.9.0.md` | title: 0.9.0 {small}`2023-04-11` | headings: 0.9.0 {small}`2023-04-11`
- `docs/release-notes/0.7.8.md` | title: 0.7.8 {small}`9 November, 2021` | headings: 0.7.8 {small}`9 November, 2021`
- `docs/release-notes/0.7.7.md` | title: 0.7.7 {small}`9 November, 2021` | headings: 0.7.7 {small}`9 November, 2021`
- `docs/release-notes/0.7.6.md` | title: 0.7.6 {small}`11 April, 2021` | headings: 0.7.6 {small}`11 April, 2021`
- `docs/release-notes/0.7.5.md` | title: 0.7.5 {small}`12 November, 2020` | headings: 0.7.5 {small}`12 November, 2020`
- `docs/release-notes/0.7.4.md` | title: 0.7.4 {small}`10 July, 2020` | headings: 0.7.4 {small}`10 July, 2020`
- `docs/release-notes/0.7.3.md` | title: 0.7.3 {small}`20 May, 2020` | headings: 0.7.3 {small}`20 May, 2020`
- `docs/release-notes/0.7.2.md` | title: 0.7.2 {small}`15 May, 2020` | headings: 0.7.2 {small}`15 May, 2020`
- `docs/release-notes/0.6.x.md` | title: 0.6.\* {small}`2019-*-*` | headings: 0.6.\* {small}`2019-*-*`
- `docs/release-notes/0.6.0.md` | title: 0.6.0 {small}`1 May, 2018` | headings: 0.6.0 {small}`1 May, 2018`
- `docs/release-notes/0.5.0.md` | title: 0.5.0 {small}`9 February, 2018` | headings: 0.5.0 {small}`9 February, 2018`
- `docs/release-notes/0.4.0.md` | title: 0.4.0 {small}`23 December, 2017` | headings: 0.4.0 {small}`23 December, 2017`
- `docs/release-notes/0.12.9.md` | title: 0.12.9 {small}`2026-01-29` | headings: 0.12.9 {small}`2026-01-29`
- `docs/release-notes/0.12.8.md` | title: 0.12.8 {small}`2026-01-27` | headings: 0.12.8 {small}`2026-01-27`
- `docs/release-notes/0.12.7.md` | title: 0.12.7 {small}`2025-12-16` | headings: 0.12.7 {small}`2025-12-16`
- `docs/release-notes/0.12.6.md` | title: 0.12.6 {small}`2025-11-06` | headings: 0.12.6 {small}`2025-11-06`
- `docs/release-notes/0.12.5.md` | title: 0.12.5 {small}`2025-11-03` | headings: 0.12.5 {small}`2025-11-03`
- `docs/release-notes/0.12.4.md` | title: 0.12.4 {small}`2025-10-27` | headings: 0.12.4 {small}`2025-10-27`
- `docs/release-notes/0.12.3.md` | title: 0.12.3 {small}`2025-10-16` | headings: 0.12.3 {small}`2025-10-16`
- `docs/release-notes/0.12.10.md` | title: 0.12.10 {small}`2026-02-06` | headings: 0.12.10 {small}`2026-02-06`
- `docs/release-notes/0.12.0.md` | title: 0.12.0 {small}`2025-07-16` | headings: 0.12.0 {small}`2025-07-16`
- `docs/release-notes/0.11.4.md` | title: 0.11.4 {small}`2025-03-26` | headings: 0.11.4 {small}`2025-03-26`
- `docs/release-notes/0.11.3.md` | title: 0.11.3 {small}`2025-01-10` | headings: 0.11.3 {small}`2025-01-10`
- `docs/release-notes/0.11.1.md` | title: 0.11.1 {small}`2024-11-12` | headings: 0.11.1 {small}`2024-11-12`
- `docs/release-notes/0.11.0.md` | title: 0.11.0 {small}`2024-11-07` | headings: 0.11.0 {small}`2024-11-07`
- `docs/release-notes/0.10.9.md` | title: 0.10.9 {small}`2024-08-28` | headings: 0.10.9 {small}`2024-08-28`
- `docs/release-notes/0.10.8.md` | title: 0.10.8 {small}`2024-06-20` | headings: 0.10.8 {small}`2024-06-20`
- `docs/release-notes/0.10.7.md` | title: 0.10.7 {small}`2024-04-09` | headings: 0.10.7 {small}`2024-04-09`
- `docs/release-notes/0.10.6.md` | title: 0.10.6 {small}`2024-03-11` | headings: 0.10.6 {small}`2024-03-11`
- `docs/release-notes/0.10.5.md` | title: 0.10.5 {small}`2024-01-25` | headings: 0.10.5 {small}`2024-01-25`
- `docs/release-notes/0.10.4.md` | title: 0.10.4 {small}`2024-01-04` | headings: 0.10.4 {small}`2024-01-04`
- `docs/release-notes/0.10.3.md` | title: 0.10.3 {small}`2023-10-31` | headings: 0.10.3 {small}`2023-10-31`
- `docs/release-notes/0.10.2.md` | title: 0.10.2 {small}`2023-10-11` | headings: 0.10.2 {small}`2023-10-11`
- `docs/release-notes/0.10.1.md` | title: 0.10.1 {small}`2023-10-08` | headings: 0.10.1 {small}`2023-10-08`
- `docs/release-notes/0.10.0.md` | title: 0.10.0 {small}`2023-10-06` | headings: 0.10.0 {small}`2023-10-06`
- `docs/release-notes/2342.fix.md` | title: 2342 Fix | headings: (no heading extracted)
- `docs/release-notes/2338.breaking.md` | title: 2338 Breaking | headings: (no heading extracted)
- `docs/release-notes/2309.breaking.md` | title: 2309 Breaking | headings: (no heading extracted)
- `docs/release-notes/2133.breaking.md` | title: 2133 Breaking | headings: (no heading extracted)
- `docs/release-notes/2087.feat.md` | title: 2087 Feat | headings: (no heading extracted)
- `docs/release-notes/2071.feat.md` | title: 2071 Feat | headings: (no heading extracted)
- `docs/release-notes/1927.breaking.md` | title: 1927 Breaking | headings: (no heading extracted)

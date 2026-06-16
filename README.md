# portfolio-manifest

**Single source of truth** for [edwin-brain](https://edwin-brain.web.app) — Edwin's AI portfolio.

This repo is intentionally tiny and **public**: the website reads `projects.json` from here at
runtime, so adding or reordering projects needs **no redeploy**. Only Edwin can push; the public
can read but not change anything.

## Add or change a project

1. Edit `projects.json`.
2. Set `order` to control where it appears in the scroll journey (ascending).
3. `git push`. A GitHub Action validates the file against `schema.json`; an invalid push fails CI.
4. Refresh the live site — it picks up the change automatically.

## Fields

See `schema.json`. Required per project: `slug`, `order`, `title`, `tagline`, `brainRegion`,
`category`, `year`, `problem`, `architecture[]`, `stack[]`, `skills[]`, `role`, `status`, `accent`.
Optional: `icon`, `highlights[]`, `proof[]`, `links { live, repo, case_study }`.

- `category`: short badge label, e.g. `"AI System Builder"`, `"AI Agent"`
- `year`: shown next to the badge, e.g. `"2026"`
- `icon`: animated icon — one of `brain` | `chat` | `network` | `audio` | `voice` | `web` | `data` (default `brain`)
- `highlights[]`: 2-4 short bullets shown on the COMPACT card; the rest (`problem`, `architecture`, `skills`, `role`, `proof`) shows after the visitor clicks **More**
- `status`: `live` | `public` | `case-study` | `archived`
- `links.live`: live URL (shows a **Live ↗** button); `links.repo`: public GitHub repo (shows **GitHub ↗** + live stats)
- `accent`: `#RRGGBB` hex — the section's color in the brain map

## Validate locally

```bash
npx ajv-cli@5 validate -s schema.json -d projects.json --strict=false
```

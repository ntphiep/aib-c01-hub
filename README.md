# AIB-C01 Study Hub

Static study site for the AWS Certified AI Business Strategist exam (AIB-C01, beta), live at https://aib-c01-hub.vercel.app (Vercel project `aib-c01-hub`).

| Path | Content |
|---|---|
| `src/site.json` | Exam config: domains, tasks, topics, home tiles, mock sizes, glossary categories, accent colors |
| `src/index.html` | App shell shared by all study hubs: navigation, search, light/dark theme, chapters, glossary, sources page, quiz, mock exam, flashcards |
| `src/data/topics/` | 5 chapters: 4 exam domains plus AWS offerings at strategy level |
| `src/data/quiz/`, `src/data/cards/` | Quiz questions and flashcards per chapter |
| `src/data/resources.json` | Curated external study sources shown on the page Nguồn học |
| `src/data/glossary-parts/` | Glossary terms per chapter; the build merges them and links the first mention in each section to a popover |
| `src/icons/` | AWS Architecture Icons copied from the SAP-C02 hub, plus `marketplace.svg` from the AWS Architecture Icons package (07/2026) |
| `src/figs/` | Unmodified images from docs.aws.amazon.com (CC BY-SA 4.0) used by `figure` blocks, named `<topic>-<what>.png` |
| `src/fav/` | Favicons of the hosts on the page Nguồn học, downloaded by `node favicons.mjs` |
| `research/` | Official exam guide text: overview, 4 domains, concepts, in-scope and out-of-scope services |
| `diagram.mjs` | ELK auto layout and SVG rendering for diagrams |
| `build.mjs` | Builds `src/` into `dist/`, merges the glossary, creates the search index and the task map |
| `validate.py` | Content rules (schema, English terms, option counts, at least 1 source per section and 3 hosts per topic) |
| `SCHEMA.md` | Content format and writing rules |
| `src/watch.json` | Freshness config: exam guide pages, release-note feeds, date the content was last verified |
| `freshness.py` | Weekly check of exam guide pages, release notes and every source url; stdlib Python |
| `FRESHNESS.md` | How the weekly freshness check and the cloud agent keep the content current |
| `.github/workflows/` | `freshness.yml` runs the weekly check; `freshness-pr.yml` opens a pull request for each `claude/freshness-*` branch |
| `vercel.json` | Vercel build settings for Git deployments; branch `freshness` is never deployed |

Edit content, then run:

```
python3 -I validate.py src/data/topics/*.json src/data/quiz/*.json src/data/cards/*.json src/data/glossary-parts/*.json src/data/resources.json
node build.mjs --check <topicId>   # 0 layout warnings, screenshot in preview/<topicId>.png
node build.mjs                     # full build into dist/
```

Progress sync uses the same Supabase project as the SAP-C02 hub (`hnpixqdvxszxjwovtusr`, RPCs `get_progress` and `save_progress`) with a separate sync code; local progress lives in `localStorage` keys `aibHub` and `aibSync`. Anyone with a sync link can read and overwrite that progress.

Deploy: after `node build.mjs`, run `npx vercel deploy dist --prod --yes --project aib-c01-hub --scope nguyen-hieps-projects` with a token of Vercel account `ntphiep` (Composio connection `legacy`).

The engine files `src/index.html`, `build.mjs`, `diagram.mjs`, `validate.py`, `favicons.mjs`, `freshness.py`, `FRESHNESS.md`, `vercel.json` and `.github/workflows/` are identical in `/home/harry/W/aib-c01-hub`, `/home/harry/W/databricks-dep-hub` and `/home/harry/W/dp-700-hub`. Change them in one hub, then copy them to the other two.

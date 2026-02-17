# Legacy Site (Markdown Version)

This folder contains the original multi-page markdown version of the GitHub Pages site, before it was replaced by the single-page HTML design.

These files were the Jekyll/minima-based site that lived in `docs/`.

## Pages

| File | Description |
|------|-------------|
| [index.md](index.md) | Landing page — overview, stats, abstract, historical context |
| [dataset.md](dataset.md) | Dataset structure, JSONL schemas, question type breakdown |
| [methodology.md](methodology.md) | Construction methodology, prompts, historian-in-the-loop |
| [visualizations.md](visualizations.md) | Interactive sunburst charts + corpus projections |
| [benchmarks.md](benchmarks.md) | Benchmarks, use cases, limitations, future work |
| [cite.md](cite.md) | BibTeX citation, license, ethics |

## How to restore

To revert to the multi-page site, copy these `.md` files back into `docs/`, re-add `theme: minima` and the `header_pages` list to `docs/_config.yml`, and delete `docs/index.html`.

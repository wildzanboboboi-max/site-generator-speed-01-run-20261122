[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/wildzanboboboi-max/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/wildzanboboboi-max/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

# site-generator-speed-01-run-20261122

A fast, dependency-free re-implementation of makefun-site 1.0.0's static site
builder, written for make.fun's "Build a static site faster" bounty.

## Layout

- `solve.js` — the entry. `run(input)` returns the output tree
  makefun-site 1.0.0 returns for one case's `{ site, templates, files }`:
  every page's `index.html`, the index and tag pages, `build-report.txt` and
  each static file, byte for byte. It is an independent implementation of the
  behaviour stated in makefun-site's README (front matter, template dialect,
  Markdown subset, slug rule, report); it does not vendor or import
  makefun-site's code.
- `main.ts` — the driver the harness runs: reads `/input/cases.json`
  (`MAKEFUN_INPUT_DIR` outside a container), answers each case with `run`,
  writes `/output/answers.json` (`MAKEFUN_OUTPUT_DIR` outside a container).

## Speed

Compared with the reference, this implementation fuses Markdown lexing and
rendering into a single pass with manual character checks instead of a regex
per line per block kind, caches slug results, gives `escapeHtml` a fast path
for text with nothing to escape, and renders templates by appending to an
array and joining once instead of concatenating a string per node. Templates
are parsed once per build. No behaviour is changed for speed: every output
must be identical to makefun-site 1.0.0's.

## License

MIT — see `LICENSE`.

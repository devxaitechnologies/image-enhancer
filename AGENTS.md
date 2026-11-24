# AGENTS.md

Engineering guidelines for contributors and coding agents working on Image Enhancer.

## Product principle: best effort

- Best-effort processing is the minimum guarantee. When the input is available and processing can run, return the best result the system can produce.
- A result with minor imperfections is better than returning the unchanged input or nothing.
- Low confidence, incomplete coverage or a quality warning must not block output on their own. Pick the most plausible validated strategy, produce the result, and surface uncertainty as non-blocking metadata or UI copy.
- Only suggest "retry" or "refresh" when repeating the action can actually change the outcome.
- Reserve hard failure for cases where processing truly cannot run or no usable input or output exists.

## Investigation workflow

- Treat unexpected results as a pattern-discovery task first, not threshold tuning. Derive geometry and rendering rules from the samples (anchor position, size, subpixel offset, alpha shape and strength, background-dependent behavior) before changing heuristics.
- Build batch reports and visual artifacts from the sample set: a full list with dimensions and scores, crop sheets, candidate overlays, and before/after crops for every changed strategy.
- Do not generalize from a single image. Cluster samples by size, anchor, background and residual behavior, then make the smallest change the cluster supports.
- Prefer improving candidate localization and estimation over loosening safety gates. Safety gates are a final fallback.
- A score computed only with the candidate's own selected parameters is useful for ranking, not as independent proof of quality. Promotion evidence should come from frozen cross-profile or decoy checks and blind visual review.
- Keep signed polarity checks intact when a rescue assumes a particular template polarity; do not replace them with absolute or max scores without independent validation.
- Treat noisy review signals (texture hard-reject flags, dark-hole flags, selection-stage damage warnings) as hints, not as ground truth for status, ranking, blocking or retry behavior, unless validated on frozen holdout data.
- Keep experimental repair strategies offline until a preregistered holdout shows useful recall and no damage to clean outputs.
- Sample provenance is separate from processing quality. Do not label a sample as edited or passing without evidence, and do not add runtime rejection rules just to exclude unusual inputs.

## Build and local services

| Task | Command |
| --- | --- |
| Production build | `pnpm build` |
| Local dist server | `pnpm dev` (starts at `http://127.0.0.1:4173/`, increments if the port is busy) |
| Tests | `pnpm test` |

- The generated `dist/` directory is the active local build surface; keep deployment assumptions aligned with the repository contents.
- Always trust the port printed by `pnpm dev`.
- Local-only paths and settings belong in `.env`; use `.env.example` as the public template.

## Browser validation notes

- Verify installed userscripts against the freshly built `dist/userscript/image-enhancer.user.js` (compare source content, not just the version string).
- Do not assume Web Worker support in restricted pages. Treat a worker as usable only after its startup handshake succeeds, and always keep a working main-thread fallback.
- Read runtime flags across `unsafeWindow` when running in a userscript sandbox.
- When performance regresses, first check that the page runtime actually installed, that the processing queue is not blocked on an image that is not yet renderable, and that no expensive refinement step runs without being adopted. Only then touch the core algorithm.
- Do not intercept or cancel the page's native download or copy actions. Let the page's own flow run and process the resulting request passively, with an intent window long enough for slow responses (around 30 seconds) that is released after success or failure.

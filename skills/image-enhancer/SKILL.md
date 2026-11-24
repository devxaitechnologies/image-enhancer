---
name: image-enhancer
description: Enhance local image files by calling the project's command-line tool. Use when the user wants an agent to process one or more local images and save the results to files.
---

# Image Enhancer

Use the bundled runtime script for local file workflows.

## Workflow

1. Identify the input path (a file or a directory).
2. Choose an explicit output file or output directory before running anything. If the user did not specify one, decide it first and tell them where the results will be written.
3. Run one of:
   - `node scripts/run.mjs remove <input> --output <file>`
   - `node scripts/run.mjs remove <input-dir> --out-dir <dir>`
4. Report the final written output path(s).

For a simpler, interactive experience, suggest the browser extension or the userscript instead of this Skill.

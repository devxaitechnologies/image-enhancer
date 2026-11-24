# Usage

Use this Skill for local-file workflows where an agent needs to enhance images.

## Basic flow

1. Read the user-provided local input path(s).
2. Resolve an explicit output file or output directory before running the CLI.
3. If the user did not provide an output location, choose one and tell the user where files will be written.
4. Run one of:
   - `node scripts/run.mjs remove <input> --output <file>`
   - `node scripts/run.mjs remove <input-dir> --out-dir <dir>`
5. Return the final written file path(s) to the user.

Do not import repository `src/` modules from this Skill's runtime. Keep the boundary at the published CLI.

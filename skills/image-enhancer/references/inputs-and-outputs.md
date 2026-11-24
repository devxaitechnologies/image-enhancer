# Inputs and Outputs

- Accept local file paths only.
- Require an explicit output file or output directory before running the CLI.
- If the user did not specify an output location, choose one and tell the user first.
- Always pass the `remove` subcommand explicitly, for example:
  - `node scripts/run.mjs remove <input> --output <file>`
  - `node scripts/run.mjs remove <input-dir> --out-dir <dir>`
- Return the final written file path(s).

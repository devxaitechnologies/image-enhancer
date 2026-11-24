# Limitations

- This Skill is a thin wrapper over the `gwr` CLI. Inside this repository it uses the local `bin/gwr.mjs`; in standalone installs it looks for `gwr` on `PATH` and can fall back to `pnpm dlx image-enhancer`. Override the package spec with `GWR_SKILL_CLI_SPEC` for staged rollouts or local validation.
- Inputs must be local files; remote URLs are out of scope.
- The Skill does not implement any image processing itself.

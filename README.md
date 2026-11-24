# Image Enhancer

Image Enhancer cleans up and enhances images directly in your browser or from the command line. Processing happens locally, so your files are never uploaded anywhere.

## Features

- **Local processing** — all work runs on your device.
- **Several ways to use it** — browser extension, userscript, command-line tool and a JavaScript SDK.
- **Batch friendly** — process a single file or a whole folder.
- **Best-effort results** — when an image can be processed, you always get the best result the tool can produce, with any uncertainty reported as metadata rather than a hard failure.

## Getting started

### Requirements

- Node.js 20 or newer
- pnpm

### Install and build

```bash
pnpm install
pnpm build      # production build, written to dist/
```

### Run the local preview

```bash
pnpm dev        # serves dist/ on http://127.0.0.1:4173 (the port increments if busy)
```

### Run the tests

```bash
pnpm test
```

## Usage

### Browser extension

1. Run `pnpm build`.
2. Open `chrome://extensions` and enable **Developer mode**.
3. Choose **Load unpacked** and select the generated extension folder in `dist/`.

### Userscript

1. Install a userscript manager such as Tampermonkey.
2. Build the project and open `dist/userscript/image-enhancer.user.js` through the local server to install it.

### Command line

```bash
node bin/gwr.mjs remove <input> --output <file>
node bin/gwr.mjs remove <input-dir> --out-dir <dir>
```

Options:

| Option | Description |
| --- | --- |
| `--output <file>` | Write the result to a specific file. |
| `--out-dir <dir>` | Write results for a directory of inputs into a folder. |
| `--overwrite` | Replace existing output files. |
| `--json` | Print machine-readable results. |

### JavaScript SDK

```js
import { /* ... */ } from 'image-enhancer';           // Node.js
import { /* ... */ } from 'image-enhancer/browser';    // browsers
import { /* ... */ } from 'image-enhancer/image-data'; // raw ImageData
```

Type declarations ship with the package.

## Project layout

| Path | Purpose |
| --- | --- |
| `src/core/` | Image processing engine |
| `src/sdk/` | Public JavaScript API |
| `src/cli/` | Command-line interface |
| `src/extension/` | Browser extension |
| `src/userscript/` | Userscript runtime |
| `public/` | Local preview pages and static assets |
| `scripts/` | Build, benchmark and diagnostic tooling |
| `tests/` | Automated tests |

## Contributing

Contributions are welcome. Please keep changes focused, include tests for behavior changes, and run `pnpm test` before opening a pull request. See [AGENTS.md](AGENTS.md) for engineering guidelines.

## License

MIT

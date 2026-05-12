# pi-openai-code-interpreter

[![ci](https://github.com/code-yeongyu/pi-openai-code-interpreter/actions/workflows/ci.yml/badge.svg)](https://github.com/code-yeongyu/pi-openai-code-interpreter/actions/workflows/ci.yml) [![license: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

OpenAI native code interpreter extension for the [pi coding agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent).

This package is the standalone extraction of senpi's former builtin `openai-code-interpreter` extension.

## Behavior

The extension does not register a new tool. It intercepts OpenAI Responses API requests before they are sent and ensures a native `code_interpreter` tool is present for `openai-responses` / `azure-openai-responses` payloads only when code interpreter is explicitly enabled.

| Case | Result |
|------|--------|
| `PI_OPENAI_CODE_INTERPRETER` is enabled, API is `openai-responses`/`azure-openai-responses`, and no native `code_interpreter` tool exists | injects `{ type: "code_interpreter", container: { type: "auto" } }` |
| `PI_OPENAI_CODE_INTERPRETER` is enabled and a native `code_interpreter` tool already exists | preserves existing native tool (no duplication) |
| `PI_OPENAI_CODE_INTERPRETER` is enabled and a function variant named `code_interpreter` is present | strips function variant and keeps/uses native variant |
| `PI_OPENAI_CODE_INTERPRETER_CONTAINER` is a non-empty string | injects with `container: "<trimmed value>"` |
| `PI_OPENAI_CODE_INTERPRETER` is disabled or unset | no-op |
| API is non-Responses | no-op |

Truthy values for `PI_OPENAI_CODE_INTERPRETER` are: `1`, `true`, `yes`, `on` (case-insensitive, surrounding whitespace allowed).

It also appends a system-prompt section for Responses sessions indicating native `code_interpreter` availability when enabled.

## Installation

The package targets the [`pi`](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) coding agent. Pi loads extensions from `~/.pi/agent/extensions/`, project `.pi/extensions/`, or via the `--extension` / `-e` CLI flag.

```bash
# From npm (once published)
pi install npm:pi-openai-code-interpreter

# From git
pi install git:github.com/code-yeongyu/pi-openai-code-interpreter

# Manual placement
git clone https://github.com/code-yeongyu/pi-openai-code-interpreter ~/.pi/agent/extensions/pi-openai-code-interpreter
cd ~/.pi/agent/extensions/pi-openai-code-interpreter && npm install

# Dev / one-shot test
pi -e /path/to/pi-anthropic-code-execution/src/index.ts
```

After installation, restart pi or run `/reload` inside an interactive session.

## Development

```bash
npm install
npm test
npm run typecheck
npm run check
pi -e ./src/index.ts
```

The test suite uses vitest. TypeScript is strict, Node-only, and uses ESM imports with `.js` suffixes.

## Origin

Ported from `packages/coding-agent/src/core/extensions/builtin/openai-code-interpreter/index.ts` in `code-yeongyu/senpi-mono`.

## License

[MIT](LICENSE).

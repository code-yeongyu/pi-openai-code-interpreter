# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.1] - 2026-09-24

### Changed

- Migrate peer dependencies from `@mariozechner/pi-*` to `@earendil-works/pi-*` (scope consolidation)
- Add `@earendil-works/pi-ai` and `@earendil-works/pi-coding-agent` 0.87.1 as exact devDependencies
- Update devDependencies: `@biomejs/biome` 2.5.14, `vitest` 5.0.1, `@types/node` 26.6.2, `@typescript/native-preview` 7.0.0-dev.20260707.2
- Set `engines.node` to `>=22.19.0` (Bun 1.4.2 target)
- Establish CI with Bun 1.4.2 on Node 22/24 and Ubuntu/macOS
- Generate `bun.lock` and `package-lock.json` for lockfile parity

## [0.1.0] - 2026-05-07

### Added

- Initial release. Native OpenAI code_interpreter policy extension for the pi coding agent. Injects `code_interpreter` into openai-responses and azure-openai-responses requests when `PI_OPENAI_CODE_INTERPRETER` is enabled.

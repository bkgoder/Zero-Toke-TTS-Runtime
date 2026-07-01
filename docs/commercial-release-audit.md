# Commercial Release Audit

## Decision

Use this project as the first low-friction licensing test.

The project is already a complete end-user application: a VS Code voice studio with local Piper TTS, runtime bootstrap, voice management, SQLite history, MCP/SSE integration, HTTP proxying, Docker deployment and a web UI.

The copyright remains with ForgeFabrik. The recommended model is:

- noncommercial use under the existing ForgeFabrik Noncommercial License
- separate written commercial license for companies, paid services, SaaS, bundling or resale
- no copyright transfer

## Release blockers found

1. `README.md` says MIT, while `LICENSE` applies the ForgeFabrik Noncommercial License.
2. `README.md` installs `zero-token-tts-1.5.2.vsix`, while `package.json` is version `1.5.3`.
3. `package.json` repository, homepage and bug URLs point to `bkgoder/Zero-Token-Explotion`, not the current repository.
4. `manifest/runtime-v1.json` still references release tag `v1.5.2`; this must remain unchanged until matching 1.5.3 runtime assets actually exist.
5. `package.json` has `private: true`, which blocks normal registry publication. Keep it only when distributing VSIX files manually; remove it before a registry release.
6. The package metadata uses `SEE LICENSE IN LICENSE`, which is correct for the custom licensing model, but the public documentation must describe the commercial-license path consistently.

## First distribution channel

Primary channel: Visual Studio Marketplace or Open VSX for the extension package.

The extension itself can be offered for noncommercial use. Commercial users receive a separate written license. Runtime binaries remain distributed through signed GitHub release assets and the existing manifest/bootstrap mechanism.

## Minimum release work

- align README license text with `LICENSE`
- align displayed extension version with `package.json`
- replace stale repository URLs with the actual canonical repository or rename the repository first
- verify every runtime asset and SHA-256 checksum named by the manifest
- run `npm ci`, `npm run build`, and VSIX packaging
- install the VSIX into a clean VS Code profile
- test Linux x64 first, then the other declared targets
- add a support/contact address for commercial license requests
- publish a concise privacy statement: local TTS, no cloud speech generation by default

## Commercial license scope

A standard commercial license should permit one legal entity to:

- use the extension internally
- modify the supplied source for internal use
- bundle the extension with one named commercial product when explicitly granted

It should not permit:

- resale of the source as a standalone competing product
- sublicensing or source redistribution
- trademark use
- removal of required copyright and license notices

## Why this project is suitable for the test

- clear end-user benefit
- simple demonstration
- no mandatory hosted service
- local-first privacy angle
- existing installer and release architecture
- useful to developers, accessibility users and teams using coding agents
- low operational burden compared with the larger infrastructure projects

This document is an internal release checklist, not marketing copy and not legal advice.

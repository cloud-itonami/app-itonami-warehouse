# cljs release bundle built by an oracle (2026-11-17)

ORACLE evidence, not a native build. `tauri/bundle/js/app.js` is the output of a JVM shadow-cljs
release run on a mirror of the `.cljk` sources. This repository ignores `cljs/public/js/`, so the
bundle is committed under `tauri/bundle/`, which the Tauri host build overlays onto the static
frontend. No CI, gate, packaging or runtime path runs the oracle; the host only copies the committed
file.

- Command: `python3 cljs-release-oracle.py <work> app-itonami-warehouse app cljs` (script: `oracle/cljs-release-oracle.py`
  in network-awai/app-itonami-resource-flow; mirrors `.cljk` to `.cljc` and `.mjs` to `.js`, overrides
  every `io.github.kotoba-lang/*` dependency with the local worktree, runs `shadow-cljs -A:oracle release app`).
- Tools: node v26.0.0, npm 11.12.1, openjdk 21.0.1, shadow-cljs 2.28.20,
  kotoba-lang/kotoba@426ddd2a635b6714ad60a8d7852f4f802e3e54b6 (sparse `lib/`).
- Input: this repository at 429b6a7f07097cc36802b71278552496f1e18ed9.
- Output: `app.js` 310303 bytes, sha256 9226dcc8c35ab83860a8e8ffb4d6a2fa98b610ff43954387b19afa7fa90c67a9.
- Check: the Tauri host built from it renders the page in Chromium under a CSP with no `'unsafe-eval'`;
  no console errors.
- Note: the rendered page is the generated appview scaffold (route/status listing); it is not a product UI.
- Not shown: behaviour with live data; that a native (Amu) build produces the same code; `cargo check`.

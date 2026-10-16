# UPSTREAM.md: what `local` carries over Epistates/pmetal

`local` is based on the upstream release **v0.5.0** (tag `v0.5.0`, `0891716`). Release tags are
cut on `local` as `v<base>-local<NN>` (`v0.5.0-local01` is the first). `main` is meant to mirror
`Epistates/pmetal` `main`; see the tier model in `eejd/macports-ports-local`
(`docs/development-model.md`, "Forks, upstreams and port tiers").

Upstream `main` is far past v0.5.0 and bundles a different MLX (a commit pin, not v0.31.1), so
`local` stays on the release until upstream cuts the next one.

| What | Commits | Status upstream |
|---|---|---|
| Offline/sandboxed build: `FETCHCONTENT_SOURCE_DIR_*` forwarding in `pmetal-bridge/build.rs` | `a00581b`, `8f203f9`, `26b3f1c`; merged into `local` via `23c23db` | **Merged upstream** as `23c23db` (Epistates PR #17, after v0.5.0). It is the only post-release upstream commit `local` contains. |
| Metal toolchain resolved without xcrun's per-user discovery (`PMETAL_METAL_TOOLCHAIN_BIN`, cryptex mount, xcrun fallback) in `pmetal-metal/build.rs` | `e8bcfe3` (fork PR #3) | Not proposed upstream. A port onto current upstream `main` conflicts in `build.rs` and needs rework. Candidate `topic/*` once that is done. |
| OpenAI content-parts and compatibility hardening in `pmetal-serve`, plus the conformance and benchmark harness `crates/pmetal-serve/eval/` | `fee6ca1` | Not proposed upstream. Conflicts in `routes.rs` and `types.rs` against current `main`. |
| CI: Python 3.14, Rust MSRV verification leg | `c660379`, `4c15f7e` (fork PR #2) | Fork-specific CI; conflicts in `.github/workflows` against current `main`. |
| Merge commits | `925a121`, `1f60ff4`, `69918c8`, `a3884e3` | Integration of the above. |

Nothing is adopted from another fork: every commit above is our own work or upstream's.

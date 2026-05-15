# Rust builds with crane

Use `github:ipetkov/crane` (not `buildRustPackage`) for all Rust builds:

1. Add `crane` as a flake input with `nixpkgs.follows`
2. Instantiate: `craneLib = crane.lib.${system}.overrideToolchain rustToolchain`
3. Build with `craneLib.buildPackage` — reads `Cargo.lock` automatically, no cargoSha256
4. Use `craneLib.cleanCargoSource` for src to filter only cargo-related files
5. For incremental builds: `craneLib.buildDepsOnly` + cargoArtifacts pattern

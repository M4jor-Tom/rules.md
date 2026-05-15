# Root vs module just concerns

- **Root `justfile`** owns monorepo orchestration: Docker images, compose lifecycle, proto generation. These span modules.
- **Module `justfile`s** (e.g. `<module>/justfile`) own module-internal dev tasks: build, test, lint, fmt. These are self-contained.
- Never duplicate a module task in the root justfile — invoke the module's justfile with `-f` instead.
- Root tasks must never be placed in a module justfile.

# CI must delegate to just

CI workflows must call `just` (or `just -f <path>`) — never inline the raw commands. This keeps the single source of truth in justfiles and avoids drift.

- Backend tasks (fmt, lint, test): `nix develop ./<module> -c just -f <module>/justfile <cmd>`
- Proto drift check: `nix develop ./<module> -c just proto-check` (uses root justfile)
- Docker image: `just docker-image` (uses root justfile)
- If a just target does not exist for a CI step, add it to the appropriate justfile — do not inline.

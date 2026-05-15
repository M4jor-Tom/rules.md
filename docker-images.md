# Building Docker images with Nix

When asked to create or modify Docker images:

1. Use `pkgs.dockerTools.buildImage` in a `pkg/image.nix` file
2. The flake must expose `packages.dockerImage` in its outputs
3. Build and load with:
   ```
   nix build ./server#dockerImage && skopeo copy --policy containers/policy.json docker-archive:result containers-storage:stargem-backend:latest
   ```
4. The project `containers/policy.json` provides the trust policy for `docker-archive` transport — always pass it via `--policy`
5. No Dockerfile, no apt, no debian base images

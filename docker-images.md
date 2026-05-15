# Building Docker images with Nix

When asked to create or modify Docker images:

1. Use `pkgs.dockerTools.buildImage` in a `pkg/image.nix` file
2. The flake must expose `packages.dockerImage` in its outputs
3. Build with `nix build .#dockerImage && docker load < result`
4. No Dockerfile, no apt, no debian base images

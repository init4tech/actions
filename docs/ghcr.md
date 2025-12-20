# ghcr.yml

## Base Usage

```yml
build-and-push:
  uses: init4tech/actions/.github/workflows/ghcr.yml@main
```

## Description

This workflow builds and pushes a Docker image to GitHub Container Registry (GHCR). It builds multi-platform images for both `linux/amd64` and `linux/arm64` architectures and generates artifact attestations for supply chain security.

The workflow automatically:
- Builds the Docker image from the repository's `Dockerfile`
- Tags the image based on the git reference (branch, PR, tag, etc.)
- Pushes to `ghcr.io/<repository-name>`
- Generates artifact attestations for provenance

## Required Permissions

The calling workflow must have the following permissions:

- `contents: read` - To checkout the repository
- `packages: write` - To push to GHCR
- `attestations: write` - To create attestations
- `id-token: write` - For OIDC authentication

## Notes

- The image name is automatically set to `ghcr.io/<repository-name>`
- The workflow uses the repository's default Dockerfile in the root directory
- Multi-platform builds are performed for both AMD64 and ARM64 architectures


# release-docker-ghcr.yml

## Base Usage

```yml
release-docker-ghcr:
  uses: init4tech/actions/.github/workflows/release-docker-ghcr.yml@main
```

## Description

This workflow builds and pushes a Docker image to GitHub Container Registry (GHCR) for multiple platforms. It builds images for both `linux/amd64` and `linux/arm64` architectures, creates a multi-platform manifest, and generates artifact attestations.

The workflow automatically:
- Builds Docker images for multiple platforms (AMD64 and ARM64)
- Tags images based on git references (branch, PR, semver tags, SHA)
- Pushes to `ghcr.io/<repository-name>`
- Creates a multi-platform manifest list
- Generates artifact attestations for provenance

## Required Permissions

The calling workflow must have the following permissions:

- `contents: write` - To create releases and tags
- `packages: write` - To push to GHCR

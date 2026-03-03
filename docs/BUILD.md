# Build template notes

This repo provides reusable GitLab CI templates for building and pushing Docker images using BuildKit.

## Multi-arch builds

By default, the build template targets:

- `linux/amd64`
- `linux/arm64`

Override per project if you need a single platform:

```yaml
variables:
  OCI_PLATFORMS: linux/arm64
```

## Caching

Layer caching is enabled via GitLab registry:

- `OCI_CACHE`: defaults to `$CI_REGISTRY_IMAGE:cache`

## Required variables (defaults)

- `OCI_IMAGE`: `$CI_REGISTRY_IMAGE`
- `OCI_TAG`: `latest`

## Security

The build runs with rootless BuildKit.

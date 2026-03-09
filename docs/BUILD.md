# Build template notes

This repo provides reusable GitLab CI templates for building and pushing Docker images using BuildKit.

## Multi-arch builds

By default, the build template targets `linux/arm64`.

Override per project if you need a different platform or multi-arch:

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

Registry credentials (`OCI_PASS`) are written to `~/.docker/config.json`
inside an ephemeral CI container and are never persisted. To prevent
accidental exposure in job logs, mark `OCI_PASS` as a
[masked variable](https://docs.gitlab.com/ee/ci/variables/#mask-a-cicd-variable)
in your project's CI/CD settings.

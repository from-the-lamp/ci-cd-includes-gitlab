# 🧞 CI/CD Includes | From the Lamp

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GitLab CI](https://img.shields.io/badge/GitLab-CI/CD-orange?logo=gitlab)](https://docs.gitlab.com/ee/ci/)
[![Docker](https://img.shields.io/badge/Docker-Build-blue?logo=docker)](https://www.docker.com/)

A collection of reusable GitLab CI/CD templates and functions optimized for fast and efficient Docker image builds using **Buildkit**.

---

## 🚀 Key Features

- **Multi-platform build**: Native support for `linux/amd64` and `linux/arm64` out of the box.
- **Rootless Buildkit**: Secure builds without root privileges.
- **Smart Caching**: Integration with GitLab Registry for layer caching.
- **Zero Configuration**: Ready-to-use presets for Backend and Frontend projects.

## 📦 Available Templates

| File | Description |
| :--- | :--- |
| `common_backend.yml` | Standard build for backend. Includes `functions/build_and_push_docker.yml`. |
| `common_frontend.yml` | Standard build for frontend. Includes `functions/build_and_push_docker.yml`. |
| `functions/build_and_push_docker.yml` | Core build mechanism using `buildctl`. |

## 🛠 Usage

Add an `include` to your `.gitlab-ci.yml`:

```yaml
include:
  - project: 'from-the-lamp/infra/ci-cd-includes'
    file: 'common_backend.yml'
    ref: 'main'

# This will automatically add the Build stage and Build job
```

> **Note:** By default, builds trigger only on merge request events.
> Push-based pipelines are not included. Override `rules` in your
> project if you need a different trigger strategy.

## ⚙️ Environment Variables

You can override variables in your project to customize the process:

| Variable | Default Value | Description |
| :--- | :--- | :--- |
| `OCI_TAG` | `latest` | Tag for the created image. |
| `OCI_PLATFORMS` | `linux/amd64,linux/arm64` | List of target platforms. |
| `OCI_IMAGE` | `$CI_REGISTRY_IMAGE` | Full path to the image in Registry. |
| `OCI_CACHE` | `$CI_REGISTRY_IMAGE:cache` | Path for the cache image. |

## 🔗 Project Structure

```text
.
├── common_backend.yml    # Backend template
├── common_frontend.yml   # Frontend template
└── functions/
    └── build_and_push_docker.yml # Core build engine
```

## 📜 License

Distributed under the **Apache 2.0** license. See the [LICENSE](./LICENSE) file for details.

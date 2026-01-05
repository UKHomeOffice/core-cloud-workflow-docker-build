# core-cloud-workflow-node-yarn-test

A GitHub Actions workflow for building docker images test on projects.

## Overview

This workflow automates code testing of Node.js projects within the core-cloud ecosystem, ensuring code quality standards are met.

## Features

- Docker image building

## Requirements

- Valid `Dockerfile`

## Usage

Reference this workflow in your GitHub Actions pipeline:

```yaml
jobs:
    test:
        uses: UKHomeOffice/core-cloud-workflow-node-docker-build
        with:
          image_name: "hello-world"
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `working_directory` | Directory to run yarn test in | No | `.` |
| `dockerfile` | Directory/Name of the Dockerfile (default: Dockerfile) | No | `Dockerfile` |
| `image_name` | Name of the image | no | `` |
| `image_tag` | The tag for the image (default: latest) | yes | `latest` |
| `tag_latest` | Should it also use the tag latest (default: true) | no | `true` |

## Outputs

| Output | Description |
|--------|-------------|
| `docker_build_exit_code` | Exit code from docker build (0 = success) |

## Support

For issues or questions:
- Create an issue in this repository
- Contact the Sauron Team on Slack: #core-cloud-team-sauron
- For tag enforcement questions, contact the Checkov workflow maintainers: #core-cloud-team-sauron

---

## Updated Repository Structure
```
core-cloud-workflow-docker-build/
.github
├── workflows
|    └── self-test.yaml
|
├── action.yaml
├── CODEOWNERS
├── README.md
└── tests
    ├── test-test-invalid/
    └── test-test-valid/
```

### 📘 SonarQube Configuration 
– `sonar-project.properties`

```
sonar.exclusions=tests/**

```

This removes all test fixtures and example IaC from SonarQube analysis, ensuring the Quality Gate only evaluates the actual workflow, action code, and scripts.

| Directory           | Purpose                                               | Excluded From SAST? |
| ------------------- | ----------------------------------------------------- | ------------------- |
| `tests/**`          | Local docker build test harness (intentionally invalid code) | ✅ Yes               |
| `action.yaml`       | Composite action logic                                | ❌ No                |

This setup ensures clean SAST results without blocking PRs due to intentionally invalid IaC.

## Contributing

Please read [CONTRIBUTING.md](./CONTRIBUTING.md)

## Security

Please read [SECURITY.md](./SECURITY.md)
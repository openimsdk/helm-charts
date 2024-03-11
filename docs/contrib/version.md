# Advanced Version Management for OpenIM Helm Charts

OpenIM Helm Charts leverage a sophisticated version management system, encompassing a variety of charts like `openim-server`, `openim-chat`, `openim-web`, and `openim-admin`. This system, while complex, ensures streamlined and efficient chart deployment and maintenance.

## The Unique Approach to Version Control

Unlike traditional software version control that often relies on branch concepts, Helm Charts for OpenIM utilize a tag-based system. This approach simplifies the versioning process as follows:

- **Chart.yaml File**: Each chart contains a `Chart.yaml` file in its directory. This file is pivotal for managing the version of each individual chart. It holds the `version` key, which gets updated with every new release.

```yaml
version: 0.1.17
```

- **Automated CICD**: Developers don't need to worry about managing branches, tags, or releases manually. These aspects are handled automatically through Continuous Integration and Continuous Deployment (CICD) systems. When a new chart version is pushed to the repository, the CICD pipeline is triggered.

- **Tagging and Releases**: The CICD system automatically builds new versions and publishes them to the Helm repository. It also tags the release, for instance, `openim-admin-0.1.2`. The tag structure was thoughtfully designed for easy navigation and version tracking.

> Naming Convention for Tags: **v1.0.0-k8s** vs. **k8s-v1.0.0**

1. **v1.0.0-k8s**: This format follows the conventional versioning system (major.minor.patch) and appends a branch-specific identifier, making it easy to recognize and sort by version number.
   
2. **k8s-v1.0.0**: Here, the branch identifier precedes the version number. This is particularly useful for repositories with multiple branches, as it allows for quick differentiation of branch-specific builds.

**Unified Strategy**:

- For a single-branch repository requiring multiple version strategies, such as helm-charts, **k8s-v1.0.0** is more convenient and distinguishable.
- For multi-branch scenarios like `openim-web` and `openim-admin`, requiring local tagging, **v1.0.0-k8s** is more suitable. It facilitates better version control and aids in managing related images and releases.

## Release Process and Installation

Post-tagging, the CICD automation handles the release process. For example, a release like `https://github.com/openimsdk/helm-charts/releases/tag/openim-admin-0.1.2` can be downloaded and extracted locally:

```bash
tar -zxvf openim-admin-0.1.2.tgz
```

details:

```bash
openim-admin# tree 
.
├── Chart.yaml
├── README.md.gotmpl
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml
```

This extraction reveals a structured directory that can be deployed using Helm:

```bash
helm install openim-admin ./openim-admin
```

## Web Interface and Repository Integration

CICD also automates the deployment of the web interface, like `https://openimsdk.github.io/helm-charts/`. Users can add the OpenIM Helm repository using:

```bash
helm repo add openim https://openimsdk.github.io/helm-charts/
```

And then search for available OpenIM charts:

```bash
helm search repo openim
```
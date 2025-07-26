# 🛠️ Helm Chart Lifecycle - Basic Installation & Management Guide

This guide outlines the standard process for installing, modifying, upgrading, and managing Helm charts using Bitnami (or other) repositories in a local or production Kubernetes cluster.

---

## 📦 Add and Manage Repositories

```bash
# Add Bitnami Helm repository
helm repo add bitnami https://charts.bitnami.com/bitnami

# Update chart repository index
helm repo update

# Search available charts in repositories
helm search repo bitnami
helm search repo nginx

# Search charts on Helm Hub
helm search hub nginx
```

---

## 🚀 Install a Helm Chart

```bash
# Install nginx chart from Bitnami repo
helm install mynginx bitnami/nginx
```

---

## 🔍 Inspect and Manage Releases

```bash
# List all installed releases in current namespace
helm ls

# Get detailed status of a specific release
helm status mynginx

# Uninstall a release
helm uninstall mynginx
```

---

## 🧰 Customize a Chart (Edit & Reinstall)

```bash
# Pull the installed chart version locally
helm pull bitnami/nginx --version 21.0.8 --untar

# Export the currently used values (default + overrides)
helm get values mynginx --namespace default --all > used-values.yaml

# Edit `used-values.yaml` as needed
# (e.g., image.tag, service.type, replicas, etc.)
```

---

## 🔍 Preview Changes Before Upgrade

```bash
# Install Helm Diff plugin (only once)
helm plugin install https://github.com/databus23/helm-diff

# Show a diff of what will change
helm diff upgrade mynginx ./nginx -f used-values.yaml
```

---

## 🔄 Apply Upgrades & Manage Versions

```bash
# Upgrade release using local chart and modified values
helm upgrade mynginx ./nginx -f used-values.yaml

# View release history and revision numbers
helm history mynginx

# Rollback to a previous revision if needed
helm rollback mynginx 1
```

---
## 🚀 dry-run & debug before installing
``` bash
helm install nginx --dry-run --debug ./nginx-repo
```
---
## 📘 Best Practices

- Always run `helm diff upgrade` before applying changes
- Use `--dry-run --debug` during testing
- Version control `values.yaml` and pulled charts
- Use namespaces to isolate releases
- Prefer declarative GitOps tools (e.g., ArgoCD, Flux) for production

---

## ✅ Prerequisites

- Kubernetes cluster (local: Minikube, Kind, or remote)
- Helm 3+
- `kubectl` configured


## 📊 Everything You Need to Know About **Helm Charts**

Helm is the package manager for Kubernetes. If Kubernetes is your OS, **Helm is your apt/yum/homebrew**.

Helm helps you define, install, and manage Kubernetes applications using **Helm Charts**.

Helm is maintained by the Cloud Native Computing Foundation.

---

# 🔹 1. What is a Helm Chart?

A **Helm Chart** is a packaged Kubernetes application.

It contains:

* Kubernetes YAML templates
* Default configuration values
* Metadata
* Dependency definitions

Think of it like:

* A Docker image → for containers
* A Helm chart → for Kubernetes apps

---

# 🔹 2. Helm Architecture

Helm works with:

* **Helm CLI**
* **Kubernetes cluster**
* **Chart repository**

Modern Helm (v3) removed Tiller (used in Helm v2).

---

# 🔹 3. Installing Helm

### macOS

```bash
brew install helm
```

### Linux

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

### Windows

```bash
choco install kubernetes-helm
```

Check version:

```bash
helm version
```

---

# 🔹 4. Helm Chart Structure

When you create a chart:

```bash
helm create mychart
```

It generates:

```
mychart/
  Chart.yaml
  values.yaml
  charts/
  templates/
  .helmignore
```

### 📁 Chart.yaml

Metadata about the chart:

```yaml
apiVersion: v2
name: mychart
version: 0.1.0
appVersion: "1.0"
```

### 📁 values.yaml

Default configuration values.

### 📁 templates/

Kubernetes resource templates (Deployment, Service, etc.)

---

# 🔹 5. Core Helm Commands

## 🔹 Create Chart

```bash
helm create mychart
```

## 🔹 Install Chart

```bash
helm install myrelease mychart
```

## 🔹 Install from Repo

```bash
helm install myrelease bitnami/nginx
```

## 🔹 Upgrade Release

```bash
helm upgrade myrelease mychart
```

## 🔹 Rollback Release

```bash
helm rollback myrelease 1
```

## 🔹 Uninstall Release

```bash
helm uninstall myrelease
```

## 🔹 List Releases

```bash
helm list
```

## 🔹 Show Values

```bash
helm show values bitnami/nginx
```

---

# 🔹 6. Working with Values

Override values:

### Using CLI

```bash
helm install myrelease mychart --set image.tag=2.0
```

### Using custom values file

```bash
helm install myrelease mychart -f custom-values.yaml
```

---

# 🔹 7. Helm Templating (Important 🔥)

Helm uses Go templates.

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}
```

Common template objects:

* `.Values`
* `.Release`
* `.Chart`
* `.Files`
* `.Capabilities`

Example:

```yaml
image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
```

---

# 🔹 8. Chart Dependencies

Define in `Chart.yaml`:

```yaml
dependencies:
  - name: redis
    version: 17.0.0
    repository: https://charts.bitnami.com/bitnami
```

Update dependencies:

```bash
helm dependency update
```

---

# 🔹 9. Helm Repositories

Add repo:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Update repo:

```bash
helm repo update
```

Search:

```bash
helm search repo nginx
```

---

# 🔹 10. Packaging & Sharing Charts

Package chart:

```bash
helm package mychart
```

Push to registry (OCI):

```bash
helm push mychart-0.1.0.tgz oci://registry.example.com/charts
```

---

# 🔹 11. Helm Hooks

Run jobs at specific lifecycle events:

```yaml
annotations:
  "helm.sh/hook": pre-install
```

Hook types:

* pre-install
* post-install
* pre-upgrade
* post-upgrade
* pre-delete
* post-delete

---

# 🔹 12. Helm Testing

Define test pod:

```yaml
annotations:
  "helm.sh/hook": test
```

Run test:

```bash
helm test myrelease
```

---

# 🔹 13. Linting & Debugging

Lint:

```bash
helm lint mychart
```

Dry run:

```bash
helm install myrelease mychart --dry-run --debug
```

Template locally:

```bash
helm template myrelease mychart
```

---

# 🔹 14. Best Practices

✅ Use semantic versioning
✅ Keep values configurable
✅ Avoid hardcoding
✅ Use `_helpers.tpl` for reusable templates
✅ Separate environment values (dev/staging/prod)
✅ Use resource limits

---

# 🔹 15. Helm vs Kustomize

Helm:

* Template-based
* Application packaging
* Versioned releases

Kustomize:

* Overlay-based
* No templating
* Built into kubectl

---

# 🔹 16. Advanced Concepts

* Subcharts
* Global values
* Library charts
* OCI registries
* Helm plugins
* Chart signing (`helm verify`)
* CRDs inside charts

---

# 🔹 17. Common Real-World Workflow

```bash
helm create myapp
helm lint myapp
helm install myapp ./myapp
helm upgrade myapp ./myapp -f prod-values.yaml
helm rollback myapp 1
```

---

# 🔹 18. Popular Public Helm Repositories

* Bitnami
* Artifact Hub

Artifact Hub is the official chart discovery platform backed by the Cloud Native Computing Foundation.

---

# 🚀 Summary

Helm Charts allow you to:

* Package Kubernetes apps
* Version them
* Configure them dynamically
* Upgrade & rollback safely
* Share them easily

---


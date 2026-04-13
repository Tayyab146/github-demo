# Kubernetes Deploy Layout

This directory contains a Kustomize-based deployment structure for:
- `base`: shared manifests for all environments
- `overlays/staging`: staging-specific config and secrets wiring
- `overlays/production`: production-specific config and domain override

## Quick start

Render staging manifests:

```bash
kustomize build deploy/overlays/staging
```

Apply staging manifests:

```bash
kubectl apply -k deploy/overlays/staging
```

Render production manifests:

```bash
kustomize build deploy/overlays/production
```

Apply production manifests:

```bash
kubectl apply -k deploy/overlays/production
```

## What to customize first

1. Container images in `deploy/base/*/deployment.yaml`
2. Ingress hosts in `deploy/base/ingress.yaml` and `deploy/overlays/production/ingress.yaml`
3. AWS region and identity in overlay `secretstore.yaml`
4. Secret keys/paths in overlay `externalsecret.yaml`
5. Remove `deploy/overlays/staging/app-secret.yaml` if using External Secrets only

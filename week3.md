# Week 3 — Kubernetes on VPS (Detailed Task Cards)

## W3D1 — k3s, certs, DNS

### 68) Install k3s
```bash
curl -sfL https://get.k3s.io | sh -s - --disable traefik
sudo kubectl get nodes
```
```bash
kubectl create namespace infra
kubectl create namespace prod
kubectl create namespace monitoring
```
```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx -n infra
```
```bash
helm repo add jetstack https://charts.jetstack.io
helm install cert-manager jetstack/cert-manager -n infra --set installCRDs=true
kubectl apply -f cluster-issuer.yaml
```
- Ingress with TLS loads via HTTPS in browser.

## W3D2 — Postgres & Redis via Helm, secrets, connectivity

### 73) Helm Postgres
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install pg bitnami/postgresql -n infra -f values-postgres.yaml
```
```bash
kubectl -n infra port-forward svc/pg-postgresql 5433:5432
psql -h 127.0.0.1 -p 5433 -U postgres
```
- Redis `SET`/`GET` works.

## W3D3 — API manifests, media strategy, migration job

### 77) API Deployment & Service
- Random pod in other ns cannot reach DB; API still works.

## W3D4 — Web manifests, env wiring, Stripe webhook

### 82) Web Deployment & Service
- CLI event returns 2xx; API logs event processed.

## W3D5 — CI/CD, HPA, rollback drill

### 85) Build & push GHCR
- App returns to previous version; downtime < 1 min.

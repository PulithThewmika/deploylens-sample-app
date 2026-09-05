# DeployLens Sample App

Sample microservices app (frontend → orders → payments) used to demo
[DeployLens](https://github.com/PulithThewmika/deploylens) deployment
observability: GitHub Actions CI, ArgoCD CD, and chaos-injectable health
metrics.

Each service exposes `ERROR_RATE` and `LATENCY_MS` env vars (0 by default)
to deterministically simulate bad deploys for demos.

## Layout

- `frontend/`, `orders/`, `payments/` — FastAPI services with their own Dockerfiles
- `deploy/` — K8s manifests (Deployment/Service/ServiceMonitor per service) and the load generator, tracked by ArgoCD

## CI/CD

Pushing to `main`/`dev` builds and pushes images to `ghcr.io/puliththewmika/deploylens-<service>`,
then commits the new image tag back into `deploy/<service>/deployment.yaml`
for ArgoCD to sync.

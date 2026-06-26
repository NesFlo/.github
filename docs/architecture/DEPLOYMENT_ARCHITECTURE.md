# Deployment Architecture (Overview)

This short note connects the deployment strategy to the platform architecture described in `ARCHITECTURE.md`. It highlights where deployment concerns map to services and what to prioritize during each evolution phase.

---

## Mapping deployment stages to architecture

- Vercel + Render (MVP): Keep the API Gateway, Authentication, and stateless API services on a PaaS. Use managed Postgres and object storage for persistence. This minimizes ops while enabling rapid iteration.
- Docker on VPS (Growth): Run `Message Processing Core`, `Workflow Engine`, and `Integration Services` as Docker services behind an Nginx reverse proxy. Add Redis and a queueing backend for resilience.
- AWS (Enterprise): Move to managed container platforms and add managed RDS, ElastiCache, S3, ELB, and IAM. Harden networking with VPCs and private subnets for databases and worker clusters.
- Kubernetes (Large scale): Deploy all services as pods with horizontal autoscaling and robust service discovery. Use Helm charts and GitOps for continuous deployment.

---

## Architectural priorities by phase

- MVP: Minimal coupling, fast feedback loops, clear API contracts (OpenAPI). Prioritize developer velocity.
- Growth: Portability, cost control, predictable performance. Prioritize reproducible builds (Docker images) and configuration-as-code.
- Enterprise: Security, compliance, HA. Prioritize multi-AZ databases, secrets management, and fine-grained IAM.
- Large scale: Operational maturity. Prioritize observability, SLOs, advanced deployment strategies, and SRE practices.

---

## Practical guidance

- Build containers for every service early and include health checks, graceful shutdown, and small images.
- Separate configuration from code using environment variables or a configuration service.
- Provide a `docker-compose.yml` for local development and small VPS deployments; provide Helm charts or k8s manifests for cloud.

---

If you want, I can scaffold the first `auth-service` repo (FastAPI) with `Dockerfile`, `pyproject.toml`, a simple health endpoint, and a GitHub Actions workflow targeting a VPS deploy preview.

# Projects

This page highlights selected infrastructure and platform work from my homelab and personal experimentation.

These projects focus on practical infrastructure patterns, reproducible deployments, and operational design rather than one-off experiments.

---

## Homelab Infrastructure Platform

A continuously evolving environment used to experiment with infrastructure architecture, containerized services, and operational workflows.

The homelab acts as a sandbox for testing deployment patterns and documenting reproducible infrastructure.

**Key components**

- Proxmox virtualization
- Docker and Docker Compose
- Traefik reverse proxy
- Technitium DNS
- Git-based documentation workflows
- internal service networking

**Focus areas**

- reverse proxy architecture
- internal DNS design
- service routing and segmentation
- operational documentation and runbooks

[View Homelab Architecture →](/homelab/)

---

## Documentation-Driven Infrastructure

This site itself is treated as a project.

Infrastructure experiments, deployment workflows, and architectural decisions are documented as reproducible runbooks.

The goal is to treat infrastructure documentation as part of the system rather than an afterthought.

**Key elements**

- MkDocs + Material theme
- GitHub Pages hosting
- GitHub Actions deployment pipeline
- local preview environment using Docker
- staged workflow using branches and pull requests

[View Runbooks →](/runbooks/)

---

## Reverse Proxy Platform (Traefik)

A centralized reverse proxy layer used to route traffic to internal services.

The platform handles routing, TLS termination, and shared middleware while allowing backend services to remain isolated from direct exposure.

**Capabilities**

- hostname-based routing
- TLS termination
- internal service discovery
- centralized access patterns

[View Traefik Runbook →](/runbooks/traefik-deployment/)
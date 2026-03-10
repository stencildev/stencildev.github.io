# Projects

This page highlights selected infrastructure and documentation projects that demonstrate how I approach system design, troubleshooting, and operational workflows.

---

## Infrastructure Documentation Site

This site itself is an infrastructure project.

It was designed to create a repeatable workflow for developing, previewing, and publishing documentation.

**Key elements**

- MkDocs with the Material theme
- Docker-based local development environment
- Traefik reverse proxy for local access
- Git branching workflow (`staging → main`)
- GitHub Actions for automated builds
- GitHub Pages for public hosting

This workflow allows content to be tested locally before being promoted to production.

See the **[Site Deployment Workflow](/runbooks/site-deployment)** page for details.

---

## Homelab Infrastructure Platform

My homelab acts as a personal platform for experimenting with infrastructure design and service deployment patterns.

The environment includes:

- Proxmox virtualization
- Docker-based services
- Traefik reverse proxy
- Technitium DNS
- media and platform services

The homelab allows me to experiment with:

- service routing
- DNS-based service discovery
- network segmentation ideas
- infrastructure documentation practices

More details can be found in the **[Homelab](/homelab/)** section of this site.

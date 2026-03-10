# Projects

This section highlights selected infrastructure and homelab projects that demonstrate how I approach system design, troubleshooting, and operational workflows.

## Personal Infrastructure Documentation Site

This site itself is built as a small infrastructure project.

Key aspects include:

- MkDocs with the Material theme
- Git-based workflow using `staging` and `main`
- Local preview environment running in Docker
- Traefik reverse proxy for internal routing
- GitHub Actions for automated builds
- GitHub Pages for public hosting

Workflow:

`staging → local preview → pull request → main → GitHub Actions build → GitHub Pages deploy`

Detailed architecture and documentation can be found in the **[Site Deployment](/notes/site-deployment)** section of the site.

## Homelab Platform

My homelab environment serves as a platform for experimenting with infrastructure design, service deployment, and operational workflows.

It is used to test networking concepts, containerized services, and documentation-driven infrastructure.

Detailed architecture and documentation can be found in the **[Homelab](/homelab/)** section of this site.
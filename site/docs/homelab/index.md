# Homelab

My homelab is where I experiment with infrastructure design, containerized services, networking, and automation.

It functions as a personal platform for testing deployment patterns and operational workflows.

## Core Infrastructure

- **Virtualization:** Proxmox
- **Container Runtime:** Docker / Docker Compose
- **Reverse Proxy:** Traefik
- **DNS:** Technitium
- **CI/CD:** GitHub Actions
- **Hosting:** GitHub Pages for public content

## Architecture Overview

```mermaid
flowchart TD
    A[Proxmox Host]

    A --> B[Docker Host]
    B --> C[Traefik]
    B --> D[Technitium DNS]
    B --> E[Portainer]
    B --> F[Glance Dashboard]
    B --> G[Plex]
    B --> H[Jellyfin]
    B --> I[PeerTube]
    B --> J[Arr Stack]
    B --> K[Authentik]

    L[GitHub Repository] --> M[GitHub Actions]
    M --> N[GitHub Pages]
    N --> O[dstencil.com]
```
[View full architecture diagram →](/homelab/architecture/)

## Development Workflow

Infrastructure and documentation follow a Git-based workflow designed to safely test changes before publishing updates.

```mermaid
flowchart LR

subgraph Local Development
A[staging branch] --> B[Local Docker preview]
end

subgraph Review
B --> C[Pull Request]
C --> D[Merge to main]
end

subgraph CI/CD
D --> E[GitHub Actions]
E --> F[Build MkDocs]
F --> G[Deploy GitHub Pages]
end

G --> H[dstencil.com]
```
[View full Development Workflow →](/homelab/workflow/)

## Goals

The homelab allows me to:

- test infrastructure designs
- experiment with service deployment patterns
- document reproducible setups
- build practical DevOps and systems administration experience

## Focus Areas

My current focus includes:

- Linux systems administration
- Docker-based application deployment
- reverse proxy and TLS design
- DNS and internal service resolution
- documentation-driven infrastructure
- safe change workflows using Git branches and pull requests
# Traefik Deployment

This runbook documents the deployment pattern used for Traefik in my homelab.

The goal of this document is to provide a reproducible reference for deploying a reverse proxy layer using Docker and Traefik while avoiding environment-specific or sensitive information.

---

## Purpose

Traefik acts as the reverse proxy layer for internal services.

Responsibilities include:

- routing requests to backend services
- centralizing entry points
- handling TLS termination
- applying shared middleware
- avoiding direct host exposure of service ports

---

## Design Goals

The deployment follows several design priorities:

- keep configuration reproducible
- separate static and dynamic configuration
- reduce exposed host ports
- centralize TLS behavior
- make configuration changes easy to validate

---

## High Level Architecture

General request flow:

```mermaid
flowchart LR
    A[Client]
    B[Traefik Entrypoint]
    C[Router Rule]
    D[Middleware]
    E[Backend Container]

    A --> B --> C --> D --> E
```

Traefik sits in front of internal services and routes requests based on hostname rules.

---

## Suggested Folder Layout

```text
traefik/
  compose.yaml
  .env
  config/
    traefik.yml
    dynamic/
      middlewares.yml
      tls.yml
      services/
  acme.json
  logs/
```

This layout separates:

- static configuration
- dynamic configuration
- runtime state
- logs

---

## Example Docker Compose Pattern

```yaml
---
services:
  traefik:
    image: docker.io/library/traefik:v3.6.2
    container_name: traefik
    networks:
      traefik:
        ipv4_address: 172.30.0.2
      default:
        ipv4_address: 192.168.1.2  # Static IP address for Traefik on your local network
    security_opt:
      - no-new-privileges:true
    ports:
      - 80:80
      - 443:443
      - 127.0.0.1:8080:8080
    env_file:
      - .env
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./config/traefik.yaml:/traefik.yaml:ro
      - ./acme.json:/acme.json
      - ./config/dynamic:/dynamic:ro
      - ./logs/access.log:/var/log/traefik/access.log
      - ./logs/traefik.log:/var/log/traefik/traefik.log
    restart: always

networks:
  traefik:
    name: traefik
    driver: bridge
    ipam:
      config:
        - subnet: 172.30.0.0/24
          gateway: 172.30.0.1
          ip_range: 172.30.0.128/25 # <-- dynamic IPs ONLY from .128-.254
    
  default:
    external: true
    name: default-net
```

This example reflects the general deployment pattern used in the homelab.
Environment-specific values such as credentials and domain information should be kept in the `.env` file.  
!!! note
    The compose example above uses a macvlan network (`default-net`) so the
    container receives an IP on the local network.

    This network must be created on the Docker host before deploying the stack.

    If the Docker host can bind ports 80 and 443 directly, published ports
    can be used instead of macvlan. 

---

## Static Configuration

Static configuration defines Traefik's core behavior.

Typical components include:

- entrypoints
- providers
- certificate resolvers
- logging
- access logs
- dashboard settings

Static configuration usually lives in:

`config/traefik.yml`

---

## Dynamic Configuration

Dynamic configuration defines:

- routers
- services
- middleware
- TLS settings

Dynamic configuration is usually split into multiple files under:

`config/dynamic/`

This keeps routing configuration modular and easier to maintain.

---

## Network Model

Backend containers join the shared Traefik network.

Typical pattern:

1. backend service joins the reverse proxy network
2. backend service does not publish host ports
3. Traefik reaches the service through the Docker network
4. DNS resolves the service hostname to the reverse proxy

---

## DNS Integration

Internal DNS should resolve service names to the Traefik entry point.

Example flow:

`internal DNS → Traefik hostname → router rule → backend container`

This makes services accessible by hostname instead of IP address.

---

## TLS Considerations

TLS can be implemented in several ways depending on the environment.

Common patterns include:

- public certificates for external services
- DNS challenge for wildcard certificates
- internal TLS for private services

Certificate management is typically centralized at the reverse proxy layer.

---

## Change Workflow

Typical safe workflow when updating Traefik configuration:

1. update configuration files
2. validate YAML formatting
3. review router rules
4. redeploy the container
5. test host-based routing
6. review logs

---

## Validation Checklist

After deployment verify:

- [x] container is running
- [x] correct Docker networks are attached
- [x] configuration files are mounted correctly
- [x] routers are loading
- [x] backend services are reachable
- [x] DNS resolution works
- [x] TLS behaves as expected
- [x] logs contain no configuration errors

---

## Troubleshooting

### Container Issues

- container failed to start
- incorrect volume mounts
- file permission problems

### Configuration Issues

- YAML syntax errors
- incorrect router names
- wrong entrypoint references
- undefined middleware

### Networking Issues

- backend service not on Traefik network
- incorrect backend port
- DNS not resolving correctly
- container name not reachable

### TLS Issues

- certificate resolver misconfiguration
- permission errors on certificate storage
- DNS challenge failures
- hostname mismatch

---

## Operational Notes

Useful operational practices:

- separate static and dynamic configuration
- keep dynamic configuration modular
- avoid exposing backend ports unnecessarily
- document hostname patterns
- review logs after configuration changes

---

## Summary

This deployment model allows Traefik to act as a centralized routing layer for internal services.

It works well for homelab environments built around:

- Docker-based services
- internal DNS
- hostname-based routing
- centralized TLS handling
- documentation-driven infrastructure
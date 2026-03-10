# Reverse Proxy

Services in the homelab are accessed through a reverse proxy layer.

This approach allows multiple internal services to be exposed in a consistent and controlled way while keeping individual containers isolated.

## Reverse Proxy Platform

The environment uses **Traefik** as the reverse proxy.

Traefik provides:

- dynamic service routing
- automatic configuration through Docker labels
- TLS termination
- centralized access points for services

## Why a Reverse Proxy

Using a reverse proxy simplifies infrastructure management.

Instead of exposing many ports across multiple systems, services are accessed through a small number of controlled entry points.

This provides several advantages:

- consistent service access
- simplified network configuration
- centralized TLS handling
- easier service discovery

## Integration with DNS

Internal DNS records point service names to the reverse proxy entry point.

Traefik then routes requests to the appropriate backend container.

This allows services to be accessed using consistent hostnames instead of IP addresses.

## Operational Benefits

This architecture allows experimentation with:

- containerized service routing
- TLS configuration
- service naming conventions
- access control layers
# DNS

My homelab relies on an internal DNS server to provide consistent service discovery and name resolution across the environment.

## DNS Server

The environment uses **Technitium DNS Server** to provide internal DNS services.

Technitium handles:

- internal name resolution
- recursive DNS queries
- local zone management
- DNS policy configuration

## Why Internal DNS Matters

Running internal DNS makes infrastructure easier to manage and reason about.

Instead of accessing services using IP addresses, systems can refer to services by name. This improves:

- usability
- service portability
- infrastructure documentation
- troubleshooting clarity

## Example Use Cases

Internal DNS enables workflows such as:

- accessing services through a reverse proxy
- resolving internal service hostnames
- simplifying infrastructure configuration
- maintaining consistent naming across environments

## Operational Benefits

Using a dedicated DNS server allows experimentation with:

- DNS policies
- service naming conventions
- network segmentation strategies
- internal service discovery patterns
# Networking

My homelab networking is designed around separation, controlled access, and predictable internal service resolution.

## Design Goals

- separate device types by trust level
- reduce unnecessary east-west access
- make internal services easy to reach by name
- keep management paths intentional
- support experimentation without exposing everything broadly

## Current Approach

My environment uses VLAN and firewall-based separation to isolate different classes of devices and services.

Examples include:

- **Primary / trusted devices**
- **Guest devices**
- **IoT devices**
- **Infrastructure and service hosts**

This allows internal services to stay organized while reducing unnecessary communication between networks.

## Internal Access

Internal services are routed through infrastructure components such as:

- **Traefik** for reverse proxying
- **Technitium DNS** for internal name resolution

This makes services easier to access consistently by name instead of relying on raw IP addresses.

## Why It Matters

This networking model helps me test infrastructure patterns that are closer to real operational environments, including:

- service segmentation
- internal DNS design
- controlled routing
- safer service exposure
- infrastructure troubleshooting
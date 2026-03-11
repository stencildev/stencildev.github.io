---
hide:
  - navigation
  - toc
---

# Development Workflow
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
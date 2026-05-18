# primos-deploy Config: 1+2 Cluster

**Topology**: 1 server + 2 workers
**Bootstrap**: ArgoCD + cert-manager

## ⚠️ Demo Project

This configuration uses **demonstration encryption keys**.
Secrets are encrypted with publicly known keys for exploration purposes.

## Quick Start

```bash
# Automatic deployment (via primos-deploy-connect)
# server-init pipeline handles everything automatically
```

## Nodes

| Role | IP |
|------|----|
| Server | 10.200.0.10 |
| Worker 1 | 10.200.0.20 |
| Worker 2 | 10.200.0.21 |

## Create Real Project

```bash
primos-deploy project create-from-demo
```
Generates real keys, requires new passwords, creates a clean project.

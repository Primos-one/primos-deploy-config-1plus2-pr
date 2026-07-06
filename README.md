# primos-deploy Config: 1+2 Cluster

**Topology**: 1 server + 2 workers
**Bootstrap**: ArgoCD + cert-manager

## Branches

| Branch | Contour |
|--------|---------|
| `main` | Legacy demo (`stacks/Pulumi.demo-cluster.yaml`, mock target IPs) |
| `v3-primos` | Containerized 1s+2w dev topology for the v3-primos L2 acceptance scenario (primos-deploy-v3 #424/#395 E5) |

## v3-primos branch (this branch)

Dev-mode **containerized** topology (decisions #52/#53/#59 of the v3-primos design):

- `stacks/Pulumi.dev.yaml` — the governed stack config the deployment-node
  agent pulls (`stacks/Pulumi.<stage>.yaml`, stage `dev`, config-pull #384):
  - 1 server + 2 worker `primos-deploy-target` containers on the `primos`
    docker resource; node IPs are **Docker-bridge container IPs** (the agent
    derives the bridge subnet from them), NOT host IPs;
  - `profile: dev` → k3s `--snapshotter=native` (overlay-on-overlay);
  - deploy SSH key injection seam (`ssh.privateKeyPath` env seam
    `PRIMOS_DEPLOY_SSH_KEY_PATH`, per-cluster deploy keypair #427);
  - `publicKubeSni: kube-01.cp.benadis.org` (k3s `--tls-san`, #428/#430);
  - ArgoCD ApplicationSet → **internal embedded Gitea** copy of this repo
    (seeded by Portal, #418).
- `apps/argocd-public-route/` + `manifests/argocd-public-route/` — ArgoCD-managed
  Traefik IngressRoute publishing the ArgoCD UI on `argocd-01.cp.benadis.org`
  (via the infra nginx L7 vhost, #428).
- `pools/dev.yaml` — dev-stage pool definition for the seeded-repo intake
  (segment-3 admission binds the `primos` resource into it).

Seeding is **pin-required** (commit SHA or tag; floating branches are refused,
Q-R2-2a): use the `v3-primos-r*` tags.

## Nodes

| Role | IP (Docker bridge) |
|------|--------------------|
| Server | 10.200.0.10 |
| Worker 1 | 10.200.0.20 |
| Worker 2 | 10.200.0.21 |

## ⚠️ Demo/test keys

This configuration uses **demonstration encryption keys** (see `DEMO_KEYS.md`).
Secrets are encrypted with publicly known keys for exploration purposes.

## Create Real Project

```bash
primos-deploy project create-from-demo
```
Generates real keys, requires new passwords, creates a clean project.

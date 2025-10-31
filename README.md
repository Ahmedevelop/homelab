# 🚀 Kubernetes & GitOps Showcase

[![Kubernetes](https://img.shields.io/badge/Kubernetes-326ce5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![ArgoCD](https://img.shields.io/badge/ArgoCD-FB542B?style=for-the-badge&logo=argo&logoColor=white)](https://argo-cd.readthedocs.io/)
[![TalosOS](https://img.shields.io/badge/TalosOS-3A3A3A?style=for-the-badge&logo=linux&logoColor=white)](https://www.talos.dev/)
[![Traefik](https://img.shields.io/badge/Traefik-24A1C1?style=for-the-badge&logo=traefikproxy&logoColor=white)](https://traefik.io/)
[![Cilium](https://img.shields.io/badge/Cilium-292929?style=for-the-badge&logo=cilium&logoColor=F9C21A)](https://cilium.io/)
[![MetalLB](https://img.shields.io/badge/MetalLB-0064FF?style=for-the-badge&logoColor=white)](https://metallb.universe.tf/)
[![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![Bitwarden](https://img.shields.io/badge/Bitwarden-175DDC?style=for-the-badge&logo=bitwarden&logoColor=white)](https://bitwarden.com/)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)](https://www.cloudflare.com/)
[![Let's Encrypt](https://img.shields.io/badge/Let's%20Encrypt-003A70?style=for-the-badge&logo=letsencrypt&logoColor=white)](https://letsencrypt.org/)

---

### 🎯 Purpose

The purpose of this repository is to **showcase my knowledge of Kubernetes and GitOps methodology** through a fully functional, self-hosted infrastructure setup.

---

## 🧩 Tech Stack Overview

| Component | Description |
|------------|-------------|
| **Kubernetes Distribution** | [TalosOS](https://www.talos.dev/) running on top of a Proxmox cluster (5 nodes: 3 control plane + 2 worker nodes) |
| **GitOps / Continuous Delivery** | [ArgoCD](https://argo-cd.readthedocs.io/) for automated deployments and declarative app management |
| **Networking & Load Balancing** | [Cilium](https://cilium.io/) as CNI, [MetalLB](https://metallb.universe.tf/) for L2 load balancing, and [Traefik](https://traefik.io/) as the ingress controller |
| **Certificates & DNS** | [Let’s Encrypt](https://letsencrypt.org/) for TLS certificates, integrated with [Cloudflare](https://www.cloudflare.com/) for DNS and web exposure |
| **Persistent Storage** | NFS server on a local VM with [`nfs-subdir-external-provisioner`](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner) providing dynamic PersistentVolume provisioning |
| **Monitoring & Observability** | [Grafana](https://grafana.com/) + [Prometheus](https://prometheus.io/) for metrics, dashboards, and alerting |
| **Secrets Management** | [External Secrets Operator (ESO)](https://external-secrets.io/) integrated with [Bitwarden Secret Manager](https://bitwarden.com/help/secrets-manager/) for centralized secret syncing |

---

##  Architecture Highlights

- **High Availability** Talos cluster (3 control planes + 2 workers)
- Fully declarative setup managed via **GitOps principles**
- **ArgoCD** continuously reconciles Git and cluster states
- **TalosOS** ensures immutable and secure Kubernetes nodes
- **Traefik + MetalLB** expose internal and external services
- **NFS-based StorageClass** for dynamic PVC provisioning
- **Grafana dashboards** provide system observability
- **ESO + Bitwarden** handle secret management and rotation

---

## 🗺️ Conceptual Diagram

```text
                            ┌───────────────────────────┐
                            │       Proxmox Cluster     │
                            └───────────────────────────┘
                                        │
          ┌────────────────────────────────────────────────────────┐
          │                         Talos HA Cluster               │
          │                                                        │
          │     ┌────────────┐   ┌────────────┐   ┌────────────┐   │
          │     │ Control #1 │   │ Control #2 │   │ Control #3 │   │
          │     │  (API etc) │   │  (API etc) │   │  (API etc) │   │
          │     └────────────┘   └────────────┘   └────────────┘   │
          │             │               │               │          │
          │             └──────────Cluster Network──────┘          │
          │                           │                            │
          │          ┌────────────────┴────────────────┐           │
          │          │                                 │           │
          │   ┌────────────┐                    ┌────────────┐     │
          │   │ Worker #1  │                    │ Worker #2  │     │
          │   │ (Apps/Pods)│                    │ (Apps/Pods)│     │
          │   └────────────┘                    └────────────┘     │
          │                                                        │
          └────────────────────────────────────────────────────────┘
                             │                 │
                             ▼                 ▼
                   +----------------+   +----------------+
                   |    ArgoCD      |   |   Traefik LB   |
                   +----------------+   +----------------+
                             │
                             ▼
                   +--------------------+
                   |  Deployed Services  |
                   +--------------------+
                             │
                             ▼
                   +--------------------+
                   |   NFS Persistent   |
                   |     Volumes        |
                   +--------------------+
```
## 🪜 Roadmap

###  Current setup
- Full HA Kubernetes cluster with **TalosOS**, **ArgoCD**, **MetalLB**, **Cilium**, **Traefik**, and **ESO + Bitwarden**
- **Cloudflare + Let’s Encrypt** integration for SSL and DNS
- **Grafana + Prometheus** for monitoring
- **Dynamic NFS storage provisioning**

###  Next on the roadmap
-  Implement **Single Sign-On (SSO)**
-  Integrate a **Local Identity Provider (IDP)** for internal authentication
-  Add **Keycloak** or **Dex** for unified user and service identity management
-  Automate **Infrastructure as Code** for full cluster bootstrapping

---

##  Key Takeaways

This setup demonstrates:

-  End-to-end **GitOps workflow**
-  Highly available **Kubernetes management**
-  Self-hosted **storage, networking, and monitoring**
-  Secure **secret and identity management**
-  Continuous delivery with **ArgoCD**

---

###  Author

**Ahmad Rzayev**  
_Systems Engineer | Kubernetes & Cloud Infrastructure Enthusiast_  
🌐 [devirthas.com](https://devirthas.com)
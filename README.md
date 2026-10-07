# DevOps Coursework

Hands-on notes and code for the DevOps module, one folder per topic. Each folder has its own
README with the commands that were run, the output, and screenshots from the run.

| Folder | Topic |
|---|---|
| `Linux Fundamentals/` | Hard vs soft links, `useradd` vs `adduser`, `journalctl`, command cheat sheet |
| `Shell Scripting/` | `sysinfo.sh`: variables, user input, `mkdir`/`touch`, output redirection |
| `Networking Fundamentals/` | `ping`, `ip`, `ss`, `curl`, `wget`, `nslookup`, `traceroute`, `hostname` |
| `Git and Github/` | `git commit -a` vs `-m`, `git cherry-pick` |
| `Docker Fundamentals/` | Six Hello World containers: Node.js, Python, Java, Apache, React, Nginx |
| `DockerFiles and Images/` | Multi-stage Go build, 365 MB toolchain to a 7 MB image |
| `Docker Networks/` | Multi-network containers, host network, bind mounts, overlay networks |
| `Kubernetes Fundamentals/` | Minikube setup, cluster architecture, core objects, the Kubernetes Basics tutorial |
| `Kubernetes Workloads/` | Rolling update, blue-green, canary and recreate strategies; the twelve-state Pod lifecycle lab |
| `Kubernetes Services/` | The five Service types, object comparisons, FQDN and CoreDNS notes |
| `Kubernetes Ingress ConfigMaps Secrets/` | ConfigMap and Secret injection, path-based Ingress, troubleshooting, Ingress vs controller |
| `Kubernetes Storage HPA Probes/` | emptyDir, hostPath, PV/PVC, StorageClass; HPA under load; a probes-plus-PVC mini project |
| `Helm/` | Helm command tour, upgrade and rollback cycle, a chart with dev and prod value files |
| `CI-CD Pipeline/` | GitHub Actions: lint, matrix tests, image publish to GHCR, smoke test of the published image |
| `DevSecOps Pipeline/` | Build, test, SAST, SCA, secret scan, image scan, security gate, push, deploy to kind |

Environment: macOS with Docker Desktop; Linux-only commands were run in Ubuntu 24.04 containers.
The Kubernetes work used Minikube with the Docker driver. The two pipelines run on GitHub Actions;
their workflow files are in `.github/workflows/`.

# Troubleshooting challenge

Two faults introduced into a working release, each diagnosed with commands before any YAML
was touched. The method is the one from [Kubernetes Troubleshooting](../../Kubernetes%20Troubleshooting/):
status, then events, then logs, then the path.

## Fault 1: backend cannot reach the database

`fault-1-wrong-db-host.yaml` is a Helm values override that sets the ConfigMap's `POSTGRES_HOST`
to a Service that does not exist.

**Symptom.** After `helm upgrade -f fault-1-wrong-db-host.yaml`, new backend Pods never become
Ready; the rollout stalls; the old Pods keep serving (rolling update protects users).
**Investigation.** `kubectl get pods` shows the new ReplicaSet's Pods `0/1` with restarts;
`kubectl logs` shows Alembic failing to resolve `tracker-postgres-typo`; `kubectl get svc`
lists the real name; `kubectl get configmap tracker-config -o yaml` shows the bad value.
**Root cause.** Wrong hostname in configuration. DNS is fine, the database is fine.
**Fix.** `helm rollback tracker` (or re-apply the correct values). Rollout completes.

## Fault 2: the Ingress sends /api to the wrong Service

`fault-2-ingress-wrong-service.yaml` edits the Ingress so `/api` points at `tracker-frontend`.

**Symptom.** The UI loads but shows "backend unreachable"; `curl /api/issues/stats` through
the Ingress returns the SPA's `index.html` instead of JSON.
**Investigation.** `kubectl describe ingress tracker` shows `/api -> tracker-frontend:80`;
`kubectl get svc` confirms the backend Service exists and has endpoints; `curl` to the backend
Service from inside the cluster works, so the application is healthy and only the routing is wrong.
**Root cause.** Ingress path misrouted.
**Fix.** `kubectl apply` the correct Ingress (or `helm upgrade` with the chart's template).

Both runs are captured in the project README. The lesson both share: when the status is
`Running` and the symptom is "wrong answer", the application is usually innocent and the
wiring (config, DNS names, routing) is where to look.

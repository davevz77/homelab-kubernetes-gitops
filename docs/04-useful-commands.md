# Useful Commands / Comandos Útiles

## English

This document contains useful commands for operating and validating the Kubernetes homelab.

## Español

Este documento contiene comandos útiles para operar y validar el homelab Kubernetes.

---

## Cluster status / Estado del clúster

```bash
kubectl get nodes -o wide
kubectl get pods -A
kubectl get ingress -A
kubectl top nodes
kubectl top pods -A
```

---

## Traefik

```bash
kubectl get pods -n traefik
kubectl get svc -n traefik
kubectl get ingress -A
```

---

## MetalLB

```bash
kubectl get pods -n metallb-system
kubectl get ipaddresspool -n metallb-system
kubectl get l2advertisement -n metallb-system
```

---

## Monitoring / Monitoreo

```bash
kubectl get pods -n monitoring
kubectl get svc -n monitoring
kubectl get ingress -n monitoring
```

---

## Grafana

```bash
kubectl get secret -n monitoring kps-grafana \
  -o jsonpath="{.data.admin-password}" | base64 --decode; echo
```

---

## Loki labels

```bash
kubectl -n monitoring run loki-labels \
  --rm -i \
  --restart=Never \
  --image=curlimages/curl \
  -- sh -c 'curl -s http://loki-gateway.monitoring.svc.cluster.local/loki/api/v1/labels'
```

---

## Loki query example

```bash
kubectl -n monitoring run loki-query-demo \
  --rm -i \
  --restart=Never \
  --image=curlimages/curl \
  -- sh -c 'curl -sG http://loki-gateway.monitoring.svc.cluster.local/loki/api/v1/query_range --data-urlencode "query={namespace=\"demo\"}" --data-urlencode "limit=20" --data-urlencode "since=1h"'
```

---

## Argo CD

```bash
kubectl get pods -n argocd
kubectl get application -n argocd
kubectl get ingress -n argocd
```

Initial admin password:

```bash
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 --decode; echo
```

---

## Gatus

```bash
kubectl get pods -n gatus
kubectl get svc -n gatus
kubectl get ingress -n gatus
kubectl get application gatus -n argocd
```

---

## Local lab URLs

```text
http://web.lab.local
http://grafana.lab.local
http://argocd.lab.local
http://gatus.lab.local
```

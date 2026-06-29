# Architecture / Arquitectura

## English

This homelab is based on a small Kubernetes cluster running on VMware Workstation.

The cluster uses one control plane node and two worker nodes. A separate management VM is used to run kubectl, Helm and other administrative tools.

Traffic enters the cluster through Traefik, which receives a local LoadBalancer IP from MetalLB. Applications are exposed using local DNS names such as `grafana.lab.local`, `argocd.lab.local` and `gatus.lab.local`.

Observability is provided by Prometheus, Grafana, Loki and Fluent Bit.

## Español

Este homelab está basado en un clúster pequeño de Kubernetes corriendo sobre VMware Workstation.

El clúster usa un nodo control plane y dos nodos worker. Una VM separada de administración se usa para ejecutar kubectl, Helm y otras herramientas administrativas.

El tráfico entra al clúster por Traefik, que recibe una IP local tipo LoadBalancer desde MetalLB. Las aplicaciones se publican usando nombres DNS locales como `grafana.lab.local`, `argocd.lab.local` y `gatus.lab.local`.

La observabilidad se implementa con Prometheus, Grafana, Loki y Fluent Bit.

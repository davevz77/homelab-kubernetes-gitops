# Homelab Kubernetes GitOps Platform

## English

This repository documents my personal Kubernetes homelab built from scratch using VMware Workstation, Ubuntu Server, kubeadm, Cilium, MetalLB, Traefik, Prometheus, Grafana, Loki, Fluent Bit, Argo CD and Gatus.

The goal of this project is to practice real DevOps, Kubernetes, observability and GitOps concepts in a home lab environment, using a practical and incremental approach.

This lab was built as a learning platform to improve my hands-on skills in Kubernetes administration, troubleshooting, infrastructure automation, monitoring, logging and GitOps application delivery.

## Architecture Overview

The lab runs on a VMware Workstation environment with multiple Ubuntu Server virtual machines.

Main components:

* `k8s-cp01`: Kubernetes control plane node
* `k8s-worker01`: Kubernetes worker node
* `k8s-worker02`: Kubernetes worker node
* `devops-tools01`: Management workstation for kubectl, Helm, Cilium CLI and GitOps operations

Core platform services:

* Kubernetes installed with kubeadm
* Cilium as the CNI plugin
* CoreDNS for internal service discovery
* Metrics Server for basic resource metrics
* MetalLB for local LoadBalancer IP allocation
* Traefik as the Ingress Controller
* Prometheus and Grafana for monitoring
* Loki and Fluent Bit for centralized logging
* Argo CD for GitOps
* Gatus as the first GitOps-managed application

## What I Built

I started by creating the virtual machines, assigning static IP addresses and preparing the Linux operating system with the required Kubernetes dependencies.

After that, I initialized the Kubernetes control plane with kubeadm, joined the worker nodes, installed Cilium for pod networking and validated DNS resolution inside the cluster.

Then I installed the base platform services:

* Metrics Server to use `kubectl top`
* MetalLB to provide LoadBalancer IPs in my local network
* Traefik to expose applications using local DNS names
* Prometheus and Grafana for monitoring dashboards
* Loki and Fluent Bit for log aggregation
* Argo CD to manage applications using GitOps principles

Finally, I deployed Gatus through Argo CD as my first GitOps-managed application.

## Current Lab URLs

These services are exposed through Traefik using local DNS entries in `/etc/hosts`:

| Service  | URL                        |
| -------- | -------------------------- |
| Grafana  | `http://grafana.lab.local` |
| Argo CD  | `http://argocd.lab.local`  |
| Gatus    | `http://gatus.lab.local`   |
| Web Demo | `http://web.lab.local`     |

## Skills Practiced

This project helped me practice:

* Kubernetes cluster bootstrap with kubeadm
* Linux networking and static IP configuration
* Container runtime configuration with containerd
* Cilium CNI installation and validation
* Kubernetes Services and Ingress
* Local LoadBalancer implementation with MetalLB
* Application publishing with Traefik
* Kubernetes metrics with Metrics Server
* Monitoring with Prometheus and Grafana
* Centralized logging with Loki and Fluent Bit
* GitOps application deployment with Argo CD
* Helm-based application deployment
* Troubleshooting real Kubernetes issues

## Troubleshooting Highlights

During the implementation, I faced and resolved several real issues:

* Incorrect node hostnames during initial Kubernetes join
* Metrics Server certificate validation errors with kubelet
* Loki failing with a read-only filesystem error
* Fluent Bit sending logs without Kubernetes metadata labels
* Loki queries failing because the wrong query endpoint was used
* Grafana Loki queries returning no data due to missing labels

These issues were useful because they helped me understand how Kubernetes components behave in real scenarios.

## Next Steps

Planned improvements:

* Move all application definitions into a GitOps repository
* Add persistent storage for Loki and other applications
* Add more applications to Argo CD
* Add dashboards for application-level monitoring
* Add alerting rules in Prometheus and Alertmanager
* Create a full documentation site for the lab
* Add CI/CD examples

---

# Plataforma Homelab Kubernetes con GitOps

## Español

Este repositorio documenta mi laboratorio personal de Kubernetes construido desde cero usando VMware Workstation, Ubuntu Server, kubeadm, Cilium, MetalLB, Traefik, Prometheus, Grafana, Loki, Fluent Bit, Argo CD y Gatus.

El objetivo de este proyecto es practicar conceptos reales de DevOps, Kubernetes, observabilidad y GitOps en un ambiente de laboratorio en casa, de forma práctica e incremental.

Este laboratorio fue creado como una plataforma de aprendizaje para mejorar mis habilidades prácticas en administración de Kubernetes, troubleshooting, automatización de infraestructura, monitoreo, logging y despliegue de aplicaciones con GitOps.

## Resumen de Arquitectura

El laboratorio corre sobre VMware Workstation con varias máquinas virtuales Ubuntu Server.

Componentes principales:

* `k8s-cp01`: nodo control plane de Kubernetes
* `k8s-worker01`: nodo worker de Kubernetes
* `k8s-worker02`: nodo worker de Kubernetes
* `devops-tools01`: máquina de administración para kubectl, Helm, Cilium CLI y operaciones GitOps

Servicios principales de la plataforma:

* Kubernetes instalado con kubeadm
* Cilium como plugin de red CNI
* CoreDNS para resolución interna de servicios
* Metrics Server para métricas básicas de recursos
* MetalLB para asignar IPs tipo LoadBalancer en la red local
* Traefik como Ingress Controller
* Prometheus y Grafana para monitoreo
* Loki y Fluent Bit para logs centralizados
* Argo CD para GitOps
* Gatus como primera aplicación administrada por GitOps

## Qué construí

Primero creé las máquinas virtuales, asigné IPs estáticas y preparé el sistema operativo Linux con las dependencias necesarias para Kubernetes.

Después inicialicé el control plane de Kubernetes con kubeadm, uní los nodos worker, instalé Cilium para la red de pods y validé la resolución DNS interna del clúster.

Luego instalé los servicios base de la plataforma:

* Metrics Server para usar `kubectl top`
* MetalLB para entregar IPs LoadBalancer en mi red local
* Traefik para publicar aplicaciones usando nombres locales
* Prometheus y Grafana para dashboards de monitoreo
* Loki y Fluent Bit para centralizar logs
* Argo CD para administrar aplicaciones con principios GitOps

Finalmente desplegué Gatus usando Argo CD como mi primera aplicación administrada por GitOps.

## URLs actuales del laboratorio

Estos servicios están publicados con Traefik usando entradas locales en `/etc/hosts`:

| Servicio | URL                        |
| -------- | -------------------------- |
| Grafana  | `http://grafana.lab.local` |
| Argo CD  | `http://argocd.lab.local`  |
| Gatus    | `http://gatus.lab.local`   |
| Web Demo | `http://web.lab.local`     |

## Habilidades practicadas

Este proyecto me ayudó a practicar:

* Creación de un clúster Kubernetes con kubeadm
* Configuración de red e IPs estáticas en Linux
* Configuración de containerd como runtime de contenedores
* Instalación y validación de Cilium CNI
* Kubernetes Services e Ingress
* Implementación de LoadBalancer local con MetalLB
* Publicación de aplicaciones con Traefik
* Métricas de Kubernetes con Metrics Server
* Monitoreo con Prometheus y Grafana
* Logs centralizados con Loki y Fluent Bit
* Despliegue de aplicaciones con GitOps usando Argo CD
* Despliegue de aplicaciones basadas en Helm
* Troubleshooting real de Kubernetes

## Problemas resueltos durante la práctica

Durante la implementación encontré y resolví varios problemas reales:

* Hostnames incorrectos durante el join inicial de nodos Kubernetes
* Errores de certificados en Metrics Server al consultar kubelet
* Loki fallando por un error de filesystem en modo solo lectura
* Fluent Bit enviando logs sin metadata correcta de Kubernetes
* Consultas de Loki fallando por usar el endpoint incorrecto
* Grafana sin mostrar logs porque faltaban labels como `namespace`, `pod` y `container`

Estos problemas fueron útiles porque me ayudaron a entender cómo se comportan los componentes de Kubernetes en escenarios reales.

## Próximos pasos

Mejoras planeadas:

* Mover todas las definiciones de aplicaciones a un repositorio GitOps
* Agregar almacenamiento persistente para Loki y otras aplicaciones
* Agregar más aplicaciones administradas por Argo CD
* Agregar dashboards para monitoreo a nivel de aplicación
* Agregar reglas de alertas en Prometheus y Alertmanager
* Crear documentación más completa del laboratorio
* Agregar ejemplos de CI/CD


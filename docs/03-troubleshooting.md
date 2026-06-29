# Troubleshooting Notes / Notas de Troubleshooting

## English

This document summarizes real issues found and solved during the Kubernetes homelab implementation.

## 1. Incorrect Kubernetes node names

During the first cluster join, some nodes appeared with unexpected names. Since the cluster was still empty, the cleanest solution was to reset the affected nodes, correct the hostnames and rejoin them using explicit node names.

Validation command:

```bash
kubectl get nodes -o wide
```

## 2. Metrics Server kubelet certificate error

Metrics Server initially failed to collect metrics because kubelet certificates did not contain the expected IP Subject Alternative Names.

The issue was solved by configuring Metrics Server with:

```bash
--kubelet-insecure-tls
--kubelet-preferred-address-types=InternalIP
```

Validation commands:

```bash
kubectl top nodes
kubectl top pods -A
```

## 3. Loki read-only filesystem error

Loki initially failed with a read-only filesystem error when trying to write to `/var/loki`.

The issue was solved by disabling read-only root filesystem for Loki and mounting `/var/loki` using an `emptyDir` volume for lab purposes.

Validation commands:

```bash
kubectl get pods -n monitoring | grep loki
kubectl logs -n monitoring loki-0 -c loki --tail=80
```

## 4. Fluent Bit missing Kubernetes labels

Fluent Bit was sending logs to Loki, but Loki only showed basic labels such as `job` and `service_name`.

The issue was caused by an incorrect `Label_Map_Path`.

Incorrect path:

```text
/fluent-bit/etc/labelmap.json
```

Correct path:

```text
/fluent-bit/etc/conf/labelmap.json
```

After fixing it, Loki showed useful Kubernetes labels such as:

```text
namespace
pod
container
node
```

Validation query in Grafana Explore:

```logql
{namespace="demo"} |= "GET"
```

---

# Español

Este documento resume problemas reales encontrados y resueltos durante la implementación del homelab Kubernetes.

## 1. Nombres incorrectos de nodos Kubernetes

Durante el primer join del clúster, algunos nodos aparecieron con nombres incorrectos. Como el clúster todavía no tenía aplicaciones importantes, la mejor solución fue resetear los nodos afectados, corregir los hostnames y unirlos de nuevo usando nombres explícitos.

Comando de validación:

```bash
kubectl get nodes -o wide
```

## 2. Error de certificados en Metrics Server

Metrics Server inicialmente no podía recolectar métricas porque los certificados de kubelet no tenían los IP Subject Alternative Names esperados.

El problema se resolvió configurando Metrics Server con:

```bash
--kubelet-insecure-tls
--kubelet-preferred-address-types=InternalIP
```

Comandos de validación:

```bash
kubectl top nodes
kubectl top pods -A
```

## 3. Error de filesystem de solo lectura en Loki

Loki inicialmente falló porque intentaba escribir en `/var/loki`, pero el filesystem estaba en modo solo lectura.

El problema se resolvió desactivando el read-only root filesystem para Loki y montando `/var/loki` usando un volumen `emptyDir` para el laboratorio.

Comandos de validación:

```bash
kubectl get pods -n monitoring | grep loki
kubectl logs -n monitoring loki-0 -c loki --tail=80
```

## 4. Fluent Bit sin labels de Kubernetes

Fluent Bit estaba enviando logs a Loki, pero Loki solo mostraba labels básicas como `job` y `service_name`.

El problema era una ruta incorrecta en `Label_Map_Path`.

Ruta incorrecta:

```text
/fluent-bit/etc/labelmap.json
```

Ruta correcta:

```text
/fluent-bit/etc/conf/labelmap.json
```

Después de corregirlo, Loki mostró labels útiles de Kubernetes como:

```text
namespace
pod
container
node
```

Consulta de validación en Grafana Explore:

```logql
{namespace="demo"} |= "GET"
```
